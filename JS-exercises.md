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





### TopTal Questions

https://www.toptal.com/javascript/interview-questions

1. What will the following code output to the console:

console.log((function f(n){return ((n > 1) ? n * f(n-1) : n)})(10));
Explain your answer.

#### Soln	

2. Consider the code snippet below. What will the console output be and why?

(function(x) {
    return (function(y) {
        console.log(x);
    })(2)
})(1);

#### Soln

3. Create a function that, given a DOM Element on the page, will visit the element itself and all of its descendents (not just its immediate children). For each element visited, the function should pass that element to a provided callback function.

The arguments to the function should be:

a DOM element
a callback function (that takes a DOM element as its argument)

#### Soln


4. What will be the output of this code?

var x = 21;
var girl = function () {
    console.log(x);
    var x = 20;
};
girl ();

#### Soln

undefined, b/c var x gets hoisted


always look for var inside own scope before anything else.
This will show whether hosited, undefined, etc


5. for (let i = 0; i < 5; i++) {
  setTimeout(function() { console.log(i); }, i * 1000 );
}
What will this code print?


#### Soln

6. What will be the output of the following code:

for (var i = 0; i < 5; i++) {
	setTimeout(function() { console.log(i); }, i * 1000 );
}
Explain your answer. How could the use of closures help here?


#### Soln

7. The following recursive code will cause a stack overflow if the array list is too large. How can you fix this and still retain the recursive pattern?

var list = readHugeList();

var nextListItem = function() {
    var item = list.pop();

    if (item) {
        // process the list item...
        nextListItem();
    }
};

#### Soln



8. What will the code below output to the console and why?

var arr1 = "john".split('');
var arr2 = arr1.reverse();
var arr3 = "jones".split('');
arr2.push(arr3);
console.log("array 1: length=" + arr1.length + " last=" + arr1.slice(-1));
console.log("array 2: length=" + arr2.length + " last=" + arr2.slice(-1));

#### Soln

This is a test of mutable array methods




9. Write a simple function (less than 160 characters) that returns a boolean indicating whether or not a string is a palindrome.


#### Soln

10. What is the output out of the following code? Explain your answer.

var a={},
    b={key:'b'},
    c={key:'c'};

a[b]=123;
a[c]=456;

console.log(a[b]);

#### Soln


Javascript object keys must be strings or symbosl


object[]   backet notation will coerce input to string


So object[{key:'b'}]
 and object[{key:'c'}] both become object["[object Object]"]


 and thus, any object keys become same key "[object Object]" due to conversion



11. In what order will the numbers 1-4 be logged to the console when the code below is executed? Why?

(function() {
    console.log(1); 
    setTimeout(function(){console.log(2)}, 1000); 
    setTimeout(function(){console.log(3)}, 0); 
    console.log(4);
})();

#### Soln

1
4
3
2

Because setTimeout, 0 is minimum time to execution, not guarantee, and callbackqueue, event loop will wait until call stack is clear, i.e. until after all the console.logs are finished

This leaves setTimeout 0 then setTimeout 1000


12. Consider the following code. What will the output be, and why?

(function () {
    try {
        throw new Error();
    } catch (x) {
        var x = 1, y = 2;
        console.log(x);
    }
    console.log(x);
    console.log(y);
})();

#### Soln



### Reddit Questions
https://www.reddit.com/r/webdev/comments/3f7q3q/been_interviewing_with_a_lot_of_tech_startups_as/


1. function doubleInteger(i) {
    //your code here
    
   }   


#### Soln

function doubleInteger(i) {
    return i*2;//*
    
}   


2. function isNumberEven(i) {
    // i will be an integer. Return true if it's even, and false if it isn't.
}

#### Soln

function isNumberEven(i) {
	return i%2 == 0;
}


3. function getFileExtension(i) {
    
    // i will be a string, but it may not have a file extension.
    // return the file extension (with no period) if it has one, otherwise false
    
}

#### Soln

function getFileExtension(i) {
    
   if (i.includes(".")) {
   var str = i.split(".");
   return str[1];
 
   } else {
   	return false;
   }
}


4. What will be printed on the console? Why?


(function() {
   var a = b = 5;
})();
console.log(b);


#### Soln

console.log(b);   -> 5

b/c var a = b = 5;

   same as 


   b = 5;
   var a = b;

b = 5 is global scoped b/c no strict or var, so it is accessible


5. Define a repeatify function on the String object. The function accepts an integer that specifies how many times the string has to be repeated. The function returns the string repeated the number of times specified.

console.log('hello'.repeatify(3));
//Should print hellohellohello.


#### Soln

String.prototype.repeatify = function(n) {
   

   var totalString = "";
   for (let i = 0; i<n; i++) {
   totalString = totalString.concat(this); 
   
   }
   return totalString;
}


6. What will log out here?	

function test() {
   console.log(a); 
   console.log(foo());
    
   var a = 1;
   function foo() {
   return 2;
   }
}
test();


#### Soln
undefined // b/c of hoisting
2


7. What will log out here?

var fullname = 'John Doe';
var obj = {
   fullname: 'Colin Ihrig',
   prop: {
      fullname: 'Aurelio De Rosa',
      getFullname: function() {
         return this.fullname;
      }
   }
};

console.log(obj.prop.getFullname()); 
 
var test = obj.prop.getFullname; 
 
console.log(test()); 

#### Soln

'Aurelio De Rosa'    b/c obj1.obj2.f()  points to first obj to left
'John Doe'      b.c var x = obj.f   x()    binds this to global


8. Fix the previous question’s issue so that the last console.log() prints Aurelio De Rosa.

var fullname = 'John Doe';
var obj = {
   fullname: 'Colin Ihrig',
   prop: {
      fullname: 'Aurelio De Rosa',
      getFullname: function() {
         return this.fullname;
      }
   }
};

console.log(obj.prop.getFullname()); 
 
var test = obj.prop.getFullname; 
 
console.log(test()); 

#### Soln

var fullname = 'Aurelio De Rosa';


9. The following recursive code will cause a stack overflow if the array list is too large. How can you fix this and still retain the recursive pattern?

var list = readHugeList();

var nextListItem = function() {
    var item = list.pop();

    if (item) {
        // process the list item...
        nextListItem();
    }
};

#### Soln


var list = readHugeList();

var nextListItem = function() {
    var item = list.pop();

    if (item) {
        // process the list item...
        setTimeout(nextListItem,0);
    }
};


Placing setTimeout in recursive function prevents stack overflow because it lets event loop handle recursion

event loop waits for call stack to clear before execution, so we won't have stack overflow
https://stackoverflow.com/questions/31250026/stack-overflow-while-processing-large-array-in-recursive-function

The stack overflow is eliminated because the event loop handles the recursion, not the call stack. When nextListItem runs, if item is not null, the timeout function (nextListItem) is pushed to the event queue and the function exits, thereby leaving the call stack clear. When the event queue runs its timed-out event, the next item is processed and a timer is set to again invoke nextListItem. Accordingly, the method is processed from start to finish without a direct recursive call, so the call stack remains clear, regardless of the number of iterations.



10. What will alert out here:

var a = 'value';

(function() {
  alert(a); 
  var a = 'value2';
})();

#### Soln

undefined     // b/c var a in iife is hoisted but not yet assigned


11. The following code will output "my name is rex, Woof!" and then "my name is, Woof!" one second later, fix it so prints correctly the second time

var Dog = function (name) {
  this.name = name;
};

Dog.prototype.bark = function () {
  console.log('my name is '+ this.name + ', Woof!');
}

var rex = new Dog('rex');

rex.bark();

setTimeout(rex.bark, 1000);


#### Soln

Problem is setTimeout unbinds this, because puts parameter f = rex.bark

and calls f like f(), leading to unbinding. To fix, we need to find way to call rex.bark as rex.bark


setTimeout(function() { rex.bark(); }, 1000)


12. The following code outputs 100, a hundred times, fix it so it outputs every number with a 100ms delay between each

for (var i = 0; i < 100; ++i) {
  setTimeout(function() {
    console.log(i);
  }, 100);
} 

#### Soln

for (var i = 0; i < 100; ++i) {
  (function(i){
  setTimeout(function() {
    console.log(i);
  }, i*100);})(i);
} 


13. The following code is outputting the array but it's filled with every number, we just want the even numbers, what's gone wrong?

var evenNumbers = []

var findEvenNumbers = function (i) {
  if (i % 2 === 0)
    console.log(i, 'is an even number, adding to array!');
    evenNumbers.push(i);
}

for (var i = 0; i < 10; i++) {
  findEvenNumbers(i);
}

console.log(evenNumbers);
//outputs:
//0 "is an even number, adding to array!"
//2 "is an even number, adding to array!"
//4 "is an even number, adding to array!"
//6 "is an even number, adding to array!"
//8 "is an even number, adding to array!"
//[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

#### Soln

Problem was if statement did no have brackets, so the conditions weren't applied to the nonbracketed code

if (i % 2 === 0)
    console.log(i, 'is an even number, adding to array!');
    evenNumbers.push(i);


if (i % 2 === 0) {
    console.log(i, 'is an even number, adding to array!');
    evenNumbers.push(i);
}



14. The following is outputting 0, but if 42 = 16 and 22 = 4 then the result should be 12

var square = function (number) {
  result = number * number;
  return result;
}

result = square(4);
result2 = square(2);
difference = result - result2;

console.log(difference);

#### Soln

Problem is lack of declaration in square function, and global scoping with shared names with result

This leads to result being reset each time square is called, so difference is always zero
because result2 is new result

result is same as new result b/c of reset

x-x= 0



15. Write a function that when passed an array of numbers it gives you the max difference between the largest and smallest number ONLY if the small number is in front of the large number, not behind it, so for example: [3,4,8,1] = 5, notice how the biggest difference is between 8 and 1, but because the 1 is after the 8 in the array it shouldn't count, so really the biggest gap is the 3 and the 8.



#### Soln



16. fizzbuzz 

Write a program that prints the numbers from 1 to 100. But for multiples of three print “Fizz” instead of the number and for the multiples of five print “Buzz”. For numbers which are multiples of both three and five print “FizzBuzz”.

#### Soln

for (let i = 1; i<=100; i++) {
	
	if (i%5 == 0 && i%3 == 0) {
		console.log('FizzBuzz');
	} else if (i%5 == 0) {
        console.log('Buzz')
	} else if (i%3 == 0) {
        console.log('Fizz')
	} else {
		console.log(i);
	}
}


17. 
function longestString(i) {

    // i will be an array.
    // return the longest string in the array

    var longestLength = 0;
    var returnString = "";

    i.forEach(function(item) {
        if ((typeof item === 'string') && (item.length > longestLength)) {
            longestLength = item.length;
            returnString = item;
        }
    });

    return returnString;
}

#### Soln

function longestString(i) {

    // i will be an array.
    // return the longest string in the array

    var longestLength = 0;
    var returnString = "";

    for (let q = 0; q<i.length; q++) {
    	if (typeof i[q] == "string" && i[q].length > longestLength) {
    		longestLength = i[q].length;
    		returnString = i[q];
    	}
    }
    return returnString;
}


#### Recursion:


1. Find sum of arrays, including array of array


function arraySum(i) {

    // i will be an array, containing integers, strings and/or arrays like itself.
    // Sum all the integers you find, anywhere in the nest of arrays.

    var sum = 0;
    function sumArray(i) {
        i.forEach(function(item) {
            if (typeof item === 'number') {
                sum = sum + item;
            }
            // Remember that everything is an object in JavaScript!!!
            if (item instanceof Array) {
                sum = sum + sumArray(item);
            }
        });
    return sum;
    }

    return sumArray(i);
}


#### Soln


function arraySum(i) {

    // i will be an array, containing integers, strings and/or arrays like itself.
    // Sum all the integers you find, anywhere in the nest of arrays.
	let sum = 0;

	for (let q = 0; q<i.length; q++) {
		if (i[q] !== null && i[q].constructor == Array) {
			sum += arraySum(i[q]);
		} else if(typeof i[q] == "number") {
			sum += i[q];
		}
	}
	return sum;
}

2. Factorial


#### Soln

	function getFactorial(n) {
		if (typeof n !== "number" || n<0 || isNaN(n) == true) {
			return false;
		}
		if (n == 1 || n == 0) {
		    return 1;
	    }
	    else {
			return n*getFactorial(n-1);
		}
	}


3. Reverse a String

#### Soln

	function reverseStr(str) {
		if (typeof str !== "string") return;
		if (str.length == 0) return "";
		else {
			return reverseStr(str.slice(1)) + str[0];
		}
	}






4. Pascal's Triangle


	function getPascal(n) {
		if (n<=0 || typeof n !== "number") {
			return "Please enter number greater or equal to one";
		}
		if (n == 1) {
			return [[1]];
		}
		var totalSeqs = getPascal(n-1);
		var prevSeq = totalSeqs[totalSeqs.length-1];
		var newSeq = [];
		for (let i = 0; i < prevSeq.length-1; i++) {
			newSeq.push(prevSeq[i] + prevSeq[i+1]);
		}	
		newSeq.push(1);
		newSeq.unshift(1);
		totalSeqs.push(newSeq);
		return totalSeqs;
	}


#### Soln


5. Fibonacci Number

Fibonacci number is the number in sequence that is the sum of the previous two numbers

ex: 0 1 1 2 3 5 8 13 21 etc

start from 0 and 1

[0,1]  counts as number 1
  1    counters as number 2
  2    counters as number 3
  3    counters as number 4
  5    counters as number 5


#### Soln

Attempt 1:  problem was that return array.push gives back new length, NOT the array

function fibonacciNum(n) {
	if (typeof n !== "number" || n<0) return;
	if (n == 1 || n == 0) {
		return [0,1];
	} else {
		return fibonacciNum(n-1).push(
			fibonacciNum(n-1)[fibonacciNum(n-1).length-2] + fibonacciNum(n-1)[fibonacciNum(n-1).length-1]);
	}
	

}

Correct: 

	1. Get Array of sequence
	2. return last number on sequence

function getFibonacciSeq(n) {
	if (typeof n !== "number" || n<0) return;
	if (n == 1 || n == 0) {
		return [0,1];
	} else {
		var seq = getFibonacciSeq(n-1);
		seq.push(seq[seq.length-1] + seq[seq.length-2]);
	}
	return seq;

}

function getFibonnaciNum(n) {
	var array = getFibonacciSeq(n);
	return array[array.length-1];
}



6. Count the number of reoccurring instances of a digit in a number (E.g. 79092342 has two 9s). For bonus points, create a generator function using closures to create a recursive function using the value passed.


#### Soln

7. Using recursion, go through a string and remove characters that occur more than once. E.g. passing in "Troll" should return "trol". Passing in "abracadabra" should return "abrcd".


#### Soln