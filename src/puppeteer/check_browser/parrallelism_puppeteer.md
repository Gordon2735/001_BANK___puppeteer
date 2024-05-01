# [Parallelism of Puppeteer with Express Router Node JS. How to pass page between routes while maintaining concurrency](https://stackoverflow.com/questions/66935883/parallelism-of-puppeteer-with-express-router-node-js-how-to-pass-page-between-r)

[Ask Question](https://stackoverflow.com/questions/ask)

Asked 3 years ago

Modified [3 years ago](https://stackoverflow.com/questions/66935883/parallelism-of-puppeteer-with-express-router-node-js-how-to-pass-page-between-r?lastactivity '2021-04-05 00:30:26Z')

Viewed 2k times

This question shows research effort; it is useful and clear

3

This question does not show any research effort; it is unclear or not useful

Save this question.

[](https://stackoverflow.com/posts/66935883/timeline)

Show activity on this post.

```javascript
app.post('/api/auth/check', async (req, res) => {
try {
  const browser = await puppeteer.launch();
  const page = await browser.newPage();
  await page.goto(
    'https://www.google.com'
  );
  res.json({message: 'Success'})
} catch (e) {
  console.log(e);
  res.status(500).json({ message: 'Error' });
}});

app.post('/api/auth/register', async (req, res) => {
  console.log('register');
  // Here i'm need to transfer the current user session (page and browser) and then perform actions on the same page.
  await page.waitForTimeout(1000);
  await browser.close();
}});
```

Is it possible to somehow transfer page and browser from one route to another while maintaining puppeteer concurrency. If you set the variable globally, then the page and browser will be overwritten and multitasking will not work.

-   [node.js](https://stackoverflow.com/questions/tagged/node.js "show questions tagged 'node.js'")
-   [express](https://stackoverflow.com/questions/tagged/express "show questions tagged 'express'")
-   [http](https://stackoverflow.com/questions/tagged/http "show questions tagged 'http'")
-   [puppeteer](https://stackoverflow.com/questions/tagged/puppeteer "show questions tagged 'puppeteer'")
-   [express-router](https://stackoverflow.com/questions/tagged/express-router "show questions tagged 'express-router'")

[Share](https://stackoverflow.com/q/66935883/15588573 'Short permalink to this question')

Share a link to this question (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/66935883/edit 'Revise and improve this post')

Follow

Follow this question to receive notifications

[edited Apr 4, 2021 at 5:11](https://stackoverflow.com/posts/66935883/revisions 'show all edits to this post')

[

![Vaviloff's user avatar](https://i.stack.imgur.com/iwuRh.jpg?s=64&g=1)

](https://stackoverflow.com/users/2715393/vaviloff)

[Vaviloff](https://stackoverflow.com/users/2715393/vaviloff)

16.6k66 gold badges5050 silver badges6060 bronze badges

asked Apr 3, 2021 at 21:07

[

![apsenT's user avatar](https://lh3.googleusercontent.com/a-/AOh14GjUsPvGiJKjMmCa4ocJHpPZoufrzQwOIyV1lFTDWw=k-s64)

](https://stackoverflow.com/users/15547056/apsent)

[apsenT](https://stackoverflow.com/users/15547056/apsent)apsenT

3344 bronze badges

1

-   Welcome to SO! I'm not sure if the terms "parallelism", "concurrency" and "multitasking" are what you're looking for here. Node is single-threaded, async event-driven. I think you mean you want to maintain individual browser instances across routes without blocking the event loop and I answered under this assumption. Feel free to clarify if your intent is something else.
    – [ggorlen](https://stackoverflow.com/users/6243352/ggorlen '51,606 reputation')
    [Apr 5, 2021 at 0:22](https://stackoverflow.com/questions/66935883/parallelism-of-puppeteer-with-express-router-node-js-how-to-pass-page-between-r#comment118337814_66935883)

[Add a comment](https://stackoverflow.com/questions/66935883/parallelism-of-puppeteer-with-express-router-node-js-how-to-pass-page-between-r# 'Use comments to ask for more information or suggest improvements. Avoid answering questions in comments.') | [](https://stackoverflow.com/questions/66935883/parallelism-of-puppeteer-with-express-router-node-js-how-to-pass-page-between-r# 'Expand to show all comments on this post')

Report this ad

## 1 Answer 1

Sorted by: [Reset to default](https://stackoverflow.com/questions/66935883/parallelism-of-puppeteer-with-express-router-node-js-how-to-pass-page-between-r?answertab=scoredesc#tab-top)

Highest score (default) Trending (recent votes count more) Date modified (newest first) Date created (oldest first)

This answer is useful

2

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/66946923/timeline)

Show activity on this post.

One approach is to create a closure that returns promises that will resolve to the same page and browser instances. Since HTTP is stateless, I assume you have some session/authentication management system that associates a user's session with a Puppeteer browser instance.

I've simplified your routes a bit and added a naive token management system to associate a user with a session in the interests of making a complete, runnable example but I don't think you'll have problems adapting it to your use case.

```javascript
const express = require('express');
const puppeteer = require('puppeteer');

// https://stackoverflow.com/questions/51391080/handling-errors-in-express-async-middleware
const asyncHandler = (fn) => (req, res, next) =>
    Promise.resolve(fn(req, res, next)).catch(next);
const startPuppeteerSession = async () => {
    const browser = await puppeteer.launch();
    const page = await browser.newPage();
    return { browser, page };
};
const sessions = {};

express()
    .use((req, res, next) =>
        req.query.token === undefined ? res.sendStatus(401) : next()
    )
    .get(
        '/start',
        asyncHandler(async (req, res) => {
            sessions[req.query.token] = await startPuppeteerSession();
            res.sendStatus(200);
        })
    )
    .get(
        '/navigate',
        asyncHandler(async (req, res) => {
            const page = await sessions[req.query.token].page;
            await page.goto(req.query.to || 'http://www.example.com');
            res.sendStatus(200);
        })
    )
    .get(
        '/content',
        asyncHandler(async (req, res) => {
            const page = await sessions[req.query.token].page;
            res.send(await page.content());
        })
    )
    .get(
        '/kill',
        asyncHandler(async (req, res) => {
            const browser = await sessions[req.query.token].browser;
            await browser.close();
            delete sessions[req.query.token];
            res.sendStatus(200);
        })
    )
    .use((err, req, res, next) => res.sendStatus(500))
    .listen(8000, () => console.log('listening on port 8000'));
```

Sample usage from the client's perspective:

```bash
$ curl localhost:8000/start?token=1
OK
$ curl 'localhost:8000/navigate?to=https://stackoverflow.com/questions/66935883&token=1'
OK
$ curl localhost:8000/content?token=1 | grep 'apsenT'
        <a href="/users/15547056/apsent">apsenT</a><span class="d-none" itemprop="name">apsenT</span>
            <a href="/users/15547056/apsent">apsenT</a> is a new contributor to this site. Take care in asking for clarification, commenting, and answering.
                        <a href="/users/15547056/apsent">apsenT</a> is a new contributor. Be nice, and check out our <a href="/conduct">Code of Conduct</a>.
$ curl localhost:8000/kill?token=1
OK
```

You can see the client associated with token 1 has persisted a single browser session across multiple routes. Other clients can launch browser sessions and manipulate them simultaneously.

To reiterate, this is only a proof-of-concept of sharing a Puppeteer browser instance across routes. Using the code above, a user can just spam the `start` route and create browsers until the server crashes, so this is totally unfit for production without real authentication and session management/error handling.

<sup>Packages used: express ^4.17.1, puppeteer ^8.0.0.</sup>

[Share](https://stackoverflow.com/a/66946923/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/66946923/edit 'Revise and improve this post')

Follow
