
############################
## Basic Algorithm Scripting
############################



1. Days of the week, write a function that, given a String S representing the day of the week and an integer K (between 0 and 500), returns the day of the week that is K days later

ex: S= "Web" and K=2 , return "Fri"

let days = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"];


#### Soln

% can be used to measure cycle
get remainder after number of cycles

function getDay(s,k) {
	let days = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"];	
	let shift = k%7;
	let currentInd = days.indexOf(s);
	let newInd = (shift+currentInd)%7;
	return days[newInd];
}

%7, cycle of 7
%5, cycle of 5


2. Largest number of each array, in array of arrays, return new array: Return Largest Numbers in Arrays

Return an array consisting of the largest number from each provided sub-array. For simplicity, the provided array will contain exactly 4 sub-arrays.

Remember, you can iterate through an array with a simple for loop, and access each member with array syntax arr[i].

	largestOfFour([[4, 5, 1, 3], [13, 27, 18, 26], [32, 35, 37, 39], [1000, 1001, 857, 1]]) should return an array.
	largestOfFour([[13, 27, 18, 26], [4, 5, 1, 3], [32, 35, 37, 39], [1000, 1001, 857, 1]]) should return [27, 5, 39, 1001].
	largestOfFour([[4, 9, 1, 3], [13, 35, 18, 26], [32, 35, 97, 39], [1000000, 1001, 857, 1]]) should return [9, 35, 97, 1000000].
	largestOfFour([[17, 23, 25, 12], [25, 7, 34, 48], [4, -10, 18, 21], [-72, -3, -17, -10]]) should return [25, 48, 21, -3].

#### Soln

function largestOfFour(arr) {
	// You can do this!
	let totalArray = [];
	for (let i = 0; i < arr.length; i++) {
		let largest = arr[i][0];
		for (let j = 0; j < arr[i].length; j++) {
			if (arr[i][j] > largest) {
				largest = arr[i][j];
			}
		}
		totalArray.push(largest);
	}
	return totalArray;
}




3. Check whether string ends with given substring: confirm the ending

Check if a string (first argument, str) ends with the given target string (second argument, target).

This challenge can be solved with the .endsWith() method, which was introduced in ES2015. But for the purpose of this challenge, we would like you to use one of the JavaScript substring methods instead.

	confirmEnding("Bastian", "n") should return true.
	confirmEnding("Congratulation", "on") should return true.
	confirmEnding("Connor", "n") should return false.
	confirmEnding("Walking on water and developing software from a specification are easy if both are frozen", "specification") should return false.
	confirmEnding("He has to give me a new name", "name") should return true.
	confirmEnding("Open sesame", "same") should return true.
	confirmEnding("Open sesame", "pen") should return false.
	confirmEnding("Open sesame", "game") should return false.
	confirmEnding("If you want to save our world, you must hurry. We dont know how much longer we can withstand the nothing", "mountain") should return false.
	confirmEnding("Abstraction", "action") should return true.
	Do not use the built-in method .endsWith() to solve the challenge.


#### Soln

slice to check if 





4. Repeat a string: Repeat a given string str (first argument) for num times (second argument). Return an empty string if num is not a positive number


#### Soln

key is two different parts

newstr and str

newStr = newStr.concat(str)

b/c concat is nonmut, need to save
can't concat(newStr), else it will exponentially grow



5. Cut string to match length: Truncate a string
Truncate a string (first argument) if it is longer than the given maximum string length (second argument). Return the truncated string with a ... ending.

	truncateString("A-tisket a-tasket A green and yellow basket", 8) should return "A-tisket...".
	truncateString("Peter Piper picked a peck of pickled peppers", 11) should return "Peter Piper...".
	truncateString("A-tisket a-tasket A green and yellow basket", "A-tisket a-tasket A green and yellow basket".length) should return "A-tisket a-tasket A green and yellow basket".
	truncateString("A-tisket a-tasket A green and yellow basket", "A-tisket a-tasket A green and yellow basket".length + 2) should return "A-tisket a-tasket A green and yellow basket".
	truncateString("A-", 1) should return "A...".
	truncateString("Absolutely Longer", 2) should return "Ab...".

#### Soln


function truncateString(str, num) {
  let truncatedStr = "";
  if (str.length > num) {
    truncatedStr = str.slice(0,num);
    return truncatedStr + "...";
  } else {
    return str;
  }
  
}

truncateString("A-tisket a-tasket A green and yellow basket", 8);



6. Title Case a sentence

Return the provided string with the first letter of each word capitalized. Make sure the rest of the word is in lower case.

For the purpose of this exercise, you should also capitalize connecting words like "the" and "of".

	titleCase("I'm a little tea pot") should return a string.
	titleCase("I'm a little tea pot") should return I'm A Little Tea Pot.
	titleCase("sHoRt AnD sToUt") should return Short And Stout.
	titleCase("HERE IS MY HANDLE HERE IS MY SPOUT") should return Here Is My Handle Here Is My Spout.

#### Soln

function titleCase(str) {
	str = str.toLowerCase();
	let words = str.split(" ");
	let titledWords = [];
	for (let i = 0; i < words.length; i++) {
		let capitalizedWord = words[i].charAt(0).toUpperCase() + words[i].slice(1);
		titledWords.push(capitalizedWord);
	}
	return titledWords.join(" ");
}

titleCase("I'm a little tea pot");





7. Insert, flatten array, only at specific index, combining arrays: Slice and Splice

You are given two arrays and an index.

Use the array methods slice and splice to copy each element of the first array into the second array, in order.

Begin inserting elements at index n of the second array.

Return the resulting array. The input arrays should remain the same after the function runs.

	frankenSplice([1, 2, 3], [4, 5], 1) should return [4, 1, 2, 3, 5].
	frankenSplice([1, 2], ["a", "b"], 1) should return ["a", 1, 2, "b"].
	frankenSplice(["claw", "tentacle"], ["head", "shoulders", "knees", "toes"], 2) should return ["head", "shoulders", "claw", "tentacle", "knees", "toes"].
	All elements from the first array should be added to the second array in their original order.
	The first array should remain the same after the function runs.
	The second array should remain the same after the function runs.

#### Soln

function frankenSplice(arr1, arr2, n) {
  // It's alive. It's alive!
  let newArr = arr2.slice();

  newArr.splice(n,0,...arr1);
  return totalArray;
}

frankenSplice([1, 2, 3], [4, 5, 6], 1);





8. The sorted index in which element would be in array would be if it were sorted


#### Soln


9. Split array into many arrays: chunky monkey

Write a function that splits an array (first argument) into groups the length of size (second argument) and returns them as a two-dimensional array.

[1,2,3] => [[1,2],[3]]

chunkArrayInGroups([0, 1, 2, 3, 4, 5, 6, 7, 8], 4) should return [[0, 1, 2, 3], [4, 5, 6, 7], [8]]

	chunkArrayInGroups(["a", "b", "c", "d"], 2) should return [["a", "b"], ["c", "d"]].
	chunkArrayInGroups([0, 1, 2, 3, 4, 5], 3) should return [[0, 1, 2], [3, 4, 5]].
	chunkArrayInGroups([0, 1, 2, 3, 4, 5], 2) should return [[0, 1], [2, 3], [4, 5]].
	chunkArrayInGroups([0, 1, 2, 3, 4, 5], 4) should return [[0, 1, 2, 3], [4, 5]].
	chunkArrayInGroups([0, 1, 2, 3, 4, 5, 6], 3) should return [[0, 1, 2], [3, 4, 5], [6]].
	chunkArrayInGroups([0, 1, 2, 3, 4, 5, 6, 7, 8], 4) should return [[0, 1, 2, 3], [4, 5, 6, 7], [8]].
	chunkArrayInGroups([0, 1, 2, 3, 4, 5, 6, 7, 8], 2) should return [[0, 1], [2, 3], [4, 5], [6, 7], [8]].


https://stackoverflow.com/questions/7273668/how-to-split-a-long-array-into-smaller-arrays-with-javascript

#### Soln

Ways to split arrays:
 1. splice
 2. slice


function chunkArrayInGroups(arr,length) {
	let newArr = [];
	while (arr.length >= length) {
		newArr.push(arr.splice(0,length));
	}
	if (arr.length > 0) {
		newArr.push(arr);
	}
	return newArr;
}

chunkArrayInGroups([0, 1, 2, 3, 4, 5, 6, 7, 8], 4)


10. Falsy bouncer: Remove all falsy values from an array.

Falsy values in JavaScript are false, null, 0, "", undefined, and NaN.

Hint: Try converting each value to a Boolean.

	bouncer([7, "ate", "", false, 9]) should return [7, "ate", 9].
	bouncer(["a", "b", "c"]) should return ["a", "b", "c"].
	bouncer([false, null, 0, NaN, undefined, ""]) should return [].
	bouncer([1, null, NaN, 2, undefined]) should return [1, 2].


#### Soln

function bouncer(arr) {
  let newArr = arr.filter((ele) => {
		return ele ? true : false
	})
	return newArr;
}

bouncer([7, "ate", "", false, 9]);


11.  Mutations

Return true if the string in the first element of the array contains all of the letters of the string in the second element of the array.

For example, ["hello", "Hello"], should return true because all of the letters in the second string are present in the first, ignoring case.

The arguments ["hello", "hey"] should return false because the string "hello" does not contain a "y".

Lastly, ["Alien", "line"], should return true because all of the letters in "line" are present in "Alien".

	mutation(["hello", "hey"]) should return false.
	mutation(["hello", "Hello"]) should return true.
	mutation(["zyxwvutsrqponmlkjihgfedcba", "qrstu"]) should return true.
	mutation(["Mary", "Army"]) should return true.
	mutation(["Mary", "Aarmy"]) should return true.
	mutation(["Alien", "line"]) should return true.
	mutation(["floor", "for"]) should return true.
	mutation(["hello", "neo"]) should return false.
	mutation(["voodoo", "no"]) should return false.

i.e. checking if each char in string is in other array

#### Soln

function mutation(arr) {
	let ele1 = arr[0].toLowerCase();
	let ele2 = arr[1].toLowerCase();
	for (let i = 0; i < ele2.length; i++) {
		if (!ele1.includes(ele2.charAt(i))) {
			return false;
		}
	}
	return true;
}

mutation(["hello", "hey"]);

///////////////////////////////////////////////////////////////////////////////////////////


###################################
## Intermediate Algorithm Scripting
###################################



1. Sum all numbers between two given integers

sumAll([1, 4]) should return a number.
sumAll([1, 4]) should return 10.
sumAll([5, 10]) should return 45.


#### Soln

function sumAll(arr) {
  let sortedArr = arr.slice().sort((a,b)=>a-b);
  let largest = sortedArr[arr.length-1];
  let smallest = sortedArr[0];
  let sum = 0;
  for (let i = smallest; i<=largest; i++) {
    sum += i;
  }
  return sum;
}

sumAll([1, 4]);


2. Diff Two Arrays: Compare two arrays and return a new array with any items only found in one of the two given arrays, but not both. In other words, return the symmetric difference of the two arrays.

Remember to use Read-Search-Ask if you get stuck. Try to pair program. Write your own code.

	diffArray([1, 2, 3, 5], [1, 2, 3, 4, 5]) should return an array.
	["diorite", "andesite", "grass", "dirt", "pink wool", "dead shrub"], ["diorite", "andesite", "grass", "dirt", "dead shrub"] should return ["pink wool"].
	["diorite", "andesite", "grass", "dirt", "pink wool", "dead shrub"], ["diorite", "andesite", "grass", "dirt", "dead shrub"] should return an array with one item.
	["andesite", "grass", "dirt", "pink wool", "dead shrub"], ["diorite", "andesite", "grass", "dirt", "dead shrub"] should return ["diorite", "pink wool"].
	["andesite", "grass", "dirt", "pink wool", "dead shrub"], ["diorite", "andesite", "grass", "dirt", "dead shrub"] should return an array with two items.
	["andesite", "grass", "dirt", "dead shrub"], ["andesite", "grass", "dirt", "dead shrub"] should return [].
	["andesite", "grass", "dirt", "dead shrub"], ["andesite", "grass", "dirt", "dead shrub"] should return an empty array.
	[1, 2, 3, 5], [1, 2, 3, 4, 5] should return [4].
	[1, 2, 3, 5], [1, 2, 3, 4, 5] should return an array with one item.
	[1, "calf", 3, "piglet"], [1, "calf", 3, 4] should return ["piglet", 4].
	[1, "calf", 3, "piglet"], [1, "calf", 3, 4] should return an array with two items.
	[], ["snuffleupagus", "cookie monster", "elmo"] should return ["snuffleupagus", "cookie monster", "elmo"].
	[], ["snuffleupagus", "cookie monster", "elmo"] should return an array with three items.
	[1, "calf", 3, "piglet"], [7, "filly"] should return [1, "calf", 3, "piglet", 7, "filly"].
	[1, "calf", 3, "piglet"], [7, "filly"] should return an array with six items.

#### Soln

function diffArray(arr1, arr2) {
  let newArr = arr1.filter((ele) => {
    return !arr2.includes(ele);
  })
  let newArr2 = arr2.filter((ele) => {
    return !arr1.includes(ele);
  })

  return newArr.concat(newArr2);
}

diffArray([1, 2, 3, 5], [1, 2, 3, 4, 5]);




3. Seek and Destroy

#### Soln


4. Wherefore Art Thou

#### Soln

5. Spinal Tap Case

#### Soln


6. Pig Latin

#### Soln

7. Search and Replace

#### Soln

8. DNA Pairing

#### Soln



9. Find the missing letter in the passed letter range and return it.

If all letters are present in the range, return undefined.

	fearNotLetter("abce") should return "d".
	fearNotLetter("abcdefghjklmno") should return "i".
	fearNotLetter("stvwx") should return "u".
	fearNotLetter("bcdf") should return "e".
	fearNotLetter("abcdefghijklmnopqrstuvwxyz") should return undefined.

#### Soln

This is a comparison of two arrays by index. NOT duplicate search, which makes all comparisons



function fearNotLetter(str) {
  let alpha = "abcdefghijklmnopqrstuvwxyz";
  let startLetter = str.charAt(0);
  let startInd = alpha.indexOf(startLetter);
  let range = alpha.slice(startInd);

  for (let i = 0; i<str.length; i++) {
    if (range[i] != str[i]) {
      return range[i];
    }
  }
  return undefined;
}

fearNotLetter("abce");


10. Sorted Union 

Write a function that takes two or more arrays and returns a new array of unique values in the order of the original provided arrays.

In other words, all values present from all arrays should be included in their original order, but with no duplicates in the final array.

The unique numbers should be sorted by their original order, but the final array should not be sorted in numerical order.

Check the assertion tests for examples.

	uniteUnique([1, 3, 2], [5, 2, 1, 4], [2, 1]) should return [1, 3, 2, 5, 4].
	uniteUnique([1, 3, 2], [1, [5]], [2, [4]]) should return [1, 3, 2, [5], [4]].
	uniteUnique([1, 2, 3], [5, 2, 1]) should return [1, 2, 3, 5].
	uniteUnique([1, 2, 3], [5, 2, 1, 4], [2, 1], [6, 7, 8]) should return [1, 2, 3, 5, 4, 6, 7, 8].

#### Soln

problem is now finding unique values not between two arrays, but nested 2D arrays

function uniteUnique(arr) {
  let arg = [...arguments];
  arg = arg.reduce((accum, ele) => {
    let newEle = [];
    for (let i = 0; i < ele.length; i++) {
      if (!accum.includes(ele[i])) {
        newEle.push(ele[i]);
      }
    }
    return accum.concat(newEle);
  })
  return arg;
}

uniteUnique([1, 3, 2], [5, 2, 1, 4], [2, 1]);



11.  Convert HTML Entities

Convert the characters &, <, >, " (double quote), and ' (apostrophe), in a string to their corresponding HTML entities.

	convertHTML("Dolce & Gabbana") should return Dolce &​amp; Gabbana.
	convertHTML("Hamburgers < Pizza < Tacos") should return Hamburgers &​lt; Pizza &​lt; Tacos
	convertHTML("Sixty > twelve") should return Sixty &​gt; twelve.
	convertHTML('Stuff in "quotation marks"') should return Stuff in &​quot;quotation marks&​quot;.
	convertHTML("Schindler's List") should return Schindler&​apos;s List.
	convertHTML("<>") should return &​lt;&​gt;.
	convertHTML("abc") should return abc.

#### Soln

&    &​amp;
<    &​lt;
>    &​gt;
"    &​quot;
'    &​apos;

function convertHTML(str) {
  let newStr = str.replace(/[\"\'><&]/gi, (match)=> {
  	if (match == "&") return "&amp;";
  	else if (match == ">") return "&gt;"; 
  	else if (match == "<") return "&lt;"; 
  	else if (match == '"') return "&quot;"; 
  	else if (match == "'") return "&apos;"; 
	})
  return newStr;
}

convertHTML("Dolce & Gabbana");





12. Sum all odd fibonacci numbers

#### Soln

13. Sum All Primes

#### Soln


14. Smallest Common Multiple

#### Soln

15. Drop it:

Given the array arr, iterate through and remove each element starting from the first element (the 0 index) until the function func returns true when the iterated element is passed through it.

Then return the rest of the array once the condition is satisfied, otherwise, arr should be returned as an empty array.

	dropElements([1, 2, 3, 4], function(n) {return n >= 3;}) should return [3, 4].
	Passed
	dropElements([0, 1, 0, 1], function(n) {return n === 1;}) should return [1, 0, 1].
	Passed
	dropElements([1, 2, 3], function(n) {return n > 0;}) should return [1, 2, 3].
	Passed
	dropElements([1, 2, 3, 4], function(n) {return n > 5;}) should return [].
	Passed
	dropElements([1, 2, 3, 7, 4], function(n) {return n > 3;}) should return [7, 4].
	Passed
	dropElements([1, 2, 3, 9, 2], function(n) {return n > 2;}) should return [3, 9, 2].

#### Soln

i.e. how to delete elements from array while looping through

prob is changing in length, despite no change in total number of objects despite deleting

so, solution is to use 
  1. a variable for length
  2. use arr[0];
  3. use arr.shift() to move array down

or go from top down
https://stackoverflow.com/questions/16352546/how-to-iterate-over-an-array-and-remove-elements-in-javascript


function dropElements(arr, func) {
  let length = arr.length;
  for (let i = 0; i < length; i++) {
    if (func(arr[0])) {
      return arr;
    }
    else {
      arr.shift();
    }
  }
  return arr;
}

dropElements([1, 2, 3], function(n) {return n < 3; });


16. Steamroller

Flatten a nested array. You must account for varying levels of nesting.

	steamrollArray([[["a"]], [["b"]]]) should return ["a", "b"].
	steamrollArray([1, [2], [3, [[4]]]]) should return [1, 2, 3, 4].
	steamrollArray([1, [], [3, [[4]]]]) should return [1, 3, 4].
	steamrollArray([1, {}, [3, [[4]]]]) should return [1, {}, 3, 4].

#### Soln

function steamrollArray(arr) {
  let total = [];
  for (let i = 0; i < arr.length; i++) {
    if (typeof arr[i] == "object" && arr[i].constructor == Array) {
      total = total.concat(steamrollArray(arr[i]));
    }
    else total.push(arr[i]);
  }
  return total;
}

steamrollArray([1, [2], [3, [[4]]]]);


flattening array


17. Binary Agents

#### Soln

18. Everything be True

Check if the predicate (second argument) is truthy on all elements of a collection (first argument).

In other words, you are given an array collection of objects. The predicate pre will be an object property and you need to return true if its value is truthy. Otherwise, return false.

In JavaScript, truthy values are values that translate to true when evaluated in a Boolean context.

Remember, you can access object properties through either dot notation or [] notation.

	truthCheck([{"user": "Tinky-Winky", "sex": "male"}, {"user": "Dipsy", "sex": "male"}, {"user": "Laa-Laa", "sex": "female"}, {"user": "Po", "sex": "female"}], "sex") should return true.
	truthCheck([{"user": "Tinky-Winky", "sex": "male"}, {"user": "Dipsy"}, {"user": "Laa-Laa", "sex": "female"}, {"user": "Po", "sex": "female"}], "sex") should return false.
	truthCheck([{"user": "Tinky-Winky", "sex": "male", "age": 0}, {"user": "Dipsy", "sex": "male", "age": 3}, {"user": "Laa-Laa", "sex": "female", "age": 5}, {"user": "Po", "sex": "female", "age": 4}], "age") should return false.
	truthCheck([{"name": "Pete", "onBoat": true}, {"name": "Repeat", "onBoat": true}, {"name": "FastFoward", "onBoat": null}], "onBoat") should return false
	truthCheck([{"name": "Pete", "onBoat": true}, {"name": "Repeat", "onBoat": true, "alias": "Repete"}, {"name": "FastFoward", "onBoat": true}], "onBoat") should return true
	truthCheck([{"single": "yes"}], "single") should return true
	truthCheck([{"single": ""}, {"single": "double"}], "single") should return false
	truthCheck([{"single": "double"}, {"single": undefined}], "single") should return false
	truthCheck([{"single": "double"}, {"single": NaN}], "single") should return false

#### Soln

function truthCheck(collection, pre) {
  for (let i = 0; i < collection.length; i++) {
    if (!collection[i][pre]) {
      return false;
    }
  }
  return true;
}

truthCheck([{"user": "Tinky-Winky", "sex": "male"}, {"user": "Dipsy", "sex": "male"}, {"user": "Laa-Laa", "sex": "female"}, {"user": "Po", "sex": "female"}], "sex");


i.e. we are looping through obj and given property to see if any are falsey


19. Arguments Optional

Create a function that sums two arguments together. If only one argument is provided, then return a function that expects one argument and returns the sum.

For example, addTogether(2, 3) should return 5, and addTogether(2) should return a function.

Calling this returned function with a single argument will then return the sum:

var sumTwoAnd = addTogether(2);

sumTwoAnd(3) returns 5.

If either argument isn't a valid number, return undefined.


	addTogether(2, 3) should return 5.
	addTogether(2)(3) should return 5.
	addTogether("http://bit.ly/IqT6zt") should return undefined.
	addTogether(2, "3") should return undefined.
	addTogether(2)([3]) should return undefined.

#### Soln

This is a curried function that changes depending on arguments.length

but if one or two of arg is not a number, we return undefined

refactor




20. Make a Person
Fill in the object constructor with the following methods below:

getFirstName() getLastName() getFullName() setFirstName(first) setLastName(last) setFullName(firstAndLast)
Run the tests to see the expected output for each method.

The methods that take an argument must accept only one argument and it has to be a string.

These methods must be the only available means of interacting with the object.

	Object.keys(bob).length should return 6.
	bob instanceof Person should return true.
	bob.firstName should return undefined.
	bob.lastName should return undefined.
	bob.getFirstName() should return "Bob".
	bob.getLastName() should return "Ross".
	bob.getFullName() should return "Bob Ross".
	bob.getFullName() should return "Haskell Ross" after bob.setFirstName("Haskell").
	bob.getFullName() should return "Haskell Curry" after bob.setLastName("Curry").
	bob.getFullName() should return "Haskell Curry" after bob.setFullName("Haskell Curry").
	bob.getFirstName() should return "Haskell" after bob.setFullName("Haskell Curry").
	bob.getLastName() should return "Curry" after bob.setFullName("Haskell Curry").

#### Soln

This is an example of closure

Uses variables set in constructor function without using properties set




21. Map the debris


#### Soln