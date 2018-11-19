# JS Questions

## TOC

- [IIFE](#IIFE)



Yangshun - 109 questions

1. 


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



### Functions


#### Value

functions are a value

can be returned

This is important because instead of f() inside a function, like IIFE

f()
	return f

Then we can save f value and **reuse** it

Like counter closure

#### Return

nothing returned  -  return;   returned undefined
no return  -  console.log();   returns undefined


f returned - reusable, 


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



### Scope


### Hoisting


### Closure - think of as saving context with variables, like saving global context, but instead a function's local scope and context with its variables, allowing saving and incrementing

#### **simple** 
1. function 
2. and access to its saved reference scope/variables from where it was originally declared, like a backpack of scope that it always brings when called outside declared context

closure over == access to its scope
ex: closure over inner scope of f1, access to scope of f1
**function**
**Access to scope where originally declared**

3. when function called outside its originally declared context/own scope, brings along its saved scope

**Called outside originally declared**

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

### Typeof


typeof 1

typeof typeof 1 

#### Result - is a string
- "Number" - string











### types and Abstract (==) vs Strict (===) equality operators


