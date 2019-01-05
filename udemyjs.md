
1. Triple add function

//   add(10)(20)(30)

function add(a) {
	return function(b) {
		return function(c) {
			return a+b+c;
		}
	}
}

This is example of currying a function

turning one function, multiple inputs (a,b,c)   =>      f(a)(b)(c)
to sequence/multiple function, one input each

function, types of functions:

  - IIFE
  - curried
  - expression
  - declaration


2. 
a. What is an IIFE and why are they used?
b. Code out an IIFE that functions properly

IIFE => immediately invoked function expression

They execute right away, used to prevent polluting global scope, function does not take up variable

(function(){ console.log('s') }())


3. what will be outputted when click on number 5?

function createButtons() {
   for (var i = 1; i <= 5; i++) {
     var body = document.getElementsByTagName("BODY")[0];
     var button = document.createElement("BUTTON");
     button.innerHTML = 'Button ' + i;
     button.onclick = function() {
          alert('This is button ' + i);
     }
     body.appendChild(button);
   }
}
 
createButtons();

6 will be outputted because this is asynchronous code. when i is called, it will the i that was last updated, i.e. i =6, because to break the conditional, i++ will take i from 5 to 6.

This i is what will be gotten from event listener


4. What is a closure?
Give example of closure

Closure refers to a function and its reference to its declared scope and the variables it has access to

function a() {
	let count = 0;
	return function() {
		count++;
		return count;
	}
}

var x = a();
x();

5. What is the "this" keyword and how is it used?

"this" refers to an object that is decided depending on how function is declared

four rules, in precedence
 - new binding, refers to object created by new

 - 
 -
 -


6. What is hoisting?

It is behavior of javascript, to process function and var (not let or const) before any other code, so they are available before any other code

function is hoisted before var, overwrites var

var overwrites, so if var and var same, var 1 overwrites

opposite for function, function2, declared later, overwrites


7. var myCar = {
    color: "Blue",
    logColor: function() {
        var self = this;
        console.log("In logColor - this.color: " + this.color);
        console.log("In logColor - self.color: " + self.color);
        (function() {
            console.log("In IIFE - this.color: " + this.color);
            console.log("In IIFE - self.color: " + self.color);
        })();
    }
};
 
myCar.logColor();

This will output

"Blue"
"Blue"
undefined
"Blue"

8. == vs ===?

== is the abstract equality, it coerces the two values if different types then compares values

=== string equality, always false if different type. Only compare if same type, then check value

== all coerce to either number, string, or boolean

if boolean, coerce to num

if str, coerce to num


9. 
var num = 50;
 
function logNumber() {
    console.log(num);
    var num = 100;
}
 
logNumber();

undefined because we always have to check scope, own scope first to see if var declared, then go up

so var num =100 inside, and var num is hoisted

10. What does "use strict do"? What are its benefits?

It makes error handling more strict

- Catch errors such as undeclared var, ref error instead of declaring global var
- prevent parameter function same name, must be unique
function a(a,a,c) {} error, b/c a is defined twice


11. Curry this function
function getProduct(num1, num2) {
  return num1 * num2;
}

function getProduct(num1) {
  return function(num2) {
		return num1 * num2;
	}
}

getProduct(5)(4);


We curry because it allows saving funciton (a) with one parameter and easy changing of 2nd parameter

12. Build a counter function


function a() {
	let count = 0;
	return function b() {
		count++;
		console.log(count);
	}
}


14. What is value of y and x?

(function() {
  var x = y = 200;
})();
 
console.log('y: ', y);
console.log('x: ', x);

200
ref error

15. Describe call() and apply()

Both explicity set "this" in a function and call the f

Difference, call takes parametres as comma, while apply takes in array of parameters

fucntion.apply(this, [])
function.call(this, a,b,c)

16. What does this print out?

const list1 = [1, 2, 3, 4, 5];
const list2 = list1;
 
list1.push(6, 7, 8);
 
console.log(list2);


[1,2,3,4,5,6,7,8];


17. write the function
function getTotal() {
    // build out code...
}
 
getTotal(10, 20);
getTotal(10)(20);

function getTotal(a,b) {
    if (arguments.length == 1) {
		return function(c) {
			return a+c;
		}
	}
	else if (arguments.length == 2) {
		return a+b;
	}
}
 
getTotal(10, 20);
getTotal(10)(20);

18. 
// TASK:
// 1. Describe what JSON format is.
// 2. Delete the data types not permitted in JSON.
// 3. Replace placeholder-text with the corresponding data type,
//    properly formatted as JSON.
 
const myJsonObj = {
  myString: [some string],
  myNumber: [some number],
  myNull: [null],
  myBoolean: [false],
  myUndefined: [undefined],
  myArray: [some array],
  myFunction: [some function],
  myObject: [some object]
};



JSON format is javascript object notation, a format for transferring data

api to client, etc

It is used because easy to parse, understand

What data types allowed?

- all types EXCEPT functions and undefined
  undefined is better omitted if none
  functions not allowed because JSON is ONLY data, not for invoking functions
  
  not allowed to manipulate data

- all properties are in double quotes, not single   "property", 
  strings must also be double quotes only
  objects must also be in JSON notation


const myJsonObj = {
  "myString": "some string",
  "myNumber": 5,
  "myNull": null,
  "myBoolean": false,  
  "myArray": [20,30,"orange"],
  "myObject": {
		"name": "sam",
		"age": 5
	}
};



19. What order are numbers logged in?
function logNumbers() {
  console.log(1); 
  setTimeout(function(){console.log(2)}, 1000); 
  setTimeout(function(){console.log(3)}, 0); 
  console.log(4);
}
 
logNumbers();

1,4,3,2



20. What are the three ways of creating an object?


  1. Object literal
  2. new Object()
  3. new constructor function 


21. What is logged out?

console.log(typeof null);
console.log(typeof undefined);
console.log(typeof {});
console.log(typeof []);
 
"object"
"undefined"
"object"
"object"

22. Describe the bind method

It explicitly sets "this" to given object and returns a copy of the function
Also takes in parameters and saves them

f.bind(obj)

23. What is logged out?
const user1 = {
  name: 'Jordan',
  age: 28,
};
 
const user2 = {
  name: 'Jordan',
  age: 28,
};
 
console.log(user1 == user2);
console.log(user1 === user2);

false
false



24. What is output?

var arr1 = [];
var arr2 = new Array(50);
var arr3 = new Array(1, 2, "three", 4, "five");
var arr4 = new Array([1, 2, 3, 4, 5]);
 
console.log('arr1: ', arr1);
console.log('arr2: ', arr2);
console.log('arr3: ', arr3);
console.log('arr4: ', arr4);

[]
[ <50 empty items> ]
[1,2,"three",4,"five"]
[[1,2,3,4,5]]


- Array consturctor if one number, length
- else, one ele, will be one ele array

  new Array('a')   =>  ['a']


25. What will be outputted? .indexOf()

console.log([10, 20, 30, 40, 50].indexOf(30));
console.log([{ name: 'Pam' }, { name: 'Kent' }].indexOf({ name: 'Kent' }));
console.log('hello world'.indexOf('o'));
console.log([[1], [2], [3], [4]].indexOf([2]));

2
-1
4
-1

26. what will be logged? floating numbers and equivalents

console.log(900.9 === 300.3 * 3); 

false

b/c floating numbers, such as .3, .6, can't be represented accurately, like 1/3, 2/3

will be rounded to a different number



27. What will be logged out?

var string1 = 'Tampa';
var string2 = string1;
string1 = 'Venice';
 
console.log(string2);
 
 
////////////////////////////////
 
 
var person1 = {
  name: 'Alex',
  age: 30
};
 
var person2 = person1;
 
person2.name = 'Kyle';
 
console.log(person1);


'Tampa'

{
	name: "Kyle",
	age: 30 
}


28. What will be logged?

const data1 = 'Jordan Smith';
 
const data2 = [].filter.call(data1, function(elem, index) {
  return index > 6;
});
 
console.log(data2);

//////

["S", "m", "i", "t", "h"]

https://stackoverflow.com/questions/32922445/js-array-prototype-filter-call-can-someone-explain-me-how-this-piece-of-code

or udemy course, explanation, traub


29. What will be logged?

const a = {};
const b = { name: 'b' };
const c = { name: 'c' };
 
a[b] = 200;
a[c] = 400;
 
console.log(a[b]);


//////

400 will be logged b/c a[c] overwrites a[b], same key


30. What will be logged?

var x = 10;
 
function y() {
    x = 100;
    return;
    function x() {}
}
 
y();
 
console.log(x);

////////

10, because of hoisting


hoisting -
  1. var
    first var overwrites other var, no diff
  2. function, is equivalent to var, scoped to function or global

     the newest f, f2 overwrites f1 if share name



31. What will be logged out?

const account1 = {
  name: 'Jen',
  totalAmount: 5000,
  deductAmount: function(amount) {
    this.totalAmount -= amount;
    return 'Amount in account: ' + this.totalAmount;
  },
};
 
const account2 = {
  name: 'James',
  totalAmount: 8000,
};
 
const withdrawFromAccount = function(amount) {
  return account1.deductAmount.bind(account2, amount);
};
 
console.log(withdrawFromAccount(500)());
console.log(withdrawFromAccount(200)());


///////

'Amount in account: 7500'
'Amount in account: 7300'



https://www.reddit.com/r/reactjs/comments/9q34kx/todays_javascript_react_developer_interview/


32. What will be logged?

a = 'abc';
function f() {
    'use strict';
    a = 'xyz';
    foo = 'bar';
}
f();

#### Output

no error for a, because a does have global var, or var above scope
error, because foo is not declared



33. What is __proto__ and what does it points to everytime?

function foo(someParameter){
 // which has some method
 return undefined;
}

var b = foo(12345);

//foo's prototype;


#### Output

34. 

Object.__proto__ = null;

Object.create();

var descriptor = Object.create(null);

#### Output


35. 

var length = 10;
function fn() {
    console.log(this.length);
}

var obj = {
    length: 5,
    method: function(fn) {
        fn();
        arguments[0]();
    }
};

obj.method(fn, 1);

#### Output

10
2    // because arguments[0](), is like calling arguments.f(), on arguments

obj.f(), points to obj
array[0](), points to array



36. 

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


#### Output

1
undefined
2

catch is weird, because catch(x) will be declared, but the value won't be accessible outside catch

inside, console.log(x) => 1

but outside

console.log(x) => undefined





37. What is happening on this code?

var x = 1, y =2;

#### Output

two variables are being declared, sharing one var with comma

var x = 1;
var y = 2;



38. What will be the output?

fn1();
fn2();

var fn1 = (function() { console.log(“Inside fn1”); })();
(function fn2() { console.log(“Inside fn2”) })();


#### Output

type error, because fn1 hoisted, but expression not processed
so undefined() == fn1()

below, fn2(), is referenceerror, because fn2 is not declared yet
