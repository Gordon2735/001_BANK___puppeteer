# How do I Test for an Empty JavaScript Object?

![](/static/ghost-a2dfd8493b850dc0d9a9b1b4a41011c6.png)

#### Matthew C.

December 15, 2022

## [](https://sentry.io/answers/how-do-i-test-for-an-empty-javascript-object/#the-problem)The Problem

You want to check if an object, for example, an object returned from a fetch request, is empty. How do you do this?

## [](https://sentry.io/answers/how-do-i-test-for-an-empty-javascript-object/#the-solution)The Solution

There are various ways to check if an object is empty. The method you choose to use depends on whether you know if the value to check will be an object. The methods also have different efficiencies in terms of operations per second, which could be important if you are checking many values.

### [](https://sentry.io/answers/how-do-i-test-for-an-empty-javascript-object/#using-objectkeys)Using `Object.keys`

If you know the value you are checking is an object, you can use [`Object.keys`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys#browser_compatibility) to return an array of a passed-in object’s property names. If the object is empty, the length of the returned array will be 0:


```javascript
Object.keys(value).length === 0
``` 

### [](https://sentry.io/answers/how-do-i-test-for-an-empty-javascript-object/#using-a-forin-loop)Using a `for...in` Loop

You can use a [`for...in`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in) loop in a function to check if an object is empty. Pass in the value as an argument and loop through each property in the value:

Click to Copy

```javascript
function isEmpty(value) {
  for (let prop in value) {
    if (value.hasOwnProperty(prop)) return false;
  }
  return true;
}
``` 

For each property, check if the property exists. If there is a property, the function will return `false`. If there are no properties on the object, the function returns `true`. This method was used as an alternative to using `Object.keys` before it was added to JavaScript in the 2011 [ECMAScript 5 specification](https://262.ecma-international.org/5.1/) and is widely supported by browsers.

### [](https://sentry.io/answers/how-do-i-test-for-an-empty-javascript-object/#using-jsonstringify)Using `JSON.stringify`

You can use [`JSON.stringify()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify) to convert the value to a JSON string to check if the value is an empty object. It will be equal to an empty object string if it is:

Click to Copy

```javascript
JSON.stringify(value) === '{}'
``` 

This method is slower than the other methods.

### [](https://sentry.io/answers/how-do-i-test-for-an-empty-javascript-object/#adding-extra-checks-if-you-dont-know-if-the-value-is-an-object)Adding Extra Checks if You Don’t Know if the Value is an Object

If you don’t know if the value is an object, you’ll need to add some extra checks to determine whether it is. First, check if the value is `null` or `undefined`:

Click to Copy

```javascript
value && Object.keys(value).length === 0;
``` 

If you don’t do this check, you’ll get the following error if the value of `value` is `null` or `undefined`:

Click to Copy

`Cannot convert undefined or null to object` 

You can end up with false positives if the value is a JavaScript object constructor, such as `new Date()` or `new RegExp()`:

Click to Copy

```javascript
function isEmpty(value) {
  return value && Object.keys(value).length === 0;
}

console.log(new Date()); // Date Tue Nov 29 2022 18:18:10 GMT+0200 (South Africa Standard Time)
console.log(isEmpty(new Date())); // true
``` 

To fix this, you can also check that the constructor of the value is an object:

Click to Copy

```javascript
value.constructor === Object;
``` 

## Get Started With Sentry

Get actionable, code-level insights to resolve JavaScript performance bottlenecks and errors.

1. Create a free [Sentry account](https://sentry.io/signup)
    
2. Create a JavaScript project and note your DSN
    
3. Grab the [Sentry JavaScript SDK](https://github.com/getsentry/sentry-javascript/)
    

Click to Copy

```html
<script src="https://browser.sentry-cdn.com/7.112.2/bundle.min.js"></script>
```


4. Configure your DSN

Click to Copy

```javascript
Sentry.init({ dsn: 'https://<key>@sentry.io/<project>' });
``` 

Loved by over 4 million developers and more than 90,000 organizations worldwide, Sentry provides code-level observability to many of the world’s best-known companies like Disney, Peloton, Cloudflare, Eventbrite, Slack, Supercell, and Rockstar Games. Each month we process billions of exceptions from the most popular products on the internet.

[learn more about sentry](https://sentry.io/)[join our discord](https://discord.com/invite/Ww9hbqr)