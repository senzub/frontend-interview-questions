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


closure and hide count, setInterval keeps var alive, and updates

1. 
(function counter() {
	var count = 0;
	var timer = setInterval(() => {
		console.log(count);

		if (count == 10) {
			clearInterval(timer);
		}		
		count++;
	}, 200)
})();



Hard way -- *no* setInterval, use setTimeout



This does NOT work because it resets the var. we must wrap/hide in function to save variable while calling setTimeout
function counter() {
	var count = 0;

	setTimeout(() => {
		console.log(count);
		count++;
		setTimeout(counter,200);
	}, 200)
}

counter();

This works

1. recursive setTimeout, time difference 1000

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

2. for loop, need time difference i*1000

for (let i=0; i <= 10; i++) {
	setTimeout((i) => {
		console.log(i);
    }, i*1000, i)

}

for (var i=0; i <= 10; i++) {
	setTimeout((i) => {
		console.log(i);
    }, i*1000, i)

}

var becomes global, let is scoped to for loop


   Two key problems:
   - i*1000, the timing can't be simply 1000, because all the setTimeouts    will be executed after 1000 seconds
   i.e The difference between setTimeouts must be 1000 seconds, but now the difference will be the time to execute one iteration, which is <10ms
   - Saving the i value, so that it is proper number. If execute now, and i is not saved, we get i = maximum or minimum because all iterations have been executed




