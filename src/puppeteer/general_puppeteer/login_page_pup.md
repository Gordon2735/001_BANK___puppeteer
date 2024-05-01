# [Help with login a page using puppeteer](https://forum.codewithmosh.com/t/help-with-login-a-page-using-puppeteer/24372)

[Node](https://forum.codewithmosh.com/c/node/9)

You have selected **0** posts.

[select all](https://forum.codewithmosh.com/t/help-with-login-a-page-using-puppeteer/24372)

[cancel selecting](https://forum.codewithmosh.com/t/help-with-login-a-page-using-puppeteer/24372)

#### 1

/

#### 1

[![](https://sea2.discourse-cdn.com/business7/user_avatar/forum.codewithmosh.com/malathsam1994/48/3025_2.png)](https://forum.codewithmosh.com/u/Malathsam1994)

[Malathsam1994](https://forum.codewithmosh.com/u/Malathsam1994)

[Jan 1](https://forum.codewithmosh.com/t/help-with-login-a-page-using-puppeteer/24372 'Post date')

Hi all,

I posted a thread about three months ago, inquiring about an idea I had to create a web scraping script for tracking specific information. The purpose is to notify me if someone puts their ticket up for sale, allowing me to either purchase it for myself or buy extras for friends when I plan to attend a match at the stadium

I began implementing this script but encountered an issue initially—I am unable to log in with my credentials, especially when using headless mode. Removing the headless property poses a challenge as it prevents the script from locating the #Username indicator.

I understand that this may not be the most proficient approach, but initially, I wanted to test the script to determine its feasibility. So, technically, my steps would be:

1-Call Login Page of FC Bayern website and fill username and password fields and click the login button  
2-navigate to home screen URL  
3-navigate to tickets page  
4-navigate to Online Tickets page (which there exists the selector from which I will get the text data I need)

Below is a sample code; however, I have commented out the remaining code (Steps 3+4+5) as I am already experiencing issues in Step 1.

```typescript
const puppeteer = require('puppeteer');
const fs = require('fs/promises')

async function loginAndNavigate() {
const browser = await puppeteer.launch({headless: false, ignoreHTTPSErrors: true/_,args: ['--proxy-server=${proxy}']_/}) // Open browser in non-headless mode for visibility
const page = await browser.newPage();

    try {
      // Step 1: Navigate to the login page
      const loginUrl = 'https://id.fcbayern.com/auth/realms/fcbayern/protocol/openid-connect/auth?client_id=website&redirect_uri=https%3A%2F%2Ffcbayern.com%2Fde&state=f4111a58-e420-4a8b-88cd-7b52992ccb84&response_mode=fragment&response_type=code&scope=openid%20bpid&nonce=cb1c30f4-8c68-485f-89d4-32246d284f35';
      await page.goto(loginUrl, { waitUntil: 'domcontentloaded' });

      // Step 2: Fill in the login form
      await page.type('#username', 'malath_1994@yahoo.com');
      await page.type('#password', '************');
     //await page.click('.mdc-button primary-button span #kc-login');
     // Replace '#loginButton' with the actual selector for the login button

      // Step 3: Wait for navigation after login
      //await page.waitForNavigation({ waitUntil: 'domcontentloaded' });

      // Step 4: Navigate to the home page after successful login
      //const homePageUrl = 'https://fcbayern.com/de#state=01212e65-032e-4465-8d7c-abd5ae2ba295&session_state=9e924de6-561b-474b-a7d5-74a2ec6120eb&code=fb6fa234-94c2-4235-aba2-3048cd09c781.9e924de6-561b-474b-a7d5-74a2ec6120eb.86a7612e-c59a-4add-af7b-0daf86b93a2e';
      //await page.goto(homePageUrl, { waitUntil: 'domcontentloaded' });

      // Step 4: Navigate to the Tickets Page
      //const mainTicketsPageUrl = 'https://fcbayern.com/de/tickets';
      //await page.goto(mainTicketsPageUrl, { waitUntil: 'domcontentloaded' });

      // Step 5: Navigate to the Online Tickets Page
      //const onlineTicketsPageUrl = 'https://tickets.fcbayern.com/internetverkauf/start.aspx?session_state=53e30b30-3446-48fd-b4fb-e896c488c298&code=79e00b28-6124-4b54-a2c8-0706d1bd8e36.53e30b30-3446-48fd-b4fb-e896c488c298.f2f80aa0-ba29-4cb6-b52f-31beed21115a';
      //await page.goto(onlineTicketsPageUrl, { waitUntil: 'domcontentloaded' });
      //const selector = '[class="width-limiter__WidthLimiter-sc-cmigic-0 carousel-v1__ContentContainer-sc-1qr18n7-3 cXRQmb dFkUHA"]';
      //await page.click(selector); // Replace with the actual selector for the "Anmelden" button

      /*const availableMatches = await page.evaluate(() => {
        const selector = '.fcb-gr-8 .fcb-row strong';
        const elements = Array.from(document.querySelectorAll(selector));
        const matches = elements.map(elem => elem.textContent.trim());
        return matches;
      });

      console.log(availableMatches);
      */

    } catch (error) {
      console.error('Error:', error);
    } finally {
      // Close the browser
      //await browser.close();
    }

}

loginAndNavigate();
```

The problem persists even if I manually navigate to the login page. I encounter this error on the website. However, if I try the same process using the standard Chrome browser, I am able to log in normally.

[![image](https://global.discourse-cdn.com/business7/uploads/codewithmosh/optimized/2X/d/d11504a03be1fa0dbdd0e485412e5976d629b3b6_2_645x499.png)

image1283×994 65.6 KB

](https://global.discourse-cdn.com/business7/uploads/codewithmosh/original/2X/d/d11504a03be1fa0dbdd0e485412e5976d629b3b6.png "image")

I read on Google that I can obtain additional information in Google Chrome using the Network tab, but I am unsure about the specific steps to take.

I hope someone can assist me in this matter. Primarily, I am facing two issues: how to address the current problem and, more broadly, how to handle automatic website redirections in web scraping.

Thank you, and I wish you a good start to this new year.
