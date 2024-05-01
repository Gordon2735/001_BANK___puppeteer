<p>
    <script>Date.now()</script>
</p>

# NOTES on the child_process() Node.js Module

**What is the child_process spawn method?**

The child_process.spawn() method **spawns the child process asynchronously, without blocking the Node.js event loop**. The child_process.spawnSync() function provides equivalent functionality in a synchronous manner that blocks the event loop until the spawned process either exits or is terminated.

<br />
<br />

<span style="color: chartreuse; letter-spacing: 0.27114em; font-size: 1.3rem; font-weight: 700;">
|::::::::|::::::::|::::::::|::::::::|::::::::|::::::::|::::::::|::::::::|::::::::|::::::::|::::::::|::::::::|::::::::|::::::::|
</span>

<br />
<br />

# When does Node Spawned Child Process Actually Start?

[when does Node spawned child process actually start?](https://stackoverflow.com/questions/59798310/when-does-node-spawned-child-process-actually-start)

[Ask Question](https://stackoverflow.com/questions/ask)

Asked 4 years, 3 months ago

Modified [4 years, 3 months ago](https://stackoverflow.com/questions/59798310/when-does-node-spawned-child-process-actually-start?lastactivity '2020-01-18 10:11:35Z')

[](https://stackoverflow.com/posts/59798310/timeline)

In the [documentation for Node's Child Process `spawn()` function](https://nodejs.org/api/child_process.html), and in examples I've seen elsewhere, the pattern is to call the `spawn()` function, and _then_ to set up a bunch of handlers on the returned `ChildProcess` object. For instance, here is the first example of `spawn()` given on that documentation page:

```javascript
const { spawn } = require('child_process');
const ls = spawn('ls', ['-lh', '/usr']);

ls.stdout.on('data', (data) => {
	console.log(`stdout: ${data}`);
});

ls.stderr.on('data', (data) => {
	console.error(`stderr: ${data}`);
});

ls.on('close', (code) => {
	console.log(`child process exited with code ${code}`);
});
```

The `spawn()` function itself is called on the second line. My understanding is that `spawn()` starts a child process asynchronously. From the documentation:

> The child_process.spawn() method spawns a new process using the given command, with command line arguments in args.

**However**, the following lines of the script above go on to set up various handlers for the process, so it's assuming that the process hasn't actually started (and potentially finished) between the time `spawn()` is called on line 2 and the other stuff happens on the subsequent lines. I know JavaScript/Node is single threaded. However, the operating system is not single threaded, and naively one would read that `spawn()` call to be telling the operating system to spawn the process right now (at which point, with unfortunate timing, the OS could suspend the parent Node process and run/complete the child process before the next line of the Node code is executed).

But it must be that the process doesn't actually get spawned until the current JavaScript function completes (or more generally the current JavaScript event handler that called the current function completes), right?

That seems like a pretty important thing to say. Why doesn't it say that in the Child Process documentation page? Is there some overriding Node principle that makes it unnecessary to say that explicitly?

-   [node.js](https://stackoverflow.com/questions/tagged/node.js "show questions tagged 'node.js'")
-   [asynchronous](https://stackoverflow.com/questions/tagged/asynchronous "show questions tagged 'asynchronous'")
-   [spawn](https://stackoverflow.com/questions/tagged/spawn "show questions tagged 'spawn'")

[Share](https://stackoverflow.com/q/59798310/15588573 'Short permalink to this question')

Share a link to this question (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/59798310/edit 'Revise and improve this post')

[edited Jan 18, 2020 at 10:11](https://stackoverflow.com/posts/59798310/revisions 'show all edits to this post')

M Katz

asked Jan 18, 2020 at 7:04

[

![M Katz's user avatar](https://www.gravatar.com/avatar/560403b5eee12ac22a7a83c478ba0483?s=64&d=identicon&r=PG)

](https://stackoverflow.com/users/384670/m-katz)

[M Katz](https://stackoverflow.com/users/384670/m-katz)M Katz

5,27633 gold badges4747 silver badges6969 bronze badges

2

-   it's pretty much what explained in the nodejs doc - [nodejs.org/en/docs/guides/event-loop-timers-and-nexttick](https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/)
    – [Andy](https://stackoverflow.com/users/210085/andy '5,400 reputation')
    [Jan 18, 2020 at 7:14](https://stackoverflow.com/questions/59798310/when-does-node-spawned-child-process-actually-start#comment105737804_59798310)
-   @Andy, thanks. I see that doc does talk about this issue, although it didn't clarify things for me in the same was as jfriend00's answer.
    – [M Katz](https://stackoverflow.com/users/384670/m-katz '5,276 reputation')
    [Jan 18, 2020 at 8:33](https://stackoverflow.com/questions/59798310/when-does-node-spawned-child-process-actually-start#comment105738669_59798310)

[Add a comment](https://stackoverflow.com/questions/59798310/when-does-node-spawned-child-process-actually-start# 'Use comments to ask for more information or suggest improvements. Avoid answering questions in comments.') | [](https://stackoverflow.com/questions/59798310/when-does-node-spawned-child-process-actually-start# 'Expand to show all comments on this post')

Report this ad

## 2 Answers 2

Sorted by: [Reset to default](https://stackoverflow.com/questions/59798310/when-does-node-spawned-child-process-actually-start?answertab=scoredesc#tab-top)

Highest score (default) Trending (recent votes count more) Date modified (newest first) Date created (oldest first)

This answer is useful

5

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/59798469/timeline)

Show activity on this post.

The spawning of the new process starts immediately (it's handed over to the OS to actually fire up the process and get it going). Starting the new process with `.spawn()` is asynchronous and non-blocking. So, it will initiate the operation with the OS and immediately return. You might think that that's why it's OK to set up event handlers after it returns (because the process hasn't yet finished starting). Well, yes and no. It likely hasn't yet finished starting the new process, but that isn't the main reason why it's OK.

It's OK, because node.js runs all its events through a single threaded event queue. Thus no events from the newly spawned process can be processed until after your code finishes executing and returns control back to the system. Only then can it process the next event in the event queue and trigger one of the events you are registering handlers for.

Or, said another way, none of the events from the other process are pre-emptive. They won't/can't interrupt your existing Javascript code. So, since you're still running your Javascript code, those events can't get run yet. Instead, they sit in the event queue until your Javascript code finishes and then the interpreter can go get the next event from the event queue and run the callback associated with it. Likewise, that callback runs until it returns back to the interpreter and then the interpreter can get the next event and run its callback and so on...

That's why node.js is called an event-driven system.

As such, it's perfectly fine to do this type of structure:

```javascript
const { spawn } = require('child_process');
const ls = spawn('ls', ['-lh', '/usr']);

ls.stdout.on('data', (data) => {
	console.log(`stdout: ${data}`);
});

ls.stderr.on('data', (data) => {
	console.error(`stderr: ${data}`);
});

ls.on('close', (code) => {
	console.log(`child process exited with code ${code}`);
});
```

None of those `data` or `close` events can execute their callbacks until after your code is done and returns control back to the system. So, it's perfectly safe to set up those event handlers like you are. Even if the newly spawned process was running and generating events right away, those events will just sit in the event queue until your Javascript finishes what it is doing (which includes setting up your event handlers).

Now, if you delayed setting up the event handlers until some future tick of the event loop (as shown below) with something like a `setTimeout()`, then you could miss some events:

```javascript
const { spawn } = require('child_process');
const ls = spawn('ls', ['-lh', '/usr']);

setTimeout(() => {
	ls.stdout.on('data', (data) => {
		console.log(`stdout: ${data}`);
	});

	ls.stderr.on('data', (data) => {
		console.error(`stderr: ${data}`);
	});

	ls.on('close', (code) => {
		console.log(`child process exited with code ${code}`);
	});
}, 10);
```

Here you are not setting up the event handlers immediately as part of the same tick of the event loop, but after a short delay. Therefore some events could get processed from the event loop before you install your event handlers and you could miss some of these events. Obviously, you would never do it this way (on purpose), but I just wanted to show that code running on the same tick of the event loop does not have a problem, but code running on some future tick of the event loop could have a problem missing events.

[Share](https://stackoverflow.com/a/59798469/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/59798469/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited Jan 18, 2020 at 7:37](https://stackoverflow.com/posts/59798469/revisions 'show all edits to this post')

answered Jan 18, 2020 at 7:30

[

![jfriend00's user avatar](https://i.stack.imgur.com/Xu7hp.jpg?s=64&g=1)

](https://stackoverflow.com/users/816620/jfriend00)

[jfriend00](https://stackoverflow.com/users/816620/jfriend00)jfriend00

697k9999 gold badges1k1k silver badges1k1k bronze badges

1

-   Thanks for the explanation. I'm going to add my own answer to follow up on your answer, explaining the specific thing your answer helped me understand.
    – [M Katz](https://stackoverflow.com/users/384670/m-katz '5,276 reputation')
    [Jan 18, 2020 at 8:13](https://stackoverflow.com/questions/59798310/when-does-node-spawned-child-process-actually-start#comment105738443_59798469)

[Add a comment](https://stackoverflow.com/questions/59798310/when-does-node-spawned-child-process-actually-start# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/59798310/when-does-node-spawned-child-process-actually-start# 'Expand to show all comments on this post')

This answer is useful

1

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/59798772/timeline)

Show activity on this post.

This is to follow up on jfriend00's answer, to explain what it helped me understand, in case it helps someone else. I knew about the event-driven nature of JavaScript/Node. What jfriend00's explanation made clear to me is the idea that an event can happen and Node can be aware that it happened, but it doesn't actually decide which handlers to tell about that event until the next tick. For instance, if the `spawn()` call fails outright (e.g., command does not exist), Node obviously knows that immediately. My thought was that it would then immediately queue the appropriate handlers to run on the next tick. But what I now understand is that it puts the "raw event" (i.e., the fact that the spawn failed, with whatever details about that) in its queue, and then on the next tick it _determines_ and calls the appropriate handlers. And the same is true for other events like receiving output from the process, etc. The event is saved but the appropriate handlers for the event are only determined when the next tick runs, so handlers assigned on the previous tick, after spawn(), will get called.

[Share](https://stackoverflow.com/a/59798772/15588573 'Short permalink to this answer')

<br />
<br />

<span style="color: chartreuse; letter-spacing: 0.27114em; font-size: 1.3rem; font-weight: 700;">
|::::::::|::::::::|::::::::|::::::::|::::::::|::::::::|::::::::|::::::::|::::::::|::::::::|::::::::|::::::::|::::::::|::::::::|
</span>

<br />
<br />
