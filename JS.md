# JS Questions

## TOC

- [IIFE](#IIFE)
- [scope](#scope)


Yangshun - 109 questions


0. Why is it, in general, a good idea to leave the global scope of a website as-is and never touch it?


The global scope is shared by ALL js scripts running on site, and this shared namespace will cause conflict when different scripts have same names for variables



solutions :  [hiding](#hiding), wrapping in function, block scoping, placing in objects, IIFE



There is only ONE window/global object

So while other objects       obj1 === obj1     			=> false

window === window   				=> true


1. What tools and techniques do you use for debugging JavaScript code?

   1. Chrome devtools
   2. debugger;
   3. console.log()


2. Explain the differences on the usage of foo between function foo() {} and var foo = function() {}


The former is a function declaration while latter is function expression

How do they differ? In hoisting behaviors. 

Function declaration is hoisted completely, its body hoisted
Function expression is hoisted like a variable, its body is left behind


3. Explain how this works in JavaScript

"this" is a reference to an object that is bound when a function is called and its binding object depends on the function's call-site, or the situation in which it is called


#### Four rules for "this" binding/ for normal function declarations

   1. new binding - new f();

   2. explicit binding - f.call(obj), f.apply(obj), f.bind(obj)

   3. object implicit binding - obj.f();


   4. default binding   f();


#### Arrow function "this" binding rules

For arrow functions, () =>{}, different rules:

   1. Look for parental scope, enclosing scope. If it is ()=>{}, keep looking up until find function(){}. 

   If none, then it will be global scope

   Arrow functions inherit "this" binding from surrounding scope. Therefore, any parental ()=> also inherited, until function found. So we keep looking up

   An arrow function ()=> in global gets global "this" binding




4. What's the difference between .call and .apply?

Both are functions designed to change the "this" binding of a function and invoke it at same time

   - bind "this"
   - call

   Differences:

   - C/Call - enter arguments are "comma-separated"
   - A/Apply - enter arguments as "array"

function add(a, b) {
  return a + b;
}

console.log(add.call(null, 1, 2)); // 3
console.log(add.apply(null, [1, 2])); // 3



5. Explain Function.prototype.bind.

It is a method that takes an object and a function and returns a copy of funtion with its "this" keyword bound to the given object

   - function.bind(this);





## Summary

Parser:

places parentheses after (), return, {}

After statements, parser put for you IF on separate lines
if on same line, error

var i = 0; i++;   good
var i = 0 i++     error
var i = 0         good
i++ 

expressions, yes semicolons
statements

function, for, while, if/else, no 

- places semicolons after statements only if on separate lines, if on same line, error
	includes return;
- function declarations require () if want to be expression
	two available IIFE format
-



	1. return, important esp. in react

	function foo() {
		return 
			{
				a:5
			}
		}
		foo(); undefined, because return -->    return;  {a:1};

		parser places ; on return, stopping it from returning anything
		
		function foo() {
			return (
				{
					a:5
				}
				)
			}
		foo();
	2. IIFE   - always requires (), others it is a declaration
		function foo() {
			
			}()
		error, because not an expression

		acceptable forms:

		(function foo(){}())
		(function foo(){})()

	3. 



https://news.codecademy.com/your-guide-to-semicolons-in-javascript/





### For loops

- for (var i = 0; i<10; i++ ) {
		console.log(i);
	}
	console.log(i);
	
	Three statements.

	1. initializer
	2. condition
	3. change
	
	if condition is true, loops until false

	a. **var i;** undefined < 10, so no code, var i= null, etc
	**var i = null;**
	**var i = undefined;**
	**var i = NaN;**
	b. **var i = 11;**, 11 < 10 false, so no code


	c. i is global, it will loop one extra time for the final checkup


- order of operations in for loop
	like a triangle with line

	1 initialize -> 2 check condition  <- 4 increment	
					3 code ->

	2, 3, 4 loop over and over until condition false


	1. intialize
	2. if condition okay, then run code
	3. code
	4. increment
	5. repeat step 2
	

	Therefore, the initalized variable will **always** be one increment from its final value

	ex: for (var i = 0; i<=10; i++){
	    console.log(i);
		
	   }
	print out 0 - 10

	Then last step is to 

	1. Increment, therefore i = 11
	2. check condition last time, false, done


	for (var i = 0; i<10; i++){
	    console.log(i);
		
	   }
	i = 10

	for (var i = 10; i>0; i++){
	    console.log(i);
		
	   }
	i = 0
https://stackoverflow.com/questions/46716006/what-is-the-order-of-execution-in-a-javascript-for-loop




<a name="dom"></a>
### DOM  --   Document Object Model


It is the HTML converted to a javascript object by the browser

#### Difference between "Attributes" and "Properties"

HTML - Have Attributes on elements

DOM - has Properties on objects

They seem like same thing, but when accessed by javascript, attribute getAttribute gives inital/default

properties give newest  



const input = document.querySelector('input');
console.log(input.getAttribute('value')); // Hello
console.log(input.value); // Hello

https://stackoverflow.com/questions/19246714/html-attributes-vs-properties

https://stackoverflow.com/questions/258469/what-is-the-difference-between-attribute-and-property

https://github.com/yangshun/front-end-interview-handbook/blob/master/questions/javascript-questions.md#whats-the-difference-between-an-attribute-and-a-property

https://stackoverflow.com/questions/6003819/what-is-the-difference-between-properties-and-attributes-in-html








<a name="functions"></a>
### Functions


  1. Value
  2. parameters
  3. Return

#### Value

functions are a value

typeof function == "function"

But it is a subtype of object


can be returned

This is important because instead of f() inside a function, like IIFE

f()
	return f

Then we can save f value and **reuse** it

Like counter closure




#### Parameters

Parameters are the variables that functions bind when receive input

f(a,b)

and invoked  f(x,y)


function saves variables


var a = x;
var b = y;

**implicitly**


So this inludes in closures

var z = 1;
var q = (function bob(a) {

  return function() {
    return a;

  }
(z))



z = 7;

var w = q();

// w == 1;
// so implicit var a = z == 1;
// Saved 1, so even if outer z is now 7, still 1





#### Return

nothing returned  -  return;   returned undefined
no return  -  console.log();   returns undefined


f returned - reusable, 

   
  1. return value;
     return function() {};
     return console.log;


  2. return f();       returns the returned value of function
	 
	 return console.log('');


	 console.log() returns nothing, so return console.log();

	 returns undefined


	 it is useless


  3. return;

     no return specified 

     so undefined return


  4. No return defined at all


     returns undefined 

     ex:   var x = new Person();    returns object


      however,    var x = Person();  calls, but no defined return


      therefore, x == undefined


	** Two Examples **

	1. var x = Constructor();    no new binding, so undefined
	2. return console.log();    prints out only, no return


#### Function Formats

  1. function 
     function x() {console.log('rethr')}

  2. function expression
     var x = function() {console.log('rethr')}

  3. named function expression

     var x = function y() {console.log('rethr')}
  4. IIFE

     (function(){console.log('rethr')})()

  5. named IIFE
     (function y(){console.log('rethr')})()

Only the name of function declaration is remembered

Rest is thrown out, not accessible
1:4


#### Uses:

  1. Reuse blocks of code, refactor, DRY
  2. Wrap code to ["hide it"](#hiding)

<a name="fdeclarationfexpression"></a>
### Function Declaration vs Function Expression

Function Declaration:

function foo() {}


Function Expression: 

var foo = function(){}



Main difference: hoisting behavior

Function declaration's full body is hoisted

Function expression is hoisted like variable, body left behind, assigned later



<a name="arrowfn"></a>
### Arrow Functions - ()=>{}, new function syntax and "this binding"

  - If NO parameter, ()=>{}, () necessary
  - If ONE parameter, a =>{}, () unnecessary
  - If >ONE parameter, (a,b)=>{} () necessary

  - implict one line return
    ()=> 5

    implicit OBJECT return

    ()=> ({a:1}), wrap object in parentheses

  - explicit return, or more than one line

    () => {return 5}

    () => {
		console.log(5);
		return 5;
	}

	()=>return 5;    =>  error

  - Different "this binding", look for enclosing function(){}s





<a name="IIFE"></a>
### IIFE - immediately invoked functions

**Think of IIFE as f(), in one statement**

IIFE == f define then f();
		f
		f();

#### Two acceptable formats

	1. (function() {})()
	2. (function(){}())

	function(){}() not allowed, as parser sees function(){} as declaration, not expression to be invoked


   1. named
   2. unnamed


#### Putting IIFE in var

Normal F in var, gives reference to function

var x = function foo() {
	console.log('foo');
}

x(); => 'foo'



IIFE in var gives what is returned, just like putting f() into var
return nothing, just c.l, undefined


var x = (function foo() {
	console.log('foo');
})();

x => undefined

var x = (function foo() {
	return 'foo';
})();


i.e.  IIFE is just one step ahead of f, f().

normal f - return f value
iife - returns what f returns



<a name="hiding"></a>
### Hiding using Scope

Scope allows programmer to hide and minimally expose code




Tools:
1. function wrapping, to create closure
   
   Wrapping with all 4 others:
   IIFE, named IIFE
   FE, named FE

   function level scoping

2. objects: storing functions in objects
3. Block-level scoping

   let is like var, but block-scoped, and NOT hoisted

   ex: if() { let x = 5} console.log(x)  //Reference Error
    
   console.log(bar) reference error
   let bar = 5;

   even place in arbitary block, it will bind

   

   const - block-scoped, 

<a name="hidingvsclosure"></a>
### Hiding vs Closure

1. Hiding - has to do with protecting from global scope, creating own scope
   Principle of Least Exposure - only show/make global minimum necessary, hide all else by wrapping it
   POLE

2. Closure - has to do with mobility, ability of function to access/reference its original scope when called outside its own originally declared scope



<a name="scope"></a>
### Scope


#### Definition of Scope
- Set of access of variables
- Set of rules that determine access to variables, or how variables are 
  - found
  - stored
  - accessed later
- Also more than one scope
  - global scope
  - function scope
  - block scope
  - nested scope

- Two types of declarations: 
  1. function
  2. variable

    Variable is split into 
    LHS - var a;
    RHS - a = 2;
	LHS statement
	LHS lookup

	LHS - not necessarily left, but look for container/variable to assign
	look up, assign
	implicit parameter assignment
	a = 2, LHS

	RHS - not necessarily right, but look upvalue
	calling function, var, 
	foo(), foo is RHS

1. When encountering JS declaration, functions are collected
  variable declarations split in two, first part collected

  var a = 2;     =>    var a;
2. If this variable already exists, skip
3. If dne, create new
4. Then later, when encounter a=2; look for variable a
5. If yes, use
6. If no, 
7. If none at all, error

RHS lookup, lookup value
console.log(a);


- JS Engine looks for closest declared variable, from innermost scope to outermost. If variable does not have declaration, it is made global

  The search is stopped once engine finds variable, hence why value of a variable if the innermost value available

  JS engine sees variable declaration as two separate statements
  ex: var a = 2; =>   var a; and a = 2;


  **ALL** declarations, the var a;, function declaration are executed FIRST before the rest of code. This behavior is called "hoisting" because it is similar to pulling the declarations or hoisting it to the top of code






<a name="hoisting"></a>
### Hoisting

- Two types of declarations: 
  1. function
  2. variable, declared variables only

     undeclared variables are NOT hoisted, such as in assignment


     a = 5; becomes global, declared, but not hoisted



- Hoisting is behavior of JS engine to execute all declaration portions of statements before any other code is executed

all function and variable declarations

#### Hoisting precedence

   1. functions are hoisted before var
      
      function foo

      var foo;     ->   ignored
   2. If more than one function with same name, **Latest** function is assigned

   ex: function foo(){console.log(5);}

   function foo(){console.log(10);}

   foo();       ->    10



<a name="types"></a>
### Types

#### Seven Types


  1. Symbol - new ES6
  2. Number
  3. Object
	
	Object Subtypes


    functions
    arrays
    built-in constructors

  4. String
  5. null
  6. undefined
  7. Boolean


<a name="typeof"></a>
### Typeof

typeof is way to check type of value


#### Seven possible Answers  -- These do NOT correspond exactly to the seven listed types

  - All the answers are lowercase
  - Strings

    so typeof typeof anythign    --   always "string"

  - typeof undeclared variable == "undefined"

    can be used to check for undeclared variables

   1. "symbol"
   2. "number"

      NaN becomes part of type "number"

   3. "boolean"
   4. "string"
   5. "undefined"
   6. "function"

      function is removed from object and becomes its own type
   7. "object"

      null, array, objects all go under object


#### How to check type using typeof for special cases?

1. NaN
  
  isNaN()  ->   problem is it gives true for anything not a number, 
  [], '', etc


  so isNaN(NaN) && NaN !== NaN should give true for NaNs

2. Array
  
  Problem is array, objects both gives typeof == "object"

  so, need


  typeof [] == "object" && [].constructor == Array

3. Object

  typeof {} == "object" && {}.constructor == Object


  
  each object has constructor property in its prototype, which points to the Native objects



typeof to check
1. special cases
2. undeclared variables
   ex: typeof NULL == "undefined"


<a name="object"></a>
### Objects


#### Built-in Objects
NH

  1. Host Objects
  
  Objects provided by runtime environment, the browser or node


  ex: window, document, setTimeout

  2. Native Objects

  Objects that are part of JS v8 engine, 

  ALL constructor objects

  Array, String

  Math



#### Check Properties


  1. in, property in oject

    true/false, but goes all the way up chain

  2. Object.hasOwnProperty("prop");, only checks own object


#### To loop through properties

  1. for property  in object  

   (for of loops don't work on objects)

   https://stackoverflow.com/questions/29885220/using-objects-in-for-of-loops

  2. best:   Object.keys(obj)  to get array of keys.







<a name="ternaryoperator"></a>
### Ternary Operator

Means three, unary one, binary two


Three operands, Two operators, shortcut if/else



 Conditional ? True execute : False execute
  

#### Uses:


  1. For assigning variable conditionally, used often in React


  var x =  a ? b : c

function greeting(person) {
    var name = person ? person.name : "stranger";
    return "Howdy, " + name;
}

console.log(greeting({name: 'Alice'}));  // "Howdy, Alice"
console.log(greeting(null));             // "Howdy, stranger"​​​​​


<a name="var"></a>
### Variables


   1. Declared variables



   2. Undeclared variables 

      NOT hoisted


      To check,   var, gives reference error


      To check if undeclared var,


      typeof undecl == "undefined"


<a name="varletconst"></a>
### Var vs Let vs Const

let and const are new ES6, variable declarations

Differences:     var vs (let and const)

   1. var is function scoped         let/const are block scoped (meaning they are scoped/accessible only within {} closest block)
      
      blocks include:
      - {}, arbitrary blocks
      - functions 
      - for loops
      - if else
      - try catch
      - with

   2. var is hoisted                 let/const not hoisted, give refernce error


   3. var can be declared many times
      var x, var x, no error

      let/const can be declared only once
	  let x = 5;
	  let x   =>  error


   4.   This differnce is   let vs const

       Both can only be declared once


       But let can be reassigned

       const can only be assigned once


       let x = 5;
       x = 7;


       const z = 7;
       z = 9   => error

       but not immutable:   const z = []; z.push(5); //[5]







<a name="closure"></a>
### Closure - think of as saving context with variables, like saving global context, but instead a function's local scope and context with its variables, allowing saving and incrementing

#### **simple** 
1. function 
2. and access to its saved reference scope/variables from where it was originally declared, like a backpack of scope that it always brings when called outside declared context

closure over == access to its scope
ex: closure over inner scope of f1, access to scope of f1
**function**
**Access to scope where originally declared**

3. when function called outside its originally declared context/own scope, brings along its saved scope



**Called outside originally declared scope, has reference to scope**

#### Examples
we see closure whenever
- inner function called outside its declared are
  2/5 combo below

- setInterval also has closure, because keeps scope alive from original declared, due to inner f
  f1
    setInterval f2
- setTimeout also has closure, saves scope, due to inner f
  f1
    setTimeout f2

	for (var i=1; i<=5; i++) {
		(function(j){
			setTimeout( function timer(){
				console.log( j );
			}, j*1000 );
		})( i );
	}
- function passed into another function, also shows closure by bringing scope
- any asynchronous function
- ajax
- event handlers, 

- f in global scope is not considered closure because not called out of its originally declared context

scope backpack/variables, etc
function 						=>	   closure



#### inner function in saved context, retains access to its parent's variables, even though parental scope is gone/closed, such as in parental IIFE


function called in saved context

f1 - saved context, it is thrown out, parental scope closed
  f2 - saved, var of f1 saved with f2


#### common closure formats

demonstrating closure involves executing inner f/f2


1. outer f - f or IIFE
  2
2. inner f - f(), IIFE (good for one time, setTimeout), return f (good for counter), setTimeout, setInterval
  
  5
return f, allows reuse, such as timer

or f(), which just executes and cant access, but good for settimeout


#### Examples:

a. Outer IIFE, inner return f

var add = (function () {
    var counter = 0;
    return function () {counter += 1; return counter}
})();

add();
add();
add();

// the counter is now 3

https://www.w3schools.com/js/js_function_closures.asp

b. Outer IFFE, inner IFFE

(function() {
	var count = 0;
	(function foo() {
		console.log(count);
		count++;
		setTimeout(foo, 200)
	})()
})()

c. Outer f, inner return f

function add() {
    var counter = 0;
    return function () {counter += 1; return counter}
}

var x = add();

x();
x();
x();

// the counter is now 3


### this


### setTimeout and setInterval


- setTimeout(f(parameter){}, delay, arg, arg)
- setInterval(f(parameter){}, delay, arg, arg)

- clearTimeout(id)  id is from variable, which is from when var x = setTimeout

- clearInterval(id)  id is from variable, which is from when var x = setInterval  
  
  clearInterval **CAN** be called within the setInterval

(function counter() {
	var count = 0;
	var timer = setInterval(() => {
		console.log(count);
	    if (count == 10) {
			clearInterval(timer);
		}		
		count++;
	}, 200)
})()

  https://stackoverflow.com/questions/16599878/can-clearinterval-be-called-inside-setinterval



#### Similarities

- Both do **NOT** execute on first zero seconds, but until **AFTER** first set of time
 example: setTimeout(()=>{},200) after 200ms, do code, not on the zero
 example: setInterval(()=>{},200) after 200ms, do code, not on the zero

- To stop, save setTimeout/setInterval into a variable to get its ID.
  var x = setTimeout(())
  clearInterval(x);
- 




#### Differences
function counter() {
	var count = 0;
	setTimeout(() => {
		console.log(count);
		count++;
		setTimeout(counter, 1000);
	},1000)

}
counter();



sto sto closure, vs just executing in time interval









### Array

#### Add to front

- array.unshift()

- [x, ...array]

#### Add to end

- array.push()

- [...array, x]






<a name="usestrict"></a>
### Use Strict/Strict Mode,    "use strict"



<a name="asyncsync"></a>
### Asynchronous vs Synchronous Code

#### Asynchronous code: 
  1. Non Blocking
  2. Executed out of order of program
  3. Does not wait, while being processed, other code/parts of program is allowed to run

  Asynchronous is LATER code


#### Synchronous code: 
  1. Blocking
  2. Executed in order of program
  3. Wait until completion to execute next step. So if a part of code takes long time, it blocks the entire program. ex: alert function



<a name="eventloop"></a>
### Event Loop


single threaded loop
monitors call stack and task queue/callback queue
if call stack empty, task queue not empty

push from task queue to call stack, execute


<a name="cbcallback"></a>
### Callbacks/cb

#### Two definitions


  1. Function that is run asynchronously, run after some gap of time
  2. A function that is generally passed into another function



<a name="promise"></a>
### Promises

  Promises are OBJECTS, so typeof  == "object"

  These objects represent promises of future values


  They have Three states:

  1. pending


    After pending, promise is said to be 

    "resolved"

    There are Two "resolved" states: 

  2. fulfilled
    Like promise fulfilled

  3. rejected


   Ex: order of cheeseburger


   later, get cheeseburger (fulfilled)

   or later, get nothing (rejected)



<a name="cbcallbackvspromise"></a>
### Callbacks vs Promises

#### Callbacks are what were primarily used for two decades before promises came into picture
   
   Problems:

   1. Callback hell
      
      Nested callbacks prevented easy reading, hard to manage code

      Lack of readability

   2. Lack of readability, not sequential

       The callbacks nested prevented from easy reading 


#### Promises:
   
  1. Solved problem of nesting, by creating chainable

  "then" functions

  2. Read async code like sequential code using "then"





### types and Abstract (==) vs Strict (===) equality operators



<a name="operators"></a>
### Operators

1. +
2. - 
3. *
4. /
5. % - modulus operator      --     results in **INTEGER**
  
  It takes the remainder of the number
  NOT the decimal value

  
  15%7   1 NOT 1/7

  To get just decimal
  1. can String(number) then get second part
  2. Get % number   then divide by denominator to get fraction

  
  **watch out!!!**

  for 0, because modulus operator returns 0 for 0%0

6. ++

   Two Forms:

  1. x++

    This returns the x, and increments after, so
    x = 5;
    var y = x++

    x now 6,
    y is 5, because returned BEFORE incremented


  2. ++x

    This increments THEN returns x, so
    x = 5;
    var y = ++x

    x now 6,
    y is also 6, because incremented BEFORE returned


7. --
   
   Same as ++, but with subtraction

8. +=

<a name="orderofoperations"></a>
### Order of Operations


1. From left to right, two at a time
  
  5+"2" + 'wow';

  5 + "2"  ->    "52"
  "52" + "wow"   ->  "52wow"

2. Unary before others

  5+ +"3q"     ->   5 + NaN ->  NaN



3. var a = b = 5;

   From right to left


   b = 5;
   var a = b;



<a name="typecoercionconversion"></a>
### Type Coercion or Type Conversion


#### Boolean

Operators: 3

1. !
  !5, 5 -> true, !true -> false;

2. if ()/else
3. &&  ||, these implicitly coerce to compare, but RETURN ORIGINAL value

  ex: 5 && 8,  5->true,  8->true, return **8**



    1. List of Falsey values
      1. null
      2. 0, -0
      3. undefined
      4. ""
      5. NaN

    2. ALL other values are therefore Truthy

      Includes ALL objects, such as [], {}

      Negative numbers

      !!-2  -> true;



#### Number

Operators: 4

1. +, only if ALL numbers
2. Unary operator, +/-
3. -,/, multiply always coerce to numbers
4. ==, coerce to number,

  If any boolean, always coerce to number,
  If any str, coerce to number

  however, null not coerced to zero, only for ==
  

  So Number(null) =>   0
  But null == 0;

  false, b/c not coerced



#### String

Operators: 1

1. +, is default, if any strings, concatenate




<a name="abstractequality"></a>
### Abstract Equality   ==

1. If differnt types, convert and compare values
   Precedence:
   If boolean, to nonboolean, to number
    
   If String, with number, convert to numer
  

  So  "5" == true;
      "5" == 1;

       5 == 1;  -> false


<a name="strictequality"></a>
### Strict Equality   ===

1. NO conversion
2. If different types, always false

  ex: "0" === 0   -> false


3. If same type, compare values
4. If values same, true, else false




<a name="eventdelegation"></a>
### Event Delegation

A technique in the DOM, where a single event handler is placed on parent as a delegate to receive and respond to event acted on child

This works because event bubbling allows event to propagate/be experienced by parents up to dom


ex:  ul
       li

   instead of placing multiple event handlers on li, place one on ul, to get e.target values



<a name="eventpropagation"></a>
### Event Propagation


#### Two Types of Event propgation

  These two types travel across SAME elements, just different directions

  1. Event bubbling
  
  Event travels from target to document top

  2. Event capturing

  Event travels from document top to target





<a name="modulusoperator"></a>
### Modulus Operator

%   -  gives back remainder


#### Can be used for Three main types of problems

1. Check if Even
  Even Numbers divided by 2, remainder is ALWAYS 0

  n%2 == 0;


2. Check if Odd
  Odd Numbers divided by 2, remainder is ALWAYS 1

  Math.abs(n%2) == 1;
  
  Because of negative even numbers


3. Check if Integer
  
  n%1, is NOT n/1, which always gives back numerator


  n%1 gives remainder, and if it is integer, get back 0

  function isInteger(n) {
    
    return Math.abs(n%1) == 0;

  }








<a name="ajax"></a>
### AJAX - Asynchronous javascript and XML

Techniques/technologies used to communicate with servers, fetch and update data
techniques to asynchronously send data and get data from servers without interfering with user/background

- communicate with server in background, get/update data
- allows updating of page without refreshing entire page



- past: XMLHttpRequest Object
- Now, fetch api


<a name="sameoriginpolicy"></a>
### Same Origin Policy
NOT single origin policy, but same

SOP, is used to limit ajax to same domain

- like preventing non parents from accessing child, parents, child, same origin

- policy to prevent ajax request cross domains
- it is a security feature/mechanism
- origin is defined as uri, hostname, and port number

  so same origin means having same:

  php
  1. protocol:   http:// vs https://
  2. hostname/domainname
  3. port   ex: :80


  paths can differ

  ex: http://shama.com and http://shama.com/bobo 

  is allowed

  but http://shama.com and https://shama.com, not because different protocol



url breakdown:
https://www.google.com/search?q=what+is+port+in+url&source=lnms&tbm=isch&sa=X&ved=0ahUKEwij94HksYrfAhWLnFkKHQOvBkIQ_AUIECgD&biw=1229&bih=578#imgrc=VCOjkKoo4Ee83M:


Two ways to bypass

1. CORS
2. JSONP


https://resources.infosecinstitute.com/bypassing-same-origin-policy-sop/




<a name="cors"></a>
### CORS - Cross Origin Resource Sharing

CORS is used to relax SOP, allow ajax cross domain

- policy to allow ajax request cross domains
- like non parents given access to report cards



<a name="jsonp"></a>
### JSONP - Javascript Object Notation with Padding

- Was created to bypass CORS policy of AJAX, so no CORS
- Uses script tag to execute function which passes JSON object

https://stackoverflow.com/questions/3839966/can-anyone-explain-what-jsonp-is-in-layman-terms


https://stackoverflow.com/questions/2067472/what-is-jsonp-all-about/2067584#2067584


