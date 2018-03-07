# You Don't Know JS: Scope & Closures  

## Chapter 2: Lexical Scope  

### Lex-time  

Lexing (aka, tokenizing) is the first phase of a standard language compiler. Lexical scope is based on where variables and blocks of scope are authored, by you, at write time, and thus is (mostly) set in stone by the time the lexer processes your code.  

Let's consider this block of code:

```js
function foo(a) {

	var b = a * 2;

	function bar(c) {
		console.log( a, b, c );
	}

	bar(b * 3);
}

foo( 2 ); // 2 4 12
```
![](https://github.com/getify/You-Dont-Know-JS/blob/master/scope%20%26%20closures/fig2.png)  

**Bubble 1** encompasses the global scope, and has just one identifier in it: `foo`.

**Bubble 2** encompasses the scope of `foo`, which includes the three identifiers: `a`, `bar` and `b`.

**Bubble 3** encompasses the scope of `bar`, and it includes just one identifier: `c`.  

### Look-ups  

**Scope look-up stops once it finds the first match.** The same identifier name can be specified at multiple layers of nested scope, which is called "shadowing" (the inner identifier "shadows" the outer identifier). Regardless of shadowing, scope look-up always starts at the innermost scope being executed at the time, and works its way outward/upward until the first match, and stops.  

### Cheating Lexical
**Don't.**
