# You Don't Know JS: Scope & Closures
# Chapter 3: Function vs. Block Scope

What kind of Javascript constructs create scopes ?

## Scope From Functions

Javascript functions are the main source of scope.

## Functions As Scopes

IIFE can be used to create a scope.

```js
var a = 2;

(function foo(){ // <-- insert this

	var a = 3;
	console.log( a ); // 3

})(); // <-- and this

console.log( a ); // 2
```

`(function foo(){ .. })` is using a function expression, `foo` is not visible in the outside scope neither in the created function scope.

### Anonymous vs. Named

Anonymous function expressions are also possible :

```js
setTimeout( function(){
	console.log("I waited 1 second!");
}, 1000 );
```

It has some disadvantages :

1. No name in stack trace so debugging more difficult.

2. No recursion possible, `arguments.callee` is deprecated.

3. Less self documented code.

### IIFE (Immediatly invoked function expression)

```js
var a = 2;

(function foo(){

	var a = 3;
	console.log( a ); // 3

})();

console.log( a ); // 2
```
Possible variation: `(function(){ .. }())`.

These two forms are identical in functionality. **It's purely a stylistic choice which you prefer.**

Another possible variation is to passs arguments:

```js
var a = 2;

(function IIFE( global ){

	var a = 3;
	console.log( a ); // 3
	console.log( global.a ); // 2

})( window );

console.log( a ); // 2
```

This can be used to prevent overridings of the `undefined` value:

```js
undefined = true; // setting a land-mine for other code! avoid!

(function IIFE( undefined ){

	var a;
	if (a === undefined) {
		console.log( "Undefined is safe here!" );
	}

})();
```

Another variation used in UMD:

```js
var a = 2;

(function IIFE( def ){
	def( window );
})(function def( global ){

	var a = 3;
	console.log( a ); // 3
	console.log( global.a ); // 2

});
```

## Blocks As Scopes

Javascript has also block scope. A block is essentially a `{ }` construct. Blocks are typically found in `if` or `for` statements. `with` statement also creates a block scope. `catch` also creates a block scope.

### `let`

`let` attaches to he nearest block it's been defined in. `let` doesn't have *hoisting*.

```js
var foo = true;

if (foo) {
	let bar = foo * 2;
	bar = something( bar );
	console.log( bar );
}

console.log( bar ); // ReferenceError
```

### `const`

`const` also creates block scoped variables. Its value can't be reassigned.
```
