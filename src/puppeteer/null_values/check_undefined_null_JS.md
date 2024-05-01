Thursday, Jun 8th 2023

#   How to check if value is undefined or null in JavaScript

How to check if value is undefined or null in JavaScriptself.\_\_wrap\_b=(t,n,e)=>{e=e||document.querySelector(\`\[data-br="${t}"\]\`);let a=e.parentElement,r=R=>e.style.maxWidth=R+"px";e.style.maxWidth="";let o=a.clientWidth,c=a.clientHeight,i=o/2-.25,l=o+.5,u;if(o){for(;i+1<l;)u=Math.round((i+l)/2),r(u),a.clientHeight===c?l=u:i=u;r(l\*n+o\*(1-n))}e.\_\_wrap\_o||(typeof ResizeObserver!="undefined"?(e.\_\_wrap\_o=new ResizeObserver(()=>{self.\_\_wrap\_b(0,+e.dataset.brr,e)})).observe(a):process.env.NODE\_ENV==="development"&&console.warn("The browser you are using does not support the ResizeObserver API. Please consider add polyfill for this API to avoid potential layout shifts or upgrade your browser. Read more: https://github.com/shuding/react-wrap-balancer#browser-support-information"))};self.\_\_wrap\_b(":R4mr36:",1)

Posted by

[- ![Pranav's profile image](https://wsrv.nl/?url=https%3A%2F%2Fsecure.gravatar.com%2Favatar%2F1f6d6e8f7c54dd180e084023865591de%3Fs%3D96%26d%3Dmonsterid%26r%3Dg&w=80&q=82&output=webp)
    
    Pranav
    
    Team Codedamn
    ](https://codedamn.com/news/author/pranav)

Table of contents

- [Understanding Undefined and Null](https://codedamn.com/news/javascript/check-if-undefined-null#understanding_undefined_and_null)
- [Checking for Undefined or Null Using the Equality Operator (==)](https://codedamn.com/news/javascript/check-if-undefined-null#checking_for_undefined_or_null_using_the_equality_operator_)
- [Checking for Undefined or Null Using the Identity Operator (===)](https://codedamn.com/news/javascript/check-if-undefined-null#checking_for_undefined_or_null_using_the_identity_operator_)
- [Using the typeof Operator](https://codedamn.com/news/javascript/check-if-undefined-null#using_the_typeof_operator)
- [Using a Custom Utility Function](https://codedamn.com/news/javascript/check-if-undefined-null#using_a_custom_utility_function)
- [FAQ](https://codedamn.com/news/javascript/check-if-undefined-null#faq)
- [Conclusion](https://codedamn.com/news/javascript/check-if-undefined-null#conclusion)

![How to check if value is undefined or null in JavaScript](https://wsrv.nl/?url=https%3A%2F%2Fcodedamn-blog.s3.amazonaws.com%2Fwp-content%2Fuploads%2F2023%2F06%2F08112912%2Fzl3JGynpZndjeAiKZrbMm.png&w=1280&q=82&output=webp)

JavaScript is a powerful and flexible programming language that powers the modern web. One aspect of the language that can sometimes cause confusion for developers is understanding the difference between `undefined` and `null`, and how to check for these values. In this blog post, we will explore the various ways to check if a value is `undefined` or `null` in JavaScript, as well as dive deeper into what these values actually represent. This post is aimed at developers who are familiar with basics of JavaScript and want to gain a better understanding of these often misunderstood concepts.

## Understanding Undefined and Null

Before diving into the various methods of checking for `undefined` and `null`, it's important to understand what these values represent in JavaScript.

### Undefined

In JavaScript, `undefined` is a primitive value that represents the absence of any value. It is the default value of variables that have been declared but not initialized. For example:

```javascript
let myVar; console.log(myVar); // Output: undefined
```

### Null


`null` is another primitive value in JavaScript that represents the intentional absence of any value. It is often used as a default value to indicate that a variable should not have any value assigned to it. For example:

```javascript
let myVar = null; console.log(myVar); // Output: null
```

Now that we understand the difference between `undefined` and `null`, let's explore different ways to check for these values in JavaScript.

## Checking for Undefined or Null Using the Equality Operator (==)

The easiest way to check if a value is either `undefined` or `null` is by using the equality operator (`==`). The equality operator performs type coercion, which means it converts the operands to the same type before making the comparison. In the case of `undefined` and `null`, they are considered equal when using the `==` operator.

```javascript
let myVar; 
if (myVar == null) {  console.log("The value is either undefined or null"); } else {  console.log("The value is neither undefined nor null"); }
```

## Checking for Undefined or Null Using the Identity Operator (===)

If you want to check if a value is specifically `undefined` or `null` without type coercion, you can use the identity operator (`===`). The identity operator checks for both value and type equality, which means it does not perform type coercion.

```javascript
let myVar; 
if (myVar === undefined) {  console.log("The value is undefined"); } else if (myVar === null) {  console.log("The value is null"); } else {  console.log("The value is neither undefined nor null"); }
```

## Using the typeof Operator

Another way to check for `undefined` is by using the `typeof` operator. The `typeof` operator returns a string that represents the type of the given operand. When the operand is `undefined`, the `typeof` operator returns the string `"undefined"`.

```javascript
let myVar; 
if (typeof myVar === "undefined") {  console.log("The value is undefined"); } else if (myVar === null) {  console.log("The value is null"); } else {  console.log("The value is neither undefined nor null"); }
```

Note that the `typeof` operator does not help in checking for `null`, as it returns the string `"object"` when the operand is `null`.

## Using a Custom Utility Function

You can also create a custom utility function to check for `undefined` or `null` values. This can be particularly useful if you need to perform this check frequently throughout your codebase.

```javascript
function isNullOrUndefined(value) {  return value === undefined || value === null; } 
let myVar; 
if (isNullOrUndefined(myVar)) {  console.log("The value is either undefined or null"); } else {  console.log("The value is neither undefined nor null"); }
```

## FAQ

### Can I use the logical OR (||) operator to check for undefined or null?

Yes, you can use the logical OR (||) operator to provide a default value when a variable is either `undefined` or `null`. However, this approach has a limitation: it will also use the default value when the original variable is any other falsy value, such as `false`, `0`, or an empty string (`""`).

```javascript
 myVar; let result = myVar || "default value"; console.log(result); // Output: "default value"
 ```

### What is the difference between null and undefined?

In JavaScript, `undefined` is a primitive value that represents the absence of any value, while `null` is another primitive value that represents the intentional absence of any value. The main difference lies in the fact that `undefined` is the default value of uninitialized variables, whereas `null` is often used as a default value to indicate that a variable should have no value assigned to it.

### How can I check for undefined or null in a function parameter?

You can use any of the methods described in this blog post to check for `undefined` or `null` in a function parameter. For example, using the equality operator:

```javascript
function myFunction(param) {  if (param == null) {  console.log("The parameter is either undefined or null");  } else {  console.log("The parameter is neither undefined nor null");  } }
```

### What should I use as a default value for a variable, undefined or null?

It is generally recommended to use `null` as a default value for a variable when you want to indicate that it should have no value assigned to it. This is because `undefined` is the default value for uninitialized variables, and using `null` helps you explicitly convey your intent.

## Conclusion

In this blog post, we have explored various ways to check if a value is `undefined` or `null` in JavaScript, as well as gained a deeper understanding of these often misunderstood concepts. By using the methods discussed in this post, you can confidently handle `undefined` and `null` values in your JavaScript code. Remember to visit [codedamn](https://codedamn.com/) for more resources on JavaScript and other programming languages. Happy coding!

Sharing is caring

Did you like what Pranav wrote? Thank them for their work by sharing it on social media.

Share

0/10000

## No comments so far

Curious about this topic? Continue your journey with these coding courses:

[

![Course thumbnail for JavaScript from Zero to Hero with 5+ projects](https://wsrv.nl/?url=https%3A%2F%2Fs3.us-east-1.amazonaws.com%2Fcreator-assets.codedamn.com%2Fdineshlg-6400c10a7195d7001409d219%2FCOURSE_IMAGE%2F2023-03-21%2F8dd3e8f8ce066ebac34568fb081a930aa66cbda8&w=256&q=82&output=webp)

4.7

146 students learning

![Photo of DINESH KUMAR REDDY](https://wsrv.nl/?url=https%3A%2F%2Fs3.us-east-1.amazonaws.com%2Fcreator-assets.codedamn.com%2Fdineshlg-6400c10a7195d7001409d219%2FPROFILE_PICTURE%2F2024-02-25%2F1ae8958b8a6303f4b3128a9dd87759bdcad81ae1&w=96&q=82&output=webp)

DINESH KUMAR REDDY

JavaScript from Zero to Hero with 5+ projects

](https://codedamn.com/learn/javascript-with-real-world-projects)[

![Course thumbnail for Mastering Advanced JavaScript](https://wsrv.nl/?url=https%3A%2F%2Fs3.us-east-1.amazonaws.com%2Fcreator-assets.codedamn.com%2Funwiredlearning-64d22d01a9b745000d38e131%2FCOURSE_IMAGE%2F2023-09-06%2F3a24322329a9579d83c085ffc029bd589855a26e&w=256&q=82&output=webp)

5.0

105 students learning

![Photo of Shubham Sarda](https://wsrv.nl/?url=https%3A%2F%2Fs3.us-east-1.amazonaws.com%2Fcreator-assets.codedamn.com%2Funwiredlearning-64d22d01a9b745000d38e131%2FPROFILE_PICTURE%2F2023-08-08%2F479daa37d7c56a1128a1c04993eba6544d265887&w=96&q=82&output=webp)

Shubham Sarda

Mastering Advanced JavaScript

](https://codedamn.com/learn/mastering-advanced-javascript)[

![Course thumbnail for Getting Started With JavaScript](https://wsrv.nl/?url=https%3A%2F%2Fs3.us-east-1.amazonaws.com%2Fcreator-assets.codedamn.com%2Flilnop-63f50c170eb1b7000bae9fb7%2FCOURSE_IMAGE%2F2023-09-05%2F30be57abcd8d160cc1e11592fad3d8d0b82f36e2&w=256&q=82&output=webp)

5.0

![Photo of Robert Nana Sarpong](https://wsrv.nl/?url=https%3A%2F%2Fs3.us-east-1.amazonaws.com%2Fcreator-assets.codedamn.com%2Flilnop-63f50c170eb1b7000bae9fb7%2FPROFILE_PICTURE%2F2023-09-05%2Fab1f71c71fa72e6bb0495e204d5bbe8e61839544&w=96&q=82&output=webp)

Robert Nana Sarpong

Getting Started With JavaScript

](https://codedamn.com/learn/javascript-getting-started)