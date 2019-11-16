1) What are the exceptions you would see in Strict mode ?

-> In strict mode you cannot use undeclared variables , The delete commad used to delete variables cannot be used.
The strict mode can be enabled globally by putting up 'use strict' on the top , but it is better if we use it inside blocks,
for example , inside functions

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

8) 




