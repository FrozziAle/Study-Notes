# Memory management

- Description:
    _This is just an explanation of a garbage collection algorithm presented in_ [MDN-Garbage Collection](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management#Garbage_collection).
    
    
### Table of contents:

1. [Introduction](#introduction).
2. [Memory Life Cycle](#memory-life-cycle).


## Introduction

- Low-level language (eg. C language) have low level memory management primitives like `free()`. ( this is not important to us now but we mention that to say that memory management must be done **explicitly**).
- Unlike JavaScript, when for example objects are not used any more they are automatically "garbage collected" to free memory.
- This gives a _**wrong**_ impression to JS developers to not care about memory management.


## Memory Life Cycle

- Regardless of the programming language, memory life cycle is pretty much always the same:
    1. Allocate the memory you need. (_explicit in low-level languages implicit in high-level languages like JS_)
    2. Use the allocated memory. (read, write) (_explicit in all languages_)
    3. Release the allocated memory when it is not needed anymore. (_explicit in low-level languages implicit in high-level languages like JS (GARBAGE COLLECTION)_)

```
:point_right: Allocate the memory in JS
```
 JavaScript does it alongside with declaring values.
 
 ```
 :point_right: Use the allocated memory
 ```
 By reading or writing the value of a variable or an object property or even passing an argument to a function.

```
 :point_right: Release the allocated memory
```
- High-level languages embed a piece of software called "**garbage collector**" whose job is to track memory allocation and use in order to find when a piece of allocated memory is not needed any longer in which case, it will automatically _free it_. 
- This process is an approximation (knowing whether some piece of memory is needed is undecidable. This means it can not be solved by an algorithm).


## Reference Counting Garbage Collection

- Description:
    _This is just an explanation of a garbage collection algorithm presented in_ [MDN-Garbage Collection](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management#Garbage_collection).
- Definition: One of algorithms of JS Grabage Collection Algorithms.
- The most naive Garbage Collection algorithm.
- It reduces the definition of "an object is not needed anymore so Garbage collect it" to "an object has no other object referencing to it so Garbage collect it". 
- MDN Example with a more clear explanation:

```javascript
var o = { 
  a: {
    b: 2
  }
}; 
```
2 objects are created:

```javascript
{ 
  a: {
    b: 2
  }
}
```
And 
```javascript
{
    b: 2
  }
```
The first one is referenced by being assigned to variable `o`. The second is referenced by the first one as a property of it.

```javascript
var o2 = o; 
```
Now the first object has a second reference `o2`
```javascript
o = 1;     
```
But now one of its references `o` variable are being re assigned to a different value. So the first object now has one reference `o2`.
```javascript
var oa = o2.a; 
```
The second object now has a reference `oa` by assigning the `o2` object `a` property to `oa`
```javascript
o2 = 'yo';
```
Now the first object loses its last reference `o2`. So it can be garbage collected.
```javascript
oa = null; 
```
Now the second object loses its reference `oa`. So it can also be garbage collected.

           