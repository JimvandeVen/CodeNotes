# You Don't Know JS: Scope & Closures  

# Chapter 1: What is Scope?  

## Compiler Theory  

In a traditional compiled-language, a chunk of source code, your program will undergo three steps before it is executed, roughly called "compilation":  
1. **Tokenizing/Lexing:** Breaking up a string into meaningful chunks, called tokens. For example ```var a = 2;```. This will be broken into the following tokens: ```var```, ```a```, ```=```, ```2```, and ```;```.  

2. **Parsing:** Taking a stream (array) of tokens and turning it into a tree of nested elements, which collectively represent the grammatical structure of the program. This tree is called an "AST" (**A**bstract **S**yntax **T**ree).  

The tree of ```var a = 2;``` might start with a top-level node called ```VariableDeclaration```, with a child node called ```Identifier``` (whose value is a), and another child called ```AssignmentExpression``` which itself has a child called ```NumericLiteral``` (whose value is ```2```).  

3. **Code-Generation:** The process of taking an AST and turning it into executable code.  

## Understanding Scope  

### The Cast  

Let's meet the cast of characters that interact to process the program var ```a = 2;```, so we understand their conversations that we'll listen in on shortly:  

1. *Engine*: Responsible for start-to-finnish compilation and execution of our JavaScript program.  

2. *Compiler*: One of *Engine's* friends; handles all the dirty work of parsing and code-generation.  

3. *Scope*: another friend of *Engine*; collects and maintains a look-up list of all the declared identifiers (variables), and enforces a strict set of rules as to how these are accessible to currently executing code.  

### Back & Forth  

When you see the program ```var a = 2;``` the *Compiler* will proceed as:  

1. Encountering ```var a```, *Compiler* asks *scope* to see if variable ```a``` already exists for that particular scope collection. If so, *Compiler* ignores this declaration and moves on. Otherwise, *Compiler* asks *Scope* to declare a new variable called ```a``` For that scope collection.  

2. *Compiler* then produces code for *Engine* to later execute, to handle the ```a = 2``` assignment. The code *Engine* runs will first ask *Scope* if there is a variable called ```a``` accessible in the current scope collection. If so, *Engine* uses that variable. If not, *Engine* looks elsewhere (see nested Scope section below).  

### Compiler Speak  

**Left Hand Side(LHS)**: Declared 
**Right Hand Side(RHS)**: "Retrieve his/her source (value)" or "go get the value of..."  

### Engine/Scope Conversation  

```function foo(a) {
	console.log( a ); // 2
}

foo( 2 );
```  
> ***Engine***: Hey *Scope*, I have an RHS reference for `foo`. Ever heard of it?

> ***Scope***: Why yes, I have. *Compiler* declared it just a second ago. He's a function. Here you go.

> ***Engine***: Great, thanks! OK, I'm executing `foo`.

> ***Engine***: Hey, *Scope*, I've got an LHS reference for `a`, ever heard of it?

> ***Scope***: Why yes, I have. *Compiler* declared it as a formal parameter to `foo` just recently. Here you go.

> ***Engine***: Helpful as always, *Scope*. Thanks again. Now, time to assign `2` to `a`.

> ***Engine***: Hey, *Scope*, sorry to bother you again. I need an RHS look-up for `console`. Ever heard of it?

> ***Scope***: No problem, *Engine*, this is what I do all day. Yes, I've got `console`. He's built-in. Here ya go.

> ***Engine***: Perfect. Looking up `log(..)`. OK, great, it's a function.

> ***Engine***: Yo, *Scope*. Can you help me out with an RHS reference to `a`. I think I remember it, but just want to double-check.

> ***Scope***: You're right, *Engine*. Same guy, hasn't changed. Here ya go.

> ***Engine***: Cool. Passing the value of `a`, which is `2`, into `log(..)`.

> ...  

### Nested Scope  

Just as a block or function is nested inside another block or function, scopes are nested inside other scopes. So, if a variable cannot be found in the immediate scope, Engine consults the next outer containing scope, continuing until found or until the outermost (aka, global) scope has been reached.  

### Errors  

```ReferenceError``` is when te RHS and LHS look-up fails to find a variable.  
```TypeError``` is when the RHS look-up found something, but you are trying to do something with the value that is impossible.  





