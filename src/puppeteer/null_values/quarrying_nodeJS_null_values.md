#   Quarrying with Puppeteer, Typescript and Node.js | Over Null Values in Classes

TypeScript is a free and open-source high-level programming language developed by Microsoft that adds static typing with optional type annotations to JavaScript. It is designed for the development of large applications and transpile's to JavaScript.

[Wikipedia](https://en.wikipedia.org/wiki/TypeScript)

![](https://encrypted-tbn1.gstatic.com/images?q=tbn:ANd9GcS2T2xeVEP510a3WXgD3UwqEs7Uom13H6bop9pDlB96F-Iq82Ps)

[Wikipedia](https://cs.wikipedia.org/wiki/TypeScript)

Node.js

Node.js is a cross-platform, open-source JavaScript runtime environment that can run on Windows, Linux, Unix, macOS, and more. Node.js runs on the V8 JavaScript engine, and executes JavaScript code outside a web browser. Node.js lets developers use JavaScript to write command line tools and for server-side scripting.

[Wikipedia](https://en.wikipedia.org/wiki/Node.js)

![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ82uBPqnWciRtiFtYrB3OCdcaZLC789VVaMpSBQzC3S1we1p12)

[Wikipedia](https://en.wikipedia.org/wiki/File:Node.js_logo.svg)

More about Node.js over null values in classes:

Puppeteer is a Node.js library that provides a high-level API for controlling Chrome. It can be used for

Web scraping, web harvesting, or web data extraction is data scraping used for extracting data from websites. Web scraping software may directly access the World Wide Web using the Hypertext Transfer Protocol or a web browser.

[Wikipedia](https://en.wikipedia.org/wiki/Web_scraping)

![](https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcSY021Uw5n_7yWkRk3W-_Hwoc4FBnDSl55NKLefAFrWzbDMYG69)

[WebHarvy](https://www.webharvy.com/articles/what-is-web-scraping.html)

More about web scraping, testing, and automation. TypeScript is a superset of JavaScript that adds static typing and other features. Node.js is a JavaScript runtime environment that allows JavaScript to be run outside of a browser.

When quarrying with Puppeteer and TypeScript and Node.js, it is important to be aware of null values in classes. Null values can occur when a property or method is not defined on a class. If you try to access a null value, you will get an error.

There are a few ways to handle null values in classes. One way is to use the TypeScript `?` operator. The `?` operator tells TypeScript that a property or method may be null. If you try to access a property or method that is null, the `?` operator will

return

Return statement

In computer programming, a return statement causes execution to leave the current subroutine and resume at the point in the code immediately after the instruction which called the subroutine, known as its return address.

[Wikipedia](https://en.wikipedia.org/wiki/Return_statement)

![](https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcToZHBIz31iHUnu1fmOUDwc3SRQuDtGjFoNWtryu71tgPAJizl5)

[C Programming Simple Steps](https://www.c-programming-simple-steps.com/return-statement.html)

More about return statements `undefined` instead of throwing an error.

Another way to handle null values in classes is to use the TypeScript `!` operator. The `!` operator tells TypeScript that a property or method is definitely not null. If you try to access a property or method that is null, the `!` operator will throw an error.

You can also use the TypeScript `typeof` operator to check the type of a property or method. If the type of a property or method is `null`, you can use the `typeof` operator to determine what to do.

For example, the following code shows how to use the `?` operator to handle a null value in a class:

```typescript
class MyClass {  
 public myProperty?: string;  
  
 public myMethod() {  
 if (this.myProperty) {  
 console.log(this.myProperty);  
 } else {  
 console.log('myProperty is null');  
 }  
 }  
}  
  
const myClass = new MyClass();  
myClass.myMethod(); // logs 'myProperty is null'
```
The following code shows how to use the `!` operator to handle a null value in a class:

```typescript
class MyClass {  
 public myProperty!: string;  
  
 public myMethod() {  
 console.log(this.myProperty);  
 }  
}  
  
const myClass = new MyClass();  
myClass.myMethod(); // throws an error
```
The following code shows how to use the `typeof` operator to handle a null value in a class:

```typescript
class MyClass {  
 public myProperty: string | null;  
  
 public myMethod() {  
 if (typeof this.myProperty === 'null') {  
 console.log('myProperty is null');  
 } else {  
 console.log(this.myProperty);  
 }  
 }  
}  
  
const myClass = new MyClass();  
myClass.myMethod(); // logs 'myProperty is null'
```

By following these tips, you can avoid errors when quarrying with Puppeteer and TypeScript and Node.js over null values in classes.