# You Don't Know JS: Scope & Closures  
# Chapter 4: Hoisting  

## The Compiler Strikes Again  

The *Engine* first compiles the code, and associates all declarations with their apropriate scopes. Then it interprets it.  

Consider this code:

```js
a = 2;

var a;

console.log( a );
```

What do you expect to be printed in the `console.log(..)` statement?

Many developers would expect `undefined`, since the `var a` statement comes after the `a = 2`, and it would seem natural to assume that the variable is re-defined, and thus assigned the default `undefined`. However, the output will be `2`.

Consider another piece of code:

```js
console.log( a );

var a = 2;
```  

Our first snippet then should be thought of as being handled like this:

```js
var a;
```
```js
a = 2;

console.log( a );
```

...where the first part is the compilation and the second part is the execution.

Similarly, our second snippet is actually processed as:

```js
var a;
```
```js
console.log( a );

a = 2;
```  

So, one way of thinking, sort of metaphorically, about this process, is that variable and function declarations are "moved" from where they appear in the flow of the code to the top of the code. This gives rise to the name "Hoisting".  

In other words, **the egg (declaration) comes before the chicken (assignment)**.  

