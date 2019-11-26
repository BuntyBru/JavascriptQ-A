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
   c) Arrow functions cannot be used as a constructor, using the 'new' word with it will throw an error
   d) Usage of 'this' keyword
```
   var bunny = {
  name: 'Usagi',
  tasks: ['transform', 'eat cake', 'blow kisses'],
  showTasks: function() {
    this.tasks.forEach(function(task) {
      alert(this.name + " wants to " + task);
    });
  }
};
```
	Now in the above case it it will lead to the following output
```
	// [object Window] wants to transform
// [object Window] wants to eat cake
// [object Window] wants to blow kisses
```
	But when you use arrow function as an inside function in bunny, it would lead to correct output

```
var bunny = {
  name: 'Usagi',
  tasks: ['transform', 'eat cake', 'blow kisses'],
  showTasks() {
    this.tasks.forEach((task) => {
      alert(this.name + " wants to " + task);
    });  
  }
};

bunny.showTasks();
// Usagi wants to transform
// Usagi wants to eat cake
// Usagi wants to blow kisses
```
	While in ES5 function the 'this' refers to the parent of the function, In ES6 arrow functions use lexical scoping , 'this' refers to its current surrounding scope and no further.


18) In those boundary cases where 'this' keyword becomes problematic in ES5 functions, How would you make it work ?

-> There are two ways one of which is using 'bind()' and other is passing a reference of 'this'	by creating a variable inside of the function,
the 'bind(this)' should be added in front of the function inside the parent function.
```
var bunny = {
  name: 'Usagi',
  tasks: ['transform', 'eat cake', 'blow kisses'],
  showTasks: function() {
    this.tasks.forEach(function(task) {
      alert(this.name + " wants to " + task);
    }.bind(this));
  }
};
```

19) What is the difference between ES5 and ES6 version of javascript?

->  a) ES6 introduced arrow functions.
	b) ES6 introduced new ways of manipulating objects like the spread operator
	c) Introduction of Promises by ES6
	d) new way of exporting modules (export default myModule)
	e) Classes were introduced by ES6

20) What do you understand by Object.create ?

-> Object.create allows us to create an object and whenever there is a failed property lookup on that object, it can consult another object

```
const parent = {
  name: 'Stacey',
  age: 35,
  heritage: 'Irish'
}

const child = Object.create(parent)
child.name = 'Ryan'
child.age = 7

console.log(child.name) // Ryan
console.log(child.age) // 7
console.log(child.heritage) // Irish
```
In the above code we see that the child object which has been made by  'parent' using Object.create(),
As we see that child object has not initialized the heritage key, but we still get the output


21) What is prototype and what is meant by prototypal Instantiation?

-> Every function in javascript has a prototype property that references an object.
Now instead of using Object.create(objName), we can directly delegate it to its prototype,like
Object.create(objName.prototype), We call this pattern as prototypal Instantiation., Prototype is a 
property that every function in JS has and it allows us to share methods along all instances of the function.


22) What is the use of 'new' keyword ?

-> When we invoke a function using the new keyword, the constructor job and the prototypal instantiation job is
already done.

23) Explain about static methods in class ?

-> The methods which are assigned to class , not its prototypes are called static methods.
Simply put, static methods are those which can be used by the class directly 

24) Explain about getters and setters in javascript ?

-> ```
var person = {
    firstName: 'Jimmy',
    lastName: 'Smith',
    get fullName() {
        return this.firstName + ' ' + this.lastName;
    },
    set fullName (name) {
        var words = name.toString().split(' ');
        this.firstName = words[0] || '';
        this.lastName = words[1] || '';
    }
}
person.fullName = 'Jack Franklin';
console.log(person.firstName); // Jack
console.log(person.lastName) // Franklin
```

Many times it may happen that we would want to have a value from the object which is a mix of two or more properties
In order to achieve that we make the use of getters and setters


25) What is the usage of Object.defineProperty ?

-> Object.defineProperty(objName, 'propertyName',{key:value}), It is used to define a new property directly on the 
object or modifies an existing property on the object and returns the object.

26) Explain Promises ?

-> A Promise is an object that may produce a single value at sometime in the future, either a resolved value,
or a reason which says why it is not resolved, A promise may be one of the possible 3 states
fulfilled, reject or pending, A callback can be attached to Promise to handle the fulfilled value or the reason for the rejection.

We use the new keyword to create an instance of promise
```
const promise = new Promise()

```

27) What is the difference between undefined and not defined in javascript ?

-> When a variable is declared but it is not initialized , it will give undefined, whereas when a variable is not declared but it is mentioned , it will give defined

28) Explain about SSL Handshake ?

-> Whenever we browse an HTTPS URL through a browser , we have too experience the SSL handshake.
The browser and the website is creating an HTTPS connection using one way SSL handshake

The main purpose of the SSL handshake is to provide privacy and data integrity for communication between a 
server and a client, During the handshake the server and client will exchange important information required to establish a secure connection, there are two types of SSL handshakes , one-way SSL and two-way SSL

The difference between them is that in one way SSL only the server authenticates with the client whereas in two-way SSL both the server and client authenticate to each other. Usually when we browse a website, One way SSL is only used, Two way SSL is mostly used in server to server communication where both parties need to validate the identity of each other.

the steps are as follows
a) the client will send information that will be required by the server to start a HTTPS connection , through the information , the client notifies the server with its version of TLS and the cipher suite list the client supports

b) The server will respond back with the configuration it selected from the client's message along with its information to proceed with the handshake, Server will select the TLS version suggested by the client (the highest supported by the server), It will also send back the cipher suite which it selected from the list of cipher suits given by the client, Along with the Server Hello, the server will also send the certificate of the server with the certificate chain, the certificate chain will be validated against the certificates in the client trust store.

c) The message sent by the server to the client will be used by the client to generate the per-master secret.

d) The next step is of the certificate request., During this step the server will send a certificate request from the client with the certificate type and other details supported by the server , there are situations where the certificate may be empty and the client may decide whether to proceed with the client certificate or not, this marks the end of server Hello

e) The client then presents its Certificate chain to the server, The certificate needs to be appropriate with respect to the negotiated cipher suite key exchange algorithm

f) Client key exchange message :- This message needs to be send by the client following the Client Certificate message , If the client certificate is not being presented the client key exchange message should be sent after the client recieves the Hello Done message 

g )Finished


29) What do you understand by CORS
-> CORS stands for Cross Origin Resource sharing, CORS is a mechanism that tells a browser when it is allowed to access a particular request when it is not of same origin.
Whenever you try to access an API which is not of the same origin(when the endpoint is not same) , Whenever you make a cross origin request the server has to include a header when it sends the response back to your browser, So whenever you make a REST API call, the response you get back is the header file and the body, SO when you make a request you can attach this header file and at the same time when you get back the response you get it along with the headers

The request which you send to the server should have a header file sent to the server so that the server gets to know that yes it is okay to open this request. The header is send mostly to avoid any malicious attacks from happening


30) What do you mean by NaN in javascript ?

-> NaN stands for Not a Number, NaN property is a value representing Not-A-Number, It is a returned value when math functions fail, example parseInt('apple') , will give NaN
We can check about NaN by using isNan();






