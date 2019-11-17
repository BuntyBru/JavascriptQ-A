1) What are the exceptions you would see in Strict mode ?

-> In strict mode you cannot use undeclared variables , The delete commad used to delete variables cannot be used.
The strict mode can be enabled globally by putting up 'use strict' on the top , but it is better if we use it inside blocks,

2) How references work in Javascript?

-> In Javascript it is not possible to have a reference from one variable to another variable, it is only possible in the 
case of compound values(Object, Arrays)
for Ex : var a = 10 ; var b =a ,
Now if we change b it is not going to affect a, but if 'a' was an object and we were changing a key of an object, It would 
be affected

3) How would you try to copy contents of an object without keeping a reference ?

-> We can try looping in through the object, but the only problem which we will have here is that , only the first level 
keys would be copied, For example :- 
let mainObj = {a:2,b:33,c:{d:22,e:55}}
Now we apply the loop method(i.e going through all the keys of the mainObj and making it a part of another obj)
ans = {a:2,b:33,c:{d:22,e:55}}
Now if we do mainObj.a =44, the value of ans.a will not change, but at the same time, if we do mainObj.c.d = 98,
the value of ans.c.d= 98
This means that if one of the properties in the original object is an object itself, then it will be shared between the copy and 
the original making their respective propertied point to the same object, this is also known as Shallow copying

4) What is the use of Object.assign() method ?

-> let newObj = Object.assign({},mainObj);
Now mainObj's key values will be assigned to newObj, but the only pitfall with Object.assign is that, it also creates shallow copies


5) What do you mean by deep copying?

-> Deep copy refers to the copy in which all the content's of the object are copied to the newObject and none of those are reference type
This can be done by using JSON.parse(JSON.stringify(object))
let newObj = JSON.parse(JSON.stringify(mainObj));,  this will create a deep copy of the object, the only downfall of this process is that
if there is a function in the mainObj , it will not be copied

6) Do spread elements help in deep copying of javascript objects ?

-> No, they provide shallow copies

7) What is coercion ?

-> Coercion is the process of converting a value from one type to another

8) Which error would you get if you would try to refer to a variable which was not defined?

-> ReferenceError:- variableName is not defined

9) What do you understand by hoisting ?

-> Hoisting simply means raised on the top of or placed on the top of, Hoisting is limited to variables using var keyword and functions 
defined using function keyword, When we talk about hoisting block scope is implied.
Hoisting is a javascript mechanism where variables and function declarations are moved to the top of their code before execution.
The process of assigning variable declarations with a default value of undefined during the creation phase is called Hoisting.


10) What is the difference between let const and var ?

-> let , const and var all are used to declare variables in javascript.
var declarations are globally scoped or functionally scoped while let and const are block scoped
var variables can be redeclared and updated within its scope, let variables can be updated but they cannot be redeclared, const variables can neither
be updated or nor redeclared
var, const and let all are hoisted at the top but the only thing is var variables are initialized with undefined whereas rest are not initialized, hence
they will throw reference error,not defined
var and let can be declared without initialization, but const has to be initialized during declaration

11) If we declare a variable within a function, Can we access it outside?

-> No, if we try accessing it we will get Reference Error

12) What do you mean by dynamically typed behaviour of javascript ?

-> Javascript is a dynamically typed language this means that the type of variable can be assigned and changed at any time during the run time of your
application after it was already compiled by javascript browser engine

13) What do you understand by Execution Context?

->  One strategy for writing software is to break up the code into several pieces, Though these pieces may ave several names (functional modules,packages etc),
but they all exist for single purpose to break apart and manage the complexity in our applications, Just like functions/modules/packages allow you to manage the
complexity of writing code, Execution Context allows the javascript engine to manage the complexity of interpreting and running your code.

The first execution context created when the JS engine runs your code is the Global execution context.Initially this would consist of two things , a global object and 
a variable called this, this will be reference to the global object which is window.
Each execution context has two separate phases, the first phase is called Creation phase and the second phase is called Execution phase
Creation Phase in simple terms is a phase where , global object is created, 'this' is created , memory spaces are set up for variables and functions , and all the 
variable declarations are assigned with a default value of 'undefined'.

In Execution phase the JS engine starts running the code line by line and executing it.
There is also one another execution context, called Function Execution Context and it is created whenever a function is invoked, The only time an execution 
context is created when the Javascript engine first starts interpreting your code and whenever a function is invoked.

14) What is the difference between global execution context and function execution context ?

-> Whenever a function execution context is created, The javascript engine will
a) Create an arguments object
b) Create an object for this 
c) Set up memory space for variables and function
d) Assign variable declarations a default value of 'undefined' while placing any function declarations in memory

15) What do you mean by Scope chain ?

-> The process of Javascript engine going one by one and checking each individual parent Execution context if a variable does not exist in the local
execution context is called scope chain

16) What do you mean by Closures in javascript ?

-> We know that variables created inside of a function are locally scoped and they cannot be accessed once the function's Execution context has been popped off the 
execution stack. , The scenario where this is not true is if you have a function nested inside of another function, In this case the child function will still have 
access to the outer function scope even after the parent execution context has been removed from the Execution Stack

```
var count = 0

function makeAdder(x) {
  return function inner (y) {
    return x + y;
  };
}

var add5 = makeAdder(5);
count += add5(2)
```
when makeAdder execution context pops out, javascript creates what is called 'Closure Scope', Inside of that closure scope it is the same variable environment which existed in the makeAdder context, the reason this happened because we have a function nested inside another function , The inner function is nested inside of the makeAdder variable environment, Even after makeAdder Execution environment has been popped off the execution stack, because that closure scope was created , inner has access to the 'x' variable via scope chain 
This concept of a child function closing over the variable environment of its parent function is called Closures.


17) What is the difference between regular functions and arrow functions ?

-> a) The first is syntax
   b) Second is not using the return keyword
   c) Third is the usage of this keyword.
   








