---
layout: post
title:      "Variables, Hoisting, and Scope in JS"
date:       2018-09-27 12:00:33 -0400
permalink:  variables_hoisting_and_scope_in_js
---



  Scope is an important concept in Javascript.  Scope, by definition, refers to where "things" are available to other "things" in the context of the program.  These things can be both functions and variables.
  The largest most "available" scope is referred to as the global scope.  Functions and variables declared in this scope are available everywhere within the program. Functions have their own scope, inside which variables can be declared and used ONLY within that function.  Variables declared inside a function cannot be accessed outside of the function.  Block statements, such as conditional if statements, also have their own scope.  Variables declared with const or let cannot be accessed outside of this block, but declaring with "var" will allow them to be accessible outside of the block.
  When dealing with functions, scope can be "chained." Functions can have functions declared inside of them.  The context of the inner functions is the parent function, so they cannot be accessed from the global scope.  This scope chain points inward, and outer functions do not have access to variables declared within their inner functions.  Another interesting fact is that Javascript compiles and executes code in two different phases. For example:
```
 const x = 1
  function  test ( ) {
  const x = 2
  return x
  }
```
 The function, when invoked, will return 2 instead of 1.  This is because in the first phase variables are declared, but not assigned a value.  During the second phase, the most-locally available value will be assigned to this variable, in this case the inner variable.  The program will not continue so it won't reach the globally scoped x variable.		 Functions also maintain the context in which they were declared.  That means even if a function is invoked within another function,  if the function was declared in the global scope that will still hold true while the second function is being invoked.
 Another important concept in JavaScript is "Hoisting."  Hoisting can lead to issues in code, which is why its preferrable to use "let" or "const" to declare variables instead of var.  The reason for this is because variables declared with var will be stored in memory as undefined during the first phase, so these variables will return "undefined" if referenced before a value is assigned to them.  Const and Let avoid this issue by throwing a reference error if no value is set before they are referenced, instead of returning "undefined."  In general, however, it is a good idea to declare variables at the top of a function before referencing them. Example:
```
 function hello () { 
 console.log(hi)
 var hi = "hi"
 }
```
 this function will log "undefined" because the variable did not have a value at the time of its reference.  This is because variable declarations are "hoisted" even though they are not physically moved.  As stated above, if the variable in the example was definied with let or const, it would return a reference error instead of returning a value.  
 
 Probably the most difficult concept I have discussed thus far is the keyword "this" in the JavaScript language. "This" is used to refer to an object, but that object changes significantly depending on where "this" is used or applied.  If used in the global scope, "this" will refer to the browser window, so "this" is usually used within functions.  In JavaScript, class objects often have functions called "methods" that pertain to instances of that class.  When "this" is called in a method, it will refer to the object that it is called on. The context changes, however, when that object has a method that uses a function within a function.  Since "this" takes on the context in which it is called, a function inside of a function will set the context to the global object, or window.  This is important to keep in mind because of how ubiquitous callback functions are while working with javascript.  One way around this dilemma is to use arrow functions instead of the normal syntax.  Arrow functions, even if they are callbacks, will assign the context of "this" to the function that is calling them.  A workaround for using arrow functions is to use ".bind(this)" chained to the block of the callback function.  Binding "this" will set the context of this within the callback function to the parent function. I personally prefer to use arrow functions as my callbacks so that I dont have to constantly bind values.  I think its generally easier and will allow you to avoid alot of mistakes and unintentional return values.

		 
		 
