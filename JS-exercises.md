# JS Exercises

1. Consider the two functions below. Will they both return the same thing? Why or why not?

function foo1()
{
  return {
      bar: "hello"
  };
}

function foo2()
{
  return
  {
      bar: "hello"
  };
}


### soln

return;    if skipped line in return, parser places semicolon on return;
	

nothing is returned, therefore, undefined

if (return 
	{
	a:1
	})
object is returned normally

https://www.toptal.com/javascript/interview-questions



2. Make this work: duplicate([1,2,3,4,5]); // [1,2,3,4,5,1,2,3,4,5]

### soln

function duplicateArray(array) {
	return array.concat(array);
}



3. Explain why the following doesn't work as an IIFE: function foo(){ }();. What needs to be changed to properly make it an IIFE?


simple function?
most function require extra to input var

### soln

IIFE is immediately invoked function expression

it is run right after creation and is gone

	1. parser reads function foo(){}(); as function definition and set of parentheses
	   
	Only function expression is IIFE, NOT definition
		
	function foo(){};
	();, so error
		
	2. There are Two acceptable IIFE formats
		
		- (function foo(){}()), the wrapping parentheses converts defintiion to expression, puts into one unit
		- (function foo(){})(); 



4. Get file extension (.doc, .html, etc)

var file1 = "50.xsl";
var file2 = "30.doc";
getFileExtension(file1); //returns xsl
getFileExtension(file2); //returns doc


### soln

function getFileExtension(filename) {
    return filename.split('.').pop();
}

The split creates an array with the file extension in position one
The pop() removes that file extension from array and returns it.


5. What will be printed on the console? Why?
(function() {
   var a = b = 5;

   console.log(a,b);
})();
console.log(a,b);

### soln

var a = b = 5; 

equivalent to

b=5;
var a = b;

From right to left, break off equation into pieces.

a = b = c = d = e = null;

e=null;
d=e;
c=d;
b=c;
a=b;
all equal null


1st console is 5, 5 because a is declared within the IIFE
2nd console is undefined, 5 because no a, while b was global variable in IIFE



https://stackoverflow.com/questions/21215418/in-javascript-what-do-multiple-equal-signs-mean


6. The following code outputs 100, a hundred times, fix it so it outputs every number with a 100ms delay between each


for (var i = 0; i < 100; ++i) {
  setTimeout(function() {
    console.log(i);
  }, 100);
} 

### soln

Problem with for loop and settimeout

settimeout is executed immediately in for loop, meaning it runs ALL the settimeouts as soon as possible

The delay between each iteration between settimeouts is nowhere near 100ms

ex:
sto1, sto2  -- 100ms -- >    c.l1, c.l2 all together


Easy way -- setInterval, and update

function counter() {
	var count = 0;
	setInterval(() => {
		console.log(count);
		count+=2;
	}, 200)
}

counter();



Hard way -- *no* setInterval, use setTimeout

function counter() {
	var count = 0;

	setTimeout(() => {
		console.log(count);
		count++;
		setTimeout(counter,200);
	}, 200)
}

counter();

function shama() {
	var iter = 0;
	function counter() {
 	   console.log(iter);
 	   iter++;
 	   setTimeout(counter, 300);
	}
	counter();
}
shama();


closure forms

demonstrating closure involves executing inner f/f2


1. outer - f or IIFE

2. inner - f(), IIFE (good for one time, setTimeout) /// return f (good for counter)

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