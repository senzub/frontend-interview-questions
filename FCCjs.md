
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



5. Cut string to match length


#### Soln



6. Title Case a sentence

#### Soln

7. Insert, flatten array, only at specific index, combining arrays

#### Soln



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


2. 

#### Soln

3. 

#### Soln

4. 

#### Soln

5. 

#### Soln

6. 

#### Soln


7. 

#### Soln

8. 

#### Soln

9. 

#### Soln



10. Find the missing letter in the passed letter range and return it.

If all letters are present in the range, return undefined.

	fearNotLetter("abce") should return "d".
	fearNotLetter("abcdefghjklmno") should return "i".
	fearNotLetter("stvwx") should return "u".
	fearNotLetter("bcdf") should return "e".
	fearNotLetter("abcdefghijklmnopqrstuvwxyz") should return undefined.

#### Soln







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





