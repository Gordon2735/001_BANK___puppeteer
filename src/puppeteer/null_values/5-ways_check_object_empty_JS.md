# 5 Ways to Check If an Object Is Empty in JavaScript

Here are a few quick and easy ways to check if an object is empty in JavaScript.

![](https://builtin.com/cdn-cgi/image/f=auto,quality=80,width=48,height=48/https://builtin.com/sites/www.builtin.com/files/styles/64_x_64/public/2022-06/Saravanan%2C%20K.%20Jagathish.png)

Written by[K. Jagathish](https://builtin.com/authors/k-jagathish)

Published on Jul. 05, 2022

![](https://builtin.com/cdn-cgi/image/f=auto,quality=80,width=48,height=48/https://builtin.com/sites/www.builtin.com/files/styles/64_x_64/public/2022-06/Saravanan%2C%20K.%20Jagathish.png)

[K. Jagathish](https://builtin.com/authors/k-jagathish)

Software Developer at Tata Consultancy Services

[](https://builtin.com/authors/k-jagathish)

K. Jagathish is a front end developer who has worked in tech for more than five years. He’s currently a developer at Tata Consultancy Services.

![javascript-check-if-object-is-empty](https://builtin.com/cdn-cgi/image/f=auto,quality=80,width=752,height=435/https://builtin.com/sites/www.builtin.com/files/styles/byline_image/public/2022-06/javascript-check-if-object-is-empty.png) [![](/profiles/builtin/themes/bix/assets/expert-contrib-badge.svg)](https://builtin.com/expert-contributors)

In this article you will learn five different ways to check if an object is empty in JavaScript. Let’s jump right in.

## How to Check If an Object Is Empty in JavaScript

1. Use Object.keys
2. Loop Over Object Properties With for…in
3. Use JSON.stringify
4. Use jQuery
5. Use Underscore and Lodash Libraries

## 1\. Use Object.keys

`Object.keys` will return an [array](https://builtin.com/company/array), which contains the property names of the object. If the length of the array is `0`, then we know that the object is empty.

```javascript
function isEmpty(obj) {
    return **Object.keys(obj).length === 0**;
}
```

We can also check this using `Object.values` and `Object.entries`. This is typically the easiest way to determine if an object is empty.

More From Built In Experts[Fauna: An Introduction](https://builtin.com/software-engineering-perspectives/faunadb)

## 2\. Loop Over Object Properties With for…in

The `for…in` statement will loop through the enumerable property of the object.

```javascript

function isEmpty(obj) {
    for(var prop in obj) {
        if(obj.hasOwnProperty(prop))
            return false;
    }
    return true;
}
```

In the above code, we will loop through object properties and if an object has at least one property, then it will enter the loop and return false. If the object doesn’t have any properties then it will return true.

Tutorials for Software Developers on Built In[Create React App and TypeScript — A Quick How-To](https://builtin.com/software-engineering-perspectives/create-react-app-typescript)

## 3\. Use JSON.stringify

If we stringify the object and the result is simply an opening and closing bracket, we know the object is empty.

```javascript
function isEmptyObject(obj){
    return JSON.stringify(obj) === '{}'
}
```

## 4\. Use jQuery

```javascript
jQuery.isEmptyObject(obj); 
```

Related Reading[What Is the @ Symbol in Python and How Do I Use It?](https://builtin.com/software-engineering-perspectives/python-symbol)

## 5\. Use Underscore and Lodash Libraries

```javascript
_.isEmpty(obj);
```

These five quick and easy ways to check if an object is empty in [JavaScript](https://builtin.com/learn/tech-dictionary/javascript) are all you need to get going.