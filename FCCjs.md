

#### Basic Algorithm Scripting

1. Days of the week, write a function that, given a String S representing the day of the week and an integer K (between 0 and 500), returns the day of the week that is K days later

ex: S= "Web" and K=2 , return "Fri"

let days = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"];


#### Soln

2. Largest number of each array, in array of arrays, return new array

#### Soln


3. Check whether string ends with given substring

#### Soln


4. Repeat a string

key is two different parts

#### Soln

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

https://stackoverflow.com/questions/7273668/how-to-split-a-long-array-into-smaller-arrays-with-javascript

#### Soln



## Intermediate Algorithm Scripting

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





