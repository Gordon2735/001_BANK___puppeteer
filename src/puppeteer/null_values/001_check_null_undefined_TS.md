#   Is there a way to check for both null and undefined?


[Is there a way to check for both \`null\` and \`undefined\`?](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined)


Since TypeScript is strongly-typed, simply using `if () {}` to check for `null` and `undefined` doesn't sound right.

Does TypeScript have any dedicated function or syntax sugar for this?


-   25
    `Since TypeScript is strongly-typed` I couldn't find this in it's docs and I have doubts about it...
    – [pawciobiel](https://stackoverflow.com/users/2829223/pawciobiel '157 reputation')
    [Aug 31, 2015 at 14:01](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment52501240_28975896)
-   4
    Recommend to read up on the latest non-nullable types , this is Typescript 2 , but already in beta as of today. \[Non-nullable types #7140\] ([github.com/Microsoft/TypeScript/pull/7140](https://github.com/Microsoft/TypeScript/pull/7140))
    – [RyBolt](https://stackoverflow.com/users/192814/rybolt '1,764 reputation')
    [Aug 5, 2016 at 13:10](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment64950315_28975896)
-   3
    TypeScript has no dedicated functions to do anything. It's a typing system and a transpiler, not a library.
    – user663031
    [Aug 9, 2017 at 8:18](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment78129288_28975896)
-   As you say it is bad to just check `if () {}` since that will also be true for `0`.
    – [Tom el Safadi](https://stackoverflow.com/users/5203853/tom-el-safadi '6,486 reputation')
    [Aug 21, 2020 at 9:18](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment112322004_28975896)

[Add a comment](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid answering questions in comments.') | [](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

Report this ad

## 28 Answers 28

Sorted by: [Reset to default](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined?answertab=scoredesc#tab-top)

Highest score (default) Trending (recent votes count more) Date modified (newest first) Date created (oldest first)

This answer is useful

670

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/28984306/timeline)

Show activity on this post.

Using a juggling-check, you can test both `null` and `undefined` in one hit:

```javascript
if (x == null) {
```

If you use a strict-check, it will only be true for values set to `null` and won't evaluate as true for undefined variables:

```javascript
if (x === null) {
```

You can try this with various values using this example:

```javascript
var a: number;
var b: number = null;

function check(x, name) {
	if (x == null) {
		console.log(name + ' == null');
	}

	if (x === null) {
		console.log(name + ' === null');
	}

	if (typeof x === 'undefined') {
		console.log(name + ' is undefined');
	}
}

check(a, 'a');
check(b, 'b');
```

Output

> "a == null"
>
> "a is undefined"
>
> "b == null"
>
> "b === null"

[Share](https://stackoverflow.com/a/28984306/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/ 'The current license for this post: CC BY-SA 3.0')

[Edit](https://stackoverflow.com/posts/28984306/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited Jun 13, 2018 at 7:59](https://stackoverflow.com/posts/28984306/revisions 'show all edits to this post')

answered Mar 11, 2015 at 10:38

[

![Fenton's user avatar](https://i.stack.imgur.com/IYU63.png?s=64&g=1)

](https://stackoverflow.com/users/75525/fenton)

[Fenton](https://stackoverflow.com/users/75525/fenton)Fenton

247k7272 gold badges395395 silver badges406406 bronze badges

15

-   122
    What is "juggling-check"?
    – [kolobok](https://stackoverflow.com/users/751200/kolobok '4,030 reputation')
    [Aug 1, 2016 at 12:55](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment64776702_28984306)
-   37
    @akapelko it is where the type is juggled (i.e. "can we make this type a boolean"). So an empty string is treated as a boolean false, for example. A common bug when juggling is: `"false" == false` a non-empty string like "false" evaluates to `true`.
    – [Fenton](https://stackoverflow.com/users/75525/fenton '246,543 reputation')
    [Aug 1, 2016 at 13:34](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment64778298_28984306)
-   28
    This is due to JS's 'type coercion'.
    – [Astravagrant](https://stackoverflow.com/users/275655/astravagrant '755 reputation')
    [Jan 16, 2017 at 13:19](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment70551806_28984306)
-   3
    @JonGunter that would be true of truthy/falsey `if(x)` style checks, but not `if(x == null)`, which only catches `null` and `undefined`. Check it using `var c: number = 0; check(c, 'b');` it is not "nully", `null`, or `undefined`.
    – [Fenton](https://stackoverflow.com/users/75525/fenton '246,543 reputation')
    [Aug 9, 2017 at 18:47](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment78156406_28984306)
-   2
    @developer - not quite, as `if (!x)` would treat (for example) the number `0` and the string `''` as null, whereas `if (x == null)` would not.
    – [Fenton](https://stackoverflow.com/users/75525/fenton '246,543 reputation')
    [Nov 4, 2017 at 9:11](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment81168482_28984306)

[](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [Show **10** more comments](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

469

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/44017547/timeline)

Show activity on this post.

```javascript
if (value) {
}
```

will evaluate to `true` if `value` is not:

-   `null`
-   `undefined`
-   `NaN`
-   empty string `''`
-   `0`
-   `false`

typescript includes javascript rules.

[Share](https://stackoverflow.com/a/44017547/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/ 'The current license for this post: CC BY-SA 3.0')

[Edit](https://stackoverflow.com/posts/44017547/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited Apr 16, 2018 at 15:09](https://stackoverflow.com/posts/44017547/revisions 'show all edits to this post')

[

![kingdaro's user avatar](https://i.stack.imgur.com/2UwB9.png?s=64&g=1)

](https://stackoverflow.com/users/1332403/kingdaro)

[kingdaro](https://stackoverflow.com/users/1332403/kingdaro)

11.8k33 gold badges3636 silver badges3838 bronze badges

answered May 17, 2017 at 6:50

[

![Ramazan Sağır's user avatar](https://i.stack.imgur.com/bNpUC.jpg?s=64&g=1)

](https://stackoverflow.com/users/1259233/ramazan-sa%c4%9f%c4%b1r)

[Ramazan Sağır](https://stackoverflow.com/users/1259233/ramazan-sa%c4%9f%c4%b1r)Ramazan Sağır

5,05511 gold badge1515 silver badges1717 bronze badges

11

-   53
    What if value is of boolean type?
    – [counterflow](https://stackoverflow.com/users/269998/counterflow '162 reputation')
    [Oct 6, 2017 at 22:56](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment80181917_44017547)
-   3
    can you combine two variables eg. if(value1 && value2) to check if both of them are undefined ?
    – [ARK](https://stackoverflow.com/users/2809294/ark '3,934 reputation')
    [Nov 17, 2017 at 16:52](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment81663631_44017547)
-   14
    @RamazanSağır yeah thanks I know that, but the fact is 0 value is something valid that I can have, the only check I want to do is that the variable is neither null or undefined. I have read that I can do it by using val != null (the != instead of !== also checks undefined value)
    – [Alex](https://stackoverflow.com/users/3241889/alex '4,649 reputation')
    [Feb 27, 2018 at 10:31](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment85017452_44017547)
-   9
    This solution will not work if the tslint rule - "strict-boolean-expressions" is enabled.
    – [ip_x](https://stackoverflow.com/users/1705343/ip-x '172 reputation')
    [Sep 24, 2018 at 11:43](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment91898133_44017547)
-   1
    It will evaluate false if value us falsy, as simple as this.
    – [Ayfri](https://stackoverflow.com/users/12184583/ayfri '630 reputation')
    [Apr 18, 2020 at 4:11](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment108415396_44017547)

[](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [Show **6** more comments](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

184

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/59029956/timeline)

Show activity on this post.

In **TypeScript 3.7** we have now **Optional chaining** and **Nullish Coalescing** to check **null** and **undefined** in the same time, example:

```javascript
let x = foo?.bar.baz();
```

this code will check if foo is defined otherwise it will return undefined

**old way** :

```javascript
if (foo != null && foo != undefined) {
	x = foo.bar.baz();
}
```

this:

```javascript
let x = (foo === null || foo === undefined) ? undefined : foo.bar();

if (foo && foo.bar && foo.bar.baz) { // ... }
```

With optional chaining will be:

```javascript
let x = foo?.bar();

if (foo?.bar?.baz) { // ... }
```

another new feature is **Nullish Coalescing**, example:

```javascript
let x = foo ?? bar(); // return foo if it's not null or undefined otherwise calculate bar
```

old way:

```javascript
let x = foo !== null && foo !== undefined ? foo : bar();
```

**BONUS** [![enter image description here](https://i.stack.imgur.com/OPBH5.png)](https://i.stack.imgur.com/OPBH5.png)

[Share](https://stackoverflow.com/a/59029956/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/59029956/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited Oct 5, 2020 at 8:36](https://stackoverflow.com/posts/59029956/revisions 'show all edits to this post')

answered Nov 25, 2019 at 10:43

[

![Fateh Mohamed's user avatar](https://i.stack.imgur.com/JkroG.jpg?s=64&g=1)

](https://stackoverflow.com/users/4399281/fateh-mohamed)

[Fateh Mohamed](https://stackoverflow.com/users/4399281/fateh-mohamed)Fateh Mohamed

20.9k55 gold badges4444 silver badges5555 bronze badges

7

-   21
    This should be the accepted answer now. Typescript 3.7 also supports "Nullish Coalescing". var foo = possibleUndefinedOrNull ?? fallbackValueIfFirstValueIsUndefinedOrNull; Here is the documentation: [typescriptlang.org/docs/handbook/release-notes/…](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-7.html)
    – [tkd_aj](https://stackoverflow.com/users/1414170/tkd-aj '1,013 reputation')
    [Nov 25, 2019 at 22:12](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment104324168_59029956)
-   Optional chaining and Nullish Coalescing are great but in case of a single `if` stmt like `if (context != null) word.ctx = context;` one still has to resort to the old juggling-check as described in the upvoted comment [stackoverflow.com/a/28984306/407986](https://stackoverflow.com/a/28984306/407986)
    – [Dmitry](https://stackoverflow.com/users/407986/dmitry '1,514 reputation')
    [Oct 28, 2020 at 5:12](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment114167488_59029956)
-   Yes, for almost scenarios, we could we `Optional chaining` , e.g. `if (foo?.bar?.baz)` [typescriptlang.org/docs/handbook/release-notes/…](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-7.html)
    – [Hien](https://stackoverflow.com/users/1737947/hien '2,090 reputation')
    [Jan 8, 2021 at 6:25](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment116026220_59029956)
-   Nullish Coalescing seems not supported in typescript 4.5.4. Is it deprecated?
    – [vinsinraw](https://stackoverflow.com/users/1195268/vinsinraw '2,057 reputation')
    [Jun 20, 2022 at 11:56](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment128392494_59029956)
-   1
    NOTE: `if (foo?.bar?.baz) { // ... }` is not a strict null|undefined check as it will be false if `baz` itself is fasley (zero, false, empty dict, empty list, etc)
    – [Nicholas Franceschina](https://stackoverflow.com/users/130221/nicholas-franceschina '6,117 reputation')
    [Nov 2, 2022 at 21:37](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment131167255_59029956)

[](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [Show **2** more comments](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

92

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/28976117/timeline)

Show activity on this post.

> Does TypeScript has dedicated function or syntax sugar for this

TypeScript fully understands the JavaScript version which is `something == null`.

TypeScript will correctly rule out both `null` and `undefined` with such checks.

# More

[https://basarat.gitbook.io/typescript/recap/null-undefined](https://basarat.gitbook.io/typescript/recap/null-undefined)

[Share](https://stackoverflow.com/a/28976117/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/28976117/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited Feb 25, 2020 at 3:05](https://stackoverflow.com/posts/28976117/revisions 'show all edits to this post')

answered Mar 10, 2015 at 23:42

[

![basarat's user avatar](https://www.gravatar.com/avatar/1400be56ff17549b926dd3260da4a494?s=64&d=identicon&r=PG)

](https://stackoverflow.com/users/390330/basarat)

[basarat](https://stackoverflow.com/users/390330/basarat)basarat

270k5959 gold badges467467 silver badges517517 bronze badges

2

-   4
    I like doing two equals `myVar == null`. Just another option.
    – [David Sherret](https://stackoverflow.com/users/188246/david-sherret '104,363 reputation')
    [Mar 11, 2015 at 2:09](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment46205756_28976117)
-   45
    `== null` is the correct way to test for null & undefined. `!!something` is a useless coercion in a conditional in JS (just use `something`). `!!something` will also coerce 0 and '' to false, which is not what you want to do if you are looking for null/undefined.
    – [C Snover](https://stackoverflow.com/users/252087/c-snover '18,428 reputation')
    [Mar 11, 2015 at 3:04](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment46206541_28976117)

[Add a comment](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

46

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/40175472/timeline)

Show activity on this post.

I did different tests on the typescript playground:

[http://www.typescriptlang.org/play/](http://www.typescriptlang.org/play/)

```javascript
let a;
let b = null;
let c = '';
var output = '';

if (a == null) output += 'a is null or undefined\n';
if (b == null) output += 'b is null or undefined\n';
if (c == null) output += 'c is null or undefined\n';
if (a != null) output += 'a is defined\n';
if (b != null) output += 'b is defined\n';
if (c != null) output += 'c is defined\n';
if (a) output += 'a is defined (2nd method)\n';
if (b) output += 'b is defined (2nd method)\n';
if (c) output += 'c is defined (2nd method)\n';

console.log(output);
```

gives:

```javascript
a is null or undefined
b is null or undefined
c is defined
```

so:

-   checking if (a == null) is right to know if a is null or undefined
-   checking if (a != null) is right to know if a is defined
-   checking if (a) is wrong to know if a is defined

[Share](https://stackoverflow.com/a/40175472/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/ 'The current license for this post: CC BY-SA 3.0')

[Edit](https://stackoverflow.com/posts/40175472/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited Jan 11, 2017 at 0:57](https://stackoverflow.com/posts/40175472/revisions 'show all edits to this post')

answered Oct 21, 2016 at 11:25

[

![Juangui Jordán's user avatar](https://www.gravatar.com/avatar/329fd7d295cb5a2289888520ae2871b5?s=64&d=identicon&r=PG)

](https://stackoverflow.com/users/627161/juangui-jord%c3%a1n)

[Juangui Jordán](https://stackoverflow.com/users/627161/juangui-jord%c3%a1n)Juangui Jordán

6,37722 gold badges3939 silver badges3131 bronze badges

3

-   2
    Why would you use the TypeScript playground for this? Nothing here has anything to do with TypeScript.
    – user663031
    [Aug 10, 2017 at 4:37](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment78168205_40175472)
-   13
    Because the question was related to Typescript, I was trying to test different proposed solutions against the Typescript transpiler.
    – [Juangui Jordán](https://stackoverflow.com/users/627161/juangui-jord%c3%a1n '6,377 reputation')
    [Aug 11, 2017 at 7:51](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment78218634_40175472)
-   8
    The TS transpiler would not transform any of this code at all.
    – user663031
    [Aug 11, 2017 at 8:32](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment78220066_40175472)

[Add a comment](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

44

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/70040699/timeline)

Show activity on this post.

### SIMPLE ANSWER

Although Typescript is a strongly typed language, it has the same problems with pointers and variables initialization inherited from Javascript.  
Javascript doesn't check whether a variable exists in the context, the so common `undefined` status.

to evaluate if value **ISN'T** `null`,`undefined`,`0`,`false`,`""`, or `NaN`:

```javascript
if ( value )
or
if ( !!value )
```

for negative conditional, check if the value is `null`,`undefined`,`0`,`false`,`""`,or `NaN`:

```javascript
if ( !value )
```

to test if is `null` or `undefined`:

```javascript
if ( value == null )
```

to test only `null`:

```javascript
if ( value === null )
```

to test only `undefined`:

```javascript
if ( value === undefined )
```

---

#### MORE DETAILED ANSWER

**1-** It will evaluate to **true** if value **is not**: `null`, `undefined`, `NaN`, `empty string ''`, `0`, `false`  
If the value is `null`,`undefined`,`NaN`,`empty string`,`0`, or `false`, will go to the **else** condition.

```javascript
if (value) {
	console.log(
		'value is something different from 0, "", false, NaN, null, undefined'
	);
} else {
	console.log('value is 0, "", false, NaN, null or undefined');
}
if (!!value) {
	console.log(
		'value is something different from 0, "", false, NaN, null, undefined'
	);
} else {
	console.log('value is 0, "", false, NaN, null or undefined');
}
```

**2-** If you want a negative condition, then you'll need to use:

```javascript
if (!value) {
	console.log('value is 0, "", false, NaN, null or undefined');
} else {
	console.log(
		'value is something different from 0, "", false, NaN, null, undefined'
	);
}
```

**3-** It will evaluate if value is `null` or `undefined`

```javascript
if (value == null) {
	console.log('is null or undefined');
} else {
	console.log('it isnt null neither undefined');
}
```

**4-** Using a test with boolean values doesn't work.  
It will **NOT** evaluate to **true** neither to **false** if value is `null`, `undefined`, `0`, `empty string`, `NaN`  
Both conditions will always go to the **else** condition.  
With the exception if value is a boolean variable.

```javascript
if (value == true) {
} else {
}
if (value == false) {
} else {
}
```

[Share](https://stackoverflow.com/a/70040699/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/70040699/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited Feb 22, 2023 at 16:10](https://stackoverflow.com/posts/70040699/revisions 'show all edits to this post')

answered Nov 19, 2021 at 20:40

[

![danilo's user avatar](https://i.stack.imgur.com/ORFjz.jpg?s=64&g=1)

](https://stackoverflow.com/users/935330/danilo)

[danilo](https://stackoverflow.com/users/935330/danilo)danilo

8,66877 gold badges4646 silver badges4848 bronze badges

1

-   Do you mean less concise?
    – [SacredGeometry](https://stackoverflow.com/users/385747/sacredgeometry '911 reputation')
    [Apr 4, 2022 at 10:57](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment126774759_70040699)

[Add a comment](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

42

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/49792111/timeline)

Show activity on this post.

You may want to try

```javascript
if(!!someValue)
```

with `!!`.

**Explanation**

The first `!` will turn your expression into a `boolean` value.

Then `!someValue` is `true` if `someValue` is _falsy_ and `false` if `someValue` is _truthy_. This might be confusing.

By adding another `!`, the expression is now `true` if `someValue` is _truthy_ and `false` if `someValue` is _falsy_, which is much easier to manage.

**Discussion**

Now, why do I bother myself with `if (!!someValue)` when something like `if (someValue)` would have give me the same result?

Because `!!someValue` is precisely a boolean expression, whereas `someValue` could be absolutely anything. This kind of expression will now alow to write functions (and God we need those) like:

```javascript
isSomeValueDefined(): boolean {
  return !!someValue
}
```

instead of:

```javascript
isSomeValueDefined(): boolean {
  if(someValue) {
    return true
  }
  return false
}
```

I hope it helps.

[Share](https://stackoverflow.com/a/49792111/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/ 'The current license for this post: CC BY-SA 3.0')

[Edit](https://stackoverflow.com/posts/49792111/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered Apr 12, 2018 at 8:52

[

![avi.elkharrat's user avatar](https://i.stack.imgur.com/7npUs.jpg?s=64&g=1)

](https://stackoverflow.com/users/4163254/avi-elkharrat)

[avi.elkharrat](https://stackoverflow.com/users/4163254/avi-elkharrat)avi.elkharrat

6,48666 gold badges4343 silver badges4949 bronze badges

5

-   so, if someValue is 'false'(with string type), then !!someValue is false(boolean type)?
    – [paul cheung](https://stackoverflow.com/users/2364553/paul-cheung '748 reputation')
    [Feb 12, 2019 at 3:47](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment96076563_49792111)
-   I guess you may say so.This technic is precisely used to avoid having this kind of confusion. I hope you like it!
    – [avi.elkharrat](https://stackoverflow.com/users/4163254/avi-elkharrat '6,486 reputation')
    [Feb 12, 2019 at 8:41](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment96083071_49792111)
-   but what confused me is !!'false' equals true. Just because of this case, i can not use this technic.
    – [paul cheung](https://stackoverflow.com/users/2364553/paul-cheung '748 reputation')
    [Feb 12, 2019 at 9:07](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment96083938_49792111)
-   `!!'false'` is in deed `true` because `'false'` is a valid string
    – [avi.elkharrat](https://stackoverflow.com/users/4163254/avi-elkharrat '6,486 reputation')
    [Feb 12, 2019 at 9:43](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment96085333_49792111)
-   so this technic can not cover this case, or is there a workaround solution?
    – [paul cheung](https://stackoverflow.com/users/2364553/paul-cheung '748 reputation')
    [Feb 12, 2019 at 9:56](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment96085810_49792111)

[Add a comment](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

39

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/52097700/timeline)

Show activity on this post.

For `Typescript 2.x.x` you should do it in a following way(using [type guard](https://www.typescriptlang.org/docs/handbook/advanced-types.html#user-defined-type-guards)):

**tl;dr**

```javascript
function isDefined<T>(value: T | undefined | null): value is T {
  return <T>value !== undefined && <T>value !== null;
}
```

---

**Why?**

In this way `isDefined()` will respect variable's type and the following code would know take this check in account.

**Example 1** - basic check:

```javascript
function getFoo(foo: string): void {
	//
}

function getBar(bar: string | undefined) {
	getFoo(bar); //ERROR: "bar" can be undefined
	if (isDefined(bar)) {
		getFoo(bar); // Ok now, typescript knows that "bar' is defined
	}
}
```

**Example 2** - types respect:

```javascript
function getFoo(foo: string): void {
	//
}

function getBar(bar: number | undefined) {
	getFoo(bar); // ERROR: "number | undefined" is not assignable to "string"
	if (isDefined(bar)) {
		getFoo(bar); // ERROR: "number" is not assignable to "string", but it's ok - we know it's number
	}
}
```

[Share](https://stackoverflow.com/a/52097700/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/52097700/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited Sep 10, 2019 at 7:47](https://stackoverflow.com/posts/52097700/revisions 'show all edits to this post')

[

![Maxim Pyshko's user avatar](https://lh6.googleusercontent.com/-66uSZhofjx4/AAAAAAAAAAI/AAAAAAAAAAA/ACHi3rdu9MEVta-7jEd8J4L0KNfu11ycSg/photo.jpg?sz=64)

](https://stackoverflow.com/users/11747513/maxim-pyshko)

[Maxim Pyshko](https://stackoverflow.com/users/11747513/maxim-pyshko)

56144 silver badges1414 bronze badges

answered Aug 30, 2018 at 12:57

[

![S Panfilov's user avatar](https://i.stack.imgur.com/Dm96U.jpg?s=64&g=1)

](https://stackoverflow.com/users/930170/s-panfilov)

[S Panfilov](https://stackoverflow.com/users/930170/s-panfilov)S Panfilov

17.2k1818 gold badges7777 silver badges100100 bronze badges

4

-   2
    I wish they added this as an util function.
    – [Totati](https://stackoverflow.com/users/4797961/totati '1,517 reputation')
    [Nov 12, 2020 at 21:48](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment114591498_52097700)
-   3
    Note that the check for nullish should be defined like this: `function isNullish<T>(value: T | undefined | null): value is undefined | null { return <T>value === undefined || <T>value === null; }`
    – [Kfir Dadosh](https://stackoverflow.com/users/1140697/kfir-dadosh '1,419 reputation')
    [Sep 23, 2021 at 13:42](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment122487289_52097700)
-   1
    @KfirDadosh is right, isNullish should be used instead, (or call it `isNotDefined` if you like). The problem with the original code is if the type parameter T is `null` or `undefined`, then the original code will return the opposite of the correct answer.
    – [Steven Obua](https://stackoverflow.com/users/553496/steven-obua '974 reputation')
    [Dec 29, 2021 at 8:10](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment124651973_52097700)
-   2
    This should be the accepted answer in 2022
    – [blwinters](https://stackoverflow.com/users/4139760/blwinters '2,031 reputation')
    [Apr 6, 2022 at 21:31](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment126839230_52097700)

[Add a comment](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

31

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/51259620/timeline)

Show activity on this post.

I think this answer needs an update, check the edit history for the old answer.

Basically, you have three deferent cases null, undefined, and undeclared, see the snippet below.

```javascript
// bad-file.ts
console.log(message);
```

You'll get an error says that variable `message` is undefined (aka undeclared), of course, the Typescript compiler shouldn't let you do that but REALLY nothing can prevent you.

```javascript
// evil-file.ts
// @ts-gnore
console.log(message);
```

The compiler will be happy to just compile the code above. So, if you're sure that all variables are declared you can simply do that

```javascript
if (message != null) {
	// do something with the message
}
```

the code above will check for `null` and `undefined`, BUT in case the `message` variable may be undeclared (for safety), you may consider the following code

```javascript
if (typeof message !== 'undefined' && message !== null) {
	// message variable is more than safe to be used.
}
```

Note: the order here `typeof(message) !== 'undefined' && message !== null` is very important you have to check for the `undefined` state first atherwise it will be just the same as `message != null`, thanks @Jaider.

[Share](https://stackoverflow.com/a/51259620/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/51259620/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited Jul 10, 2019 at 18:10](https://stackoverflow.com/posts/51259620/revisions 'show all edits to this post')

answered Jul 10, 2018 at 7:39

[

![Ahmed Kamal's user avatar](https://i.stack.imgur.com/NMhnN.jpg?s=64&g=1)

](https://stackoverflow.com/users/8195572/ahmed-kamal)

[Ahmed Kamal](https://stackoverflow.com/users/8195572/ahmed-kamal)Ahmed Kamal

2,88033 gold badges2222 silver badges3838 bronze badges

8

-   4
    M. Kamal if something = 0, your verification with !something will give you problems.
    – [justcode](https://stackoverflow.com/users/1322957/justcode '1,562 reputation')
    [Nov 21, 2018 at 10:35](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment93695096_51259620)
-   1
    @arturios can you please give me an example!!
    – [Ahmed Kamal](https://stackoverflow.com/users/8195572/ahmed-kamal '2,880 reputation')
    [Nov 21, 2018 at 13:24](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment93700584_51259620)
-   2
    @arturios But 0 is already a falsy value in JavaScript !! so what is the point here?
    – [Ahmed Kamal](https://stackoverflow.com/users/8195572/ahmed-kamal '2,880 reputation')
    [Nov 21, 2018 at 17:01](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment93708603_51259620)
-   1
    @Al-un nope, see it in action [here](<http://www.typescriptlang.org/play/#src=%2F%2F%20it's%20undefined.%0D%0Aconst%20something%20%3D%20undefined%0D%0A%0D%0Aif%20(something%20!%3D%3D%20null%20%26%26%20typeof%20something%20!%3D%3D%20'undefined')%20%7B%0D%0A%20%20%2F%2F%20your%20logic%20here...%0D%0A%7D%20else%20%7B%0D%0A%20%20%20%20console.log('NOPE%2C%20no%20errors!')%0D%0A%7D>)
    – [Ahmed Kamal](https://stackoverflow.com/users/8195572/ahmed-kamal '2,880 reputation')
    [Jan 17, 2019 at 23:45](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment95316310_51259620)
-   1
    the updated version is wrong. The first thing to check should be undefined... like: `if(typeof something !== 'undefined' && something !== null){...}`
    – [Jaider](https://stackoverflow.com/users/480700/jaider '14,608 reputation')
    [Jul 10, 2019 at 17:17](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment100487590_51259620)

[](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [Show **3** more comments](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

15

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/41763539/timeline)

Show activity on this post.

```javascript
if (data) {
}
```

it's mean !data

-   null
-   undefined
-   false
-   ....

[Share](https://stackoverflow.com/a/41763539/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/ 'The current license for this post: CC BY-SA 3.0')

[Edit](https://stackoverflow.com/posts/41763539/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered Jan 20, 2017 at 12:18

[

![artemitSoft's user avatar](https://www.gravatar.com/avatar/471865c2a44e647cfffb32d4099c38fe?s=64&d=identicon&r=PG&f=y&so-version=2)

](https://stackoverflow.com/users/2958358/artemitsoft)

[artemitSoft](https://stackoverflow.com/users/2958358/artemitsoft)artemitSoft

30655 silver badges1818 bronze badges

4

-   4
    And if data is of boolean type?
    – [counterflow](https://stackoverflow.com/users/269998/counterflow '162 reputation')
    [Oct 6, 2017 at 22:57](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment80181925_41763539)
-   can you combine two variables eg. if(value1 && value2) to check if both of them are undefined ?
    – [ARK](https://stackoverflow.com/users/2809294/ark '3,934 reputation')
    [Nov 17, 2017 at 16:54](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment81663667_41763539)
-   @ianstigator A boolean can be evaluated as `true` or `false` only. If you have a boolean with a `null` assignation or an `undefined` value, in both cases the value will be evaluated as `false`.
    – [KBeDev](https://stackoverflow.com/users/7737346/kbedev '427 reputation')
    [May 19, 2020 at 20:22](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment109483557_41763539)
-   1
    This fails when data is a boolean value
    – [Dhanika](https://stackoverflow.com/users/10429146/dhanika '777 reputation')
    [Aug 19, 2022 at 10:11](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment129648847_41763539)

[Add a comment](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

10

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/60528481/timeline)

Show activity on this post.

**UPDATE (Sept 4, 2020)**

You can now use the `??` operator to validate `null` and `undefined` "values" and set a default value. For example:

```javascript
const foo = null;
const bar = foo ?? 'exampleValue';
console.log(bar); // This will print 'exampleValue' due to the value condition of the foo constant, in this case, a null value
```

---

As a verbose way, if you want to compare _null_ and _undefined_ values **ONLY**, use the following example code for reference:

```javascript
const incomingValue: string = undefined;
const somethingToCompare: string = incomingValue; // If the line above is not declared, TypeScript will return an excepion

if (somethingToCompare == (undefined || null)) {
	console.log(`Incoming value is: ${somethingToCompare}`);
}
```

If `incomingValue` is not declared, TypeScript should return an exception. If this is declared but not defined, the `console.log()` will return "Incoming value is: undefined". Note we are not using the strict equals operator.

The "correct" way (check the other answers for details), if the `incomingValue` is not a `boolean` type, just evaluate if its value is true, this will be evaluated according to the constant/variable type. A `true` string have to be defined explicitly as string using the `= ''` assignation. If not, it will be evaluated as `false`. Let's check this case using the same context:

```javascript
const incomingValue: string = undefined;
const somethingToCompare0: string = 'Trumpet';
const somethingToCompare1: string = incomingValue;

if (somethingToCompare0) {
	console.log(`somethingToCompare0 is: ${somethingToCompare0}`); // Will return "somethingToCompare0 is: Trumpet"
}

// Now, we will evaluate the second constant
if (somethingToCompare1) {
	console.log(`somethingToCompare1 is: ${somethingToCompare1}`); // Launched if incomingValue is defined
} else {
	console.log(`somethingToCompare1 is: ${somethingToCompare1}`); // Launched if incomingValue is undefined. Will return "somethingToCompare1 is: undefined"
}
```

[Share](https://stackoverflow.com/a/60528481/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/60528481/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited Sep 4, 2020 at 20:30](https://stackoverflow.com/posts/60528481/revisions 'show all edits to this post')

answered Mar 4, 2020 at 14:36

[

![KBeDev's user avatar](https://lh4.googleusercontent.com/-v7RR3XIYT20/AAAAAAAAAAI/AAAAAAAAFhI/POgYjCPTm9g/photo.jpg?sz=64)

](https://stackoverflow.com/users/7737346/kbedev)

[KBeDev](https://stackoverflow.com/users/7737346/kbedev)KBeDev

42777 silver badges1111 bronze badges

3

-   3
    somethingToCompare == (undefined || null). (undefined || null) resolves to null, so it's a loose comparison between somethingToCompare and null
    – [carlosvini](https://stackoverflow.com/users/2321037/carlosvini '1,770 reputation')
    [Apr 23, 2020 at 19:38](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment108610551_60528481)
-   @carlosvini Sure, the point of the comparison is to be verbose and provide a code for reference. That's the reason of the non-strict equals comparison. The purpose of the answer is to be clear and explicative. I'll edit the text to avoid confusion
    – [KBeDev](https://stackoverflow.com/users/7737346/kbedev '427 reputation')
    [Apr 23, 2020 at 20:02](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment108611170_60528481)
-   1
    I don't understand what you mean. The code is not verbose or explicit, it is confusing at best and plain wrong at worst. The code `a == (b || c)` is the **not** the same as `a == b || a == c`, instead it will evaluate `b || c` (in this case to `c` since `b` is falsy in your example) and then compare that against `a`.
    – [CherryDT](https://stackoverflow.com/users/1871033/cherrydt '27,958 reputation')
    [Nov 7, 2020 at 20:33](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment114453437_60528481)

[Add a comment](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

8

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/47295117/timeline)

Show activity on this post.

If you want to pass `tslint` without setting `strict-boolean-expressions` to `allow-null-union` or `allow-undefined-union`, you need to use `isNullOrUndefined` from `node`'s `util` module or roll your own:

```javascript
// tslint:disable:no-null-keyword
export const isNullOrUndefined =
  <T>(obj: T | null | undefined): obj is null | undefined => {
    return typeof obj === "undefined" || obj === null;
  };
// tslint:enable:no-null-keyword
```

Not exactly syntactic sugar but useful when your tslint rules are strict.

[Share](https://stackoverflow.com/a/47295117/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/ 'The current license for this post: CC BY-SA 3.0')

[Edit](https://stackoverflow.com/posts/47295117/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered Nov 14, 2017 at 21:01

[

![Graeme Wicksted's user avatar](https://www.gravatar.com/avatar/1ab1f8d1bd45b30c2e1cbe4ed74cd83c?s=64&d=identicon&r=PG)

](https://stackoverflow.com/users/675561/graeme-wicksted)

[Graeme Wicksted](https://stackoverflow.com/users/675561/graeme-wicksted)Graeme Wicksted

1,79511 gold badge1919 silver badges2121 bronze badges

[Add a comment](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

7

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/44128978/timeline)

Show activity on this post.

If you are using TypeScript, it is a better approach to let the compiler check for nulls and undefineds (or the possibility thereof), rather than checking for them at run-time. (If you do want to check at run-time, then as many answers indicate, just use `value == null`).

Use the compile option [`strictNullChecks`](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-0.html) to tell the compiler to choke on possible null or undefined values. If you set this option, and then there is a situation where you **do** want to allow null and undefined, you can define the type as `Type | null | undefined`.

[Share](https://stackoverflow.com/a/44128978/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/ 'The current license for this post: CC BY-SA 3.0')

[Edit](https://stackoverflow.com/posts/44128978/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered May 23, 2017 at 7:56

user663031user663031

[Add a comment](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

3

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/64131912/timeline)

Show activity on this post.

The simplest way is to use:

`import { isNullOrUndefined } from 'util';`

and than:

`if (!isNullOrUndefined(foo))`

[Share](https://stackoverflow.com/a/64131912/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/64131912/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered Sep 30, 2020 at 6:19

[

![Ruthi's user avatar](https://www.gravatar.com/avatar/b13011595ec6657e45e5d32cef7ffe9c?s=64&d=identicon&r=PG)

](https://stackoverflow.com/users/1520221/ruthi)

[Ruthi](https://stackoverflow.com/users/1520221/ruthi)Ruthi

31211 gold badge44 silver badges1212 bronze badges

3

-   Works great here
    – [Sindri Þór](https://stackoverflow.com/users/2612536/sindri-%c3%9e%c3%b3r '2,907 reputation')
    [Apr 2, 2021 at 21:08](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment118300795_64131912)
-   7
    From the function docs: deprecated since v4.0.0 - use `value === null || value === undefined` instead.
    – [Aleksei](https://stackoverflow.com/users/6868862/aleksei '571 reputation')
    [Jun 4, 2021 at 11:03](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment119902754_64131912)
-   @Aleksei that's ironic
    – [refaelio](https://stackoverflow.com/users/929370/refaelio '408 reputation')
    [Jan 31, 2022 at 10:40](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment125381341_64131912)

[Add a comment](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

2

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/67630132/timeline)

Show activity on this post.

May be to late! but you can use `??` operator in **typescript**. see [https://mariusschulz.com/blog/nullish-coalescing-the-operator-in-typescript](https://mariusschulz.com/blog/nullish-coalescing-the-operator-in-typescript)

[Share](https://stackoverflow.com/a/67630132/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/67630132/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered May 21, 2021 at 2:30

[

![Ali Qamsari's user avatar](https://i.stack.imgur.com/mczsT.jpg?s=64&g=1)

](https://stackoverflow.com/users/8092383/ali-qamsari)

[Ali Qamsari](https://stackoverflow.com/users/8092383/ali-qamsari)Ali Qamsari

10322 silver badges1010 bronze badges

[Add a comment](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

2

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/67089554/timeline)

Show activity on this post.

We use a helper `hasValue` that both checks for nulls/undefined and ensures via TypeScript that unnecessary checks are not performed. (The latter is similar to how TS would complain about `if ("a" === undefined)`, since it is always false).

Using this consistently is always safe, unlike `!val` which matches empty strings, zero, etc. It also avoid the use of fuzzy `==` matching which is almost always a bad practice - no need to introduce an exception.

```javascript


type NullPart<T> = T & (null | undefined);

// Ensures unnecessary checks aren't performed - only a valid call if
// value could be nullable *and* could be non-nullable
type MustBeAmbiguouslyNullable<T> = NullPart<T> extends never
  ? never
  : NonNullable<T> extends never
  ? never
  : T;

export function hasValue<T>(
  value: MustBeAmbiguouslyNullable<T>,
): value is NonNullable<MustBeAmbiguouslyNullable<T>> {
  return (value as unknown) !== undefined && (value as unknown) !== null;
}

export function hasValueFn<T, A>(
  value: MustBeAmbiguouslyNullable<T>,
  thenFn: (value: NonNullable<T>) => A,
): A | undefined {
  // Undefined matches .? syntax result
  return hasValue(value) ? thenFn(value) : undefined;
}


```

[Share](https://stackoverflow.com/a/67089554/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/67089554/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited May 4, 2021 at 0:39](https://stackoverflow.com/posts/67089554/revisions 'show all edits to this post')

answered Apr 14, 2021 at 9:58

[

![Freewalker's user avatar](https://www.gravatar.com/avatar/c7564ed5b848eda69e4fea42ab2323b5?s=64&d=identicon&r=PG)

](https://stackoverflow.com/users/152711/freewalker)

[Freewalker](https://stackoverflow.com/users/152711/freewalker)Freewalker

6,84755 gold badges5353 silver badges7373 bronze badges

[Add a comment](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

2

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/76465824/timeline)

Show activity on this post.

It can be done like this:

```javascript
// value is the value which you want to check
[undefined, null].includes(value);
```

[Share](https://stackoverflow.com/a/76465824/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/76465824/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered Jun 13, 2023 at 14:10

[

![H S W's user avatar](https://i.stack.imgur.com/WAHCS.jpg?s=64&g=1)

](https://stackoverflow.com/users/8584904/h-s-w)

[H S W](https://stackoverflow.com/users/8584904/h-s-w)H S W

6,69944 gold badges2727 silver badges3737 bronze badges

[Add a comment](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

1

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/55596948/timeline)

Show activity on this post.

Late to join this thread but I find this JavaScript hack very handy in checking whether a value is undefined

```javascript
if (typeof something === 'undefined') {
	// Yes this is undefined
}
```

[Share](https://stackoverflow.com/a/55596948/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/55596948/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered Apr 9, 2019 at 16:03

[

![Shahid Manzoor Bhat's user avatar](https://i.stack.imgur.com/bMxaw.jpg?s=64&g=1)

](https://stackoverflow.com/users/2210256/shahid-manzoor-bhat)

[Shahid Manzoor Bhat](https://stackoverflow.com/users/2210256/shahid-manzoor-bhat)Shahid Manzoor Bhat

1,31711 gold badge1414 silver badges3232 bronze badges

[Add a comment](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

1

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/71493265/timeline)

Show activity on this post.

You can do this easily with a ternary operator and the new nullish coalesce operator.

First: check to see if it is true using the ternary. If so return false so the if statement does not run.

Second: because you now know the value is falsey, you can use the nullish coalesce operator to return true if it is nullish. Since it will return itself for any other value, if it is not nullish it will fail the if statement correctly.

```javascript
let x = true;
console.log('starting tests');

if (x ? false : x ?? true) {
	console.log(x, 'is nullish');
}

x = false;
if (x ? false : x ?? true) {
	console.log(x, 'is nullish');
}

x = 0;
if (x ? false : x ?? true) {
	console.log(x, 'is nullish');
}

x = 1;
if (x ? false : x ?? true) {
	console.log(x, 'is nullish');
}

x = '';
if (x ? false : x ?? true) {
	console.log(x, 'is nullish');
}

x = 'hello world';
if (x ? false : x ?? true) {
	console.log(x, 'is nullish');
}

x = null;
if (x ? false : x ?? true) {
	console.log(x, 'is nullish');
}

x = undefined;
if (x ? false : x ?? true) {
	console.log(x, 'is nullish');
}
```

Run code snippetHide results

Expand snippet

[Share](https://stackoverflow.com/a/71493265/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/71493265/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered Mar 16, 2022 at 7:39

[

![Daniel's user avatar](https://www.gravatar.com/avatar/1ddb8cec3eb40b039317865593724a41?s=64&d=identicon&r=PG&f=y&so-version=2)

](https://stackoverflow.com/users/13809150/daniel)

[Daniel](https://stackoverflow.com/users/13809150/daniel)Daniel

1,41911 gold badge55 silver badges1717 bronze badges

[Add a comment](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

0

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/53003862/timeline)

Show activity on this post.

A faster and shorter notation for `null` checks can be:

```javascript
value == null ? 'UNDEFINED' : value;
```

This line is equivalent to:

```javascript
if (value == null) {
	console.log('UNDEFINED');
} else {
	console.log(value);
}
```

Especially when you have a lot of `null` check it is a nice short notation.

[Share](https://stackoverflow.com/a/53003862/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/53003862/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered Oct 26, 2018 at 7:46

user11367277user11367277

[Add a comment](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

0

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/51652757/timeline)

Show activity on this post.

Since TypeScript is a typed superset of ES6 JavaScript. And lodash are a library of javascript.

Using lodash to checks if value is null or undefined can be done using `_.isNil()`.

```javascript
_.isNil(value);
```

### Arguments

**value** (\*): The value to check.

### Returns

**(boolean)**: Returns true if value is nullish, else false.

### Example

```javascript
_.isNil(null);
// => true

_.isNil(void 0);
// => true

_.isNil(NaN);
// => false
```

### Link

[Lodash Docs](https://lodash.com/docs/4.17.10#isNil)

[Share](https://stackoverflow.com/a/51652757/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/51652757/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered Aug 2, 2018 at 11:42

[

![7e2e63de's user avatar](https://www.gravatar.com/avatar/a9123dea9feab27c852386896bd2c5c5?s=64&d=identicon&r=PG&f=y&so-version=2)

](https://stackoverflow.com/users/4399415/7e2e63de)

[7e2e63de](https://stackoverflow.com/users/4399415/7e2e63de)7e2e63de

3733 bronze badges

1

-   1
    Why this method are -2 ? Lodash is not good with type script ?
    – [Thomas Poignant](https://stackoverflow.com/users/5815046/thomas-poignant '127 reputation')
    [Jun 13, 2019 at 14:28](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment99743482_51652757)

[Add a comment](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

0

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/44128273/timeline)

Show activity on this post.

you can use

```javascript
if(x === undefined)
```

[Share](https://stackoverflow.com/a/44128273/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/ 'The current license for this post: CC BY-SA 3.0')

[Edit](https://stackoverflow.com/posts/44128273/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited May 23, 2017 at 15:53](https://stackoverflow.com/posts/44128273/revisions 'show all edits to this post')

[

![Julian's user avatar](https://i.stack.imgur.com/AQoqr.jpg?s=64&g=1)

](https://stackoverflow.com/users/201303/julian)

[Julian](https://stackoverflow.com/users/201303/julian)

35.4k2323 gold badges126126 silver badges183183 bronze badges

answered May 23, 2017 at 7:23

[

![akshay reddy's user avatar](https://lh5.googleusercontent.com/-iPr2l4EMzhA/AAAAAAAAAAI/AAAAAAAAAaw/BdLY-Dwo8uI/photo.jpg?sz=64)

](https://stackoverflow.com/users/5272524/akshay-reddy)

[akshay reddy](https://stackoverflow.com/users/5272524/akshay-reddy)akshay reddy

4122 bronze badges

[Add a comment](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

0

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/54797861/timeline)

Show activity on this post.

I had this issue and some of the answer work just fine for `JS` but not for `TS` here is the reason.

```javascript
//JS
let couldBeNullOrUndefined;
if (couldBeNullOrUndefined == null) {
	console.log('null OR undefined', couldBeNullOrUndefined);
} else {
	console.log('Has some value', couldBeNullOrUndefined);
}
```

That is all good as JS has no Types

```javascript
//TS
let couldBeNullOrUndefined?: string | null; // THIS NEEDS TO BE TYPED AS undefined || null || Type(string)

if(couldBeNullOrUndefined === null) { // TS should always use strict-check
  console.log('null OR undefined', couldBeNullOrUndefined);
} else {
  console.log('Has some value', couldBeNullOrUndefined);
}
```

In TS if the variable wasn't defined with `null` when you try to check for that `null` the `tslint` | compiler will complain.

```javascript
//tslint.json
...
"triple-equals":[true],
...
```

```javascript
 let couldBeNullOrUndefined?: string; // to fix it add | null

 Types of property 'couldBeNullOrUndefined' are incompatible.
      Type 'string | null' is not assignable to type 'string | undefined'.
        Type 'null' is not assignable to type 'string | undefined'.
```

[Share](https://stackoverflow.com/a/54797861/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/54797861/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered Feb 21, 2019 at 1:29

[

![T04435's user avatar](https://i.stack.imgur.com/0bj79.jpg?s=64&g=1)

](https://stackoverflow.com/users/4374291/t04435)

[T04435](https://stackoverflow.com/users/4374291/t04435)T04435

13.2k55 gold badges5757 silver badges5858 bronze badges

[Add a comment](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

0

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/56695419/timeline)

Show activity on this post.

Usually I do the juggling-check as Fenton already [discussed](https://stackoverflow.com/a/28984306/4812980). To make it more readable, you can use [isNil](https://ramdajs.com/docs/#isNil) from ramda.

```javascript
import * as isNil from 'ramda/src/isNil';

totalAmount = isNil(totalAmount) ? 0 : totalAmount;
```

[Share](https://stackoverflow.com/a/56695419/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/56695419/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered Jun 21, 2019 at 0:23

[

![Neo's user avatar](https://www.gravatar.com/avatar/cd66ef3c74c35997e5747152579bd95c?s=64&d=identicon&r=PG)

](https://stackoverflow.com/users/4812980/neo)

[Neo](https://stackoverflow.com/users/4812980/neo)Neo

25322 silver badges33 bronze badges

[Add a comment](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

0

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/46665302/timeline)

Show activity on this post.

All,

The answer with the most votes, does not really work if you are working with an object. In that case, if a property is not present, the check will not work. And that was the issue in our case: see this sample:

```javascript
var x = { name: 'Homer', LastName: 'Simpson' };

var y = { name: 'Marge' };

var z = { name: 'Bart', LastName: undefined };

var a = { name: 'Lisa', LastName: '' };

var hasLastNameX = x.LastName != null;
var hasLastNameY = y.LastName != null;
var hasLastNameZ = z.LastName != null;
var hasLastNameA = a.LastName != null;

alert(
	hasLastNameX + ' ' + hasLastNameY + ' ' + hasLastNameZ + ' ' + hasLastNameA
);

var hasLastNameXX = x.LastName !== null;
var hasLastNameYY = y.LastName !== null;
var hasLastNameZZ = z.LastName !== null;
var hasLastNameAA = a.LastName !== null;

alert(
	hasLastNameXX +
		' ' +
		hasLastNameYY +
		' ' +
		hasLastNameZZ +
		' ' +
		hasLastNameAA
);
```

Outcome:

```javascript
true , false, false , true (in case of !=)
true , true, true, true (in case of !==) => so in this sample not the correct answer
```

plunkr link: [https://plnkr.co/edit/BJpVHD95FhKlpHp1skUE](https://plnkr.co/edit/BJpVHD95FhKlpHp1skUE)

[Share](https://stackoverflow.com/a/46665302/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/ 'The current license for this post: CC BY-SA 3.0')

[Edit](https://stackoverflow.com/posts/46665302/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered Oct 10, 2017 at 11:11

[

![Ben Croughs's user avatar](https://www.gravatar.com/avatar/97677628666ee64f04bf6f56bd11020c?s=64&d=identicon&r=PG)

](https://stackoverflow.com/users/3122378/ben-croughs)

[Ben Croughs](https://stackoverflow.com/users/3122378/ben-croughs)Ben Croughs

2,61611 gold badge2222 silver badges3232 bronze badges

1

-   This is not good test. None of those values are _strictly_ `null`. Try this: [plnkr.co/edit/NfiVnQNes1p8PvXd1fCG?p=preview](https://plnkr.co/edit/NfiVnQNes1p8PvXd1fCG?p=preview)
    – [simonhamp](https://stackoverflow.com/users/123696/simonhamp '3,250 reputation')
    [Nov 9, 2017 at 12:46](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment81352774_46665302)

[Add a comment](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

0

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/57862452/timeline)

Show activity on this post.

careful if you're using local storage, you can end up with the string undefined rather than the value undefined:

```javascript
localStorage.setItem('mykey', JSON.stringify(undefined));
localStorage.getItem('mykey') === 'undefined';
true;
```

People may find this useful: [https://github.com/angular/components/blob/master/src/cdk/coercion/boolean-property.spec.ts](https://github.com/angular/components/blob/master/src/cdk/coercion/boolean-property.spec.ts)

```javascript
/**
 * @license
 * Copyright Google LLC All Rights Reserved.
 *
 * Use of this source code is governed by an MIT-style license that can be
 * found in the LICENSE file at https://angular.io/license
 */

/** Coerces a data-bound value (typically a string) to a boolean. */
export function coerceBooleanProperty(value: any): boolean {
	return value != null && `${value}` !== 'false';
}

import { coerceBooleanProperty } from './boolean-property';

describe('coerceBooleanProperty', () => {
	it('should coerce undefined to false', () => {
		expect(coerceBooleanProperty(undefined)).toBe(false);
	});

	it('should coerce null to false', () => {
		expect(coerceBooleanProperty(null)).toBe(false);
	});

	it('should coerce the empty string to true', () => {
		expect(coerceBooleanProperty('')).toBe(true);
	});

	it('should coerce zero to true', () => {
		expect(coerceBooleanProperty(0)).toBe(true);
	});

	it('should coerce the string "false" to false', () => {
		expect(coerceBooleanProperty('false')).toBe(false);
	});

	it('should coerce the boolean false to false', () => {
		expect(coerceBooleanProperty(false)).toBe(false);
	});

	it('should coerce the boolean true to true', () => {
		expect(coerceBooleanProperty(true)).toBe(true);
	});

	it('should coerce the string "true" to true', () => {
		expect(coerceBooleanProperty('true')).toBe(true);
	});

	it('should coerce an arbitrary string to true', () => {
		expect(coerceBooleanProperty('pink')).toBe(true);
	});

	it('should coerce an object to true', () => {
		expect(coerceBooleanProperty({})).toBe(true);
	});

	it('should coerce an array to true', () => {
		expect(coerceBooleanProperty([])).toBe(true);
	});
});
```

[Share](https://stackoverflow.com/a/57862452/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/57862452/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

answered Sep 9, 2019 at 23:55

[

![Rusty Rob's user avatar](https://i.stack.imgur.com/EyfoY.jpg?s=64&g=1)

](https://stackoverflow.com/users/632088/rusty-rob)

[Rusty Rob](https://stackoverflow.com/users/632088/rusty-rob)Rusty Rob

16.8k99 gold badges102102 silver badges119119 bronze badges

[Add a comment](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

\-1

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/73722283/timeline)

Show activity on this post.

You could use:

```javascript
if (!!variable) {
}
```

it equals writting

```javascript
it (variable != null && variable != undefined) {}
```

[Share](https://stackoverflow.com/a/73722283/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/ 'The current license for this post: CC BY-SA 4.0')

[Edit](https://stackoverflow.com/posts/73722283/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited Sep 14, 2022 at 19:32](https://stackoverflow.com/posts/73722283/revisions 'show all edits to this post')

answered Sep 14, 2022 at 19:32

[

![Hussam Almotlak's user avatar](https://www.gravatar.com/avatar/24142506a300be74bd1dde5ecd3bef24?s=64&d=identicon&r=PG)

](https://stackoverflow.com/users/19988081/hussam-almotlak)

[Hussam Almotlak](https://stackoverflow.com/users/19988081/hussam-almotlak)Hussam Almotlak

2322 bronze badges

1

-   4
    This would omit any value that _could_ be valid that resolves to false when double-negated, such as 0 or an empty string.
    – [mwieczorek](https://stackoverflow.com/users/280919/mwieczorek '2,172 reputation')
    [Oct 27, 2022 at 9:20](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment131037592_73722283)

[Add a comment](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.') | [](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Expand to show all comments on this post')

This answer is useful

\-8

This answer is not useful

Save this answer.

[](https://stackoverflow.com/posts/28977628/timeline)

Show activity on this post.

I always write it like this:

```javascript
var foo: string;

if (!foo) {
	foo = 'something';
}
```

This will work fine and I think it's very readable.

[Share](https://stackoverflow.com/a/28977628/15588573 'Short permalink to this answer')

Share a link to this answer (Includes your user id)

Copy link[CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/ 'The current license for this post: CC BY-SA 3.0')

[Edit](https://stackoverflow.com/posts/28977628/edit 'Revise and improve this post')

Follow

Follow this answer to receive notifications

[edited Sep 9, 2019 at 23:54](https://stackoverflow.com/posts/28977628/revisions 'show all edits to this post')

[

![Rusty Rob's user avatar](https://i.stack.imgur.com/EyfoY.jpg?s=64&g=1)

](https://stackoverflow.com/users/632088/rusty-rob)

[Rusty Rob](https://stackoverflow.com/users/632088/rusty-rob)

16.8k99 gold badges102102 silver badges119119 bronze badges

answered Mar 11, 2015 at 2:36

[

![AlexB's user avatar](https://www.gravatar.com/avatar/fe31b604ef32b100fae069287f2b7fa4?s=64&d=identicon&r=PG&f=y&so-version=2)

](https://stackoverflow.com/users/1576430/alexb)

[AlexB](https://stackoverflow.com/users/1576430/alexb)AlexB

68522 gold badges77 silver badges1515 bronze badges

3

-   26
    Wouldn't work for numbers because `0` also passes the `!foo` test.
    – [hasen](https://stackoverflow.com/users/35364/hasen '164,315 reputation')
    [May 18, 2016 at 17:58](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment62135308_28977628)
-   10
    Does not work for booleans either, where `undefined` is different than `false`. This is very common with optional boolean function parameters, where you should use the common JavaScript approach: `function fn(flag?: boolean) { if (typeof flag === "undefined") flag = true; /* set default value */ }`
    – [Gingi](https://stackoverflow.com/users/225386/gingi '2,229 reputation')
    [May 27, 2016 at 18:00](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment62475728_28977628)
-   Seems to work ok for booleans: `var isTrue; if(isTrue)//skips, if(!isTrue)// enters if(isTrue === undefined)//enters`. Also tried it in typescript with `var isTrue:boolean` which was undefined, and the same if checks. @Gingi, is there something different about what you tried and what I tried?
    – [Drenai](https://stackoverflow.com/users/271012/drenai '11,892 reputation')
    [Aug 7, 2016 at 19:10](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined#comment65002172_28977628)

[Add a comment](https://stackoverflow.com/questions/28975896/is-there-a-way-to-check-for-both-null-and-undefined# 'Use comments to ask for more information or suggest improvements. Avoid comments like “+1” or “thanks”.')
