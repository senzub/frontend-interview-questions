/////////////////////////////
## Frequency Counter - 
/////////////////////////////


1. same function: write a function called same which accepts two arrays. The function should return true if every value in the array has it's corresponding value squared in the second array. 

#### my Soln

function same(arr1, arr2) {
	if (arr1.length !== arr2.length) return false;
	let arr1Count = arr1.reduce((obj, ele) => {
		obj[ele] = obj[ele] ? ++obj[ele]:1;
		return obj;
	}, {})
	let arr2Count = arr2.reduce((obj, ele) => {
		obj[ele] = obj[ele] ? ++obj[ele]:1;
		return obj;
	}, {})	
	let arr1Keys = Object.keys(arr1Count);
	return arr1Keys.every((key) => {
		return arr2Count.hasOwnProperty(key**2) && arr2Count[key**2] == arr1Count[key];
	})
}

#### CS's soln:

function same(arr1, arr2){
    if(arr1.length !== arr2.length){
        return false;
    }
    let frequencyCounter1 = {}
    let frequencyCounter2 = {}
    for(let val of arr1){
        frequencyCounter1[val] = (frequencyCounter1[val] || 0) + 1
    }
    for(let val of arr2){
        frequencyCounter2[val] = (frequencyCounter2[val] || 0) + 1        
    }
    for(let key in frequencyCounter1){
        if(!(key ** 2 in frequencyCounter2)){
            return false
        }
        if(frequencyCounter2[key ** 2] !== frequencyCounter1[key]){
            return false
        }
    }
    return true
}

same([1,2,3,2,5], [9,1,4,4,11])


2. anagrams: Given two strings, function determines if second string is anagram of 1st 

i.e. same letters, different orders

#### my Soln

function validAnagram(str1, str2) {
	if (str1.length !== str2.length) return false;
	let str1Count = [].reduce.call(str1,(obj, ele) => {
		obj[ele] = obj[ele] ? ++obj[ele]:1;
		return obj;
	}, {})
	let str2Count = [].reduce.call(str2,(obj, ele) => {
		obj[ele] = obj[ele] ? ++obj[ele]:1;
		return obj;
	}, {})
	let str1Keys = Object.keys(str1Count);
	return str1Keys.every((key) => {
		return str2Count.hasOwnProperty(key) && str2Count[key] == str1Count[key];
	})
}

#### CS's soln:

function validAnagram(first, second) {
  if (first.length !== second.length) {
    return false;
  }

  const lookup = {};

  for (let i = 0; i < first.length; i++) {
    let letter = first[i];
    // if letter exists, increment, otherwise set to 1
    lookup[letter] ? lookup[letter] += 1 : lookup[letter] = 1;
  }

  for (let i = 0; i < second.length; i++) {
    let letter = second[i];
    // can't find letter or letter is zero then it's not an anagram
    if (!lookup[letter]) {
      return false;
    } else {
      lookup[letter] -= 1;
    }
  }

  return true;
}

// {a: 0, n: 0, g: 0, r: 0, m: 0,s:1}
validAnagram('anagrams', 'nagaramm')



3. sameFrequency - Write a function called sameFrequency. Given two positive integers, find out if the two numbers have the same frequency of digits. Your solution Must have the following complexities:
Time: O(N)

sameFrequency(182,281) // true
sameFrequency(34,14) // false
sameFrequency(3589578,5879385) // true
sameFrequency(22,222) // false

#### CS's soln

function sameFrequency(num1, num2){
  let strNum1 = num1.toString();
  let strNum2 = num2.toString();
  if(strNum1.length !== strNum2.length) return false;
  
  let countNum1 = {};
  let countNum2 = {};
  
  for(let i = 0; i < strNum1.length; i++){
    countNum1[strNum1[i]] = (countNum1[strNum1[i]] || 0) + 1
  }
  
  for(let j = 0; j < strNum1.length; j++){
    countNum2[strNum2[j]] = (countNum2[strNum2[j]] || 0) + 1
  }
  
  for(let key in countNum1){
    if(countNum1[key] !== countNum2[key]) return false;
  }
 
  return true;
}

#### my soln

function sameFrequency(a,b){
  let num1 = String(a).split("");
  let num2 = String(b).split("");
  if (num1.length !== num2.length) return false;
  let countNum1 = num1.reduce((obj,ele) => {
    obj[ele] = obj[ele] ? ++obj[ele] : 1;
    return obj;
  },{});
  let countNum2 = num2.reduce((obj,ele) => {
    obj[ele] = obj[ele] ? ++obj[ele] : 1;
    return obj;
  },{}) ;
  let num1Keys = Object.keys(countNum1);
  return num1Keys.every((key) => {
      return countNum2.hasOwnProperty(key) && countNum2[key] === countNum1[key];
  });
}


4. Implement a function called areThereDuplicates which accpets a variable number of arguments, and checks whether there are any duplicates among the arguments passed in. You can solve this using the frequency counter pattern OR the multiple pointers pattern

areThereDuplicates(1,2,3) // false
areThereDuplicates(1,2,2) // true
areThereDuplicates('a','b','c','a') // true

Time - O(n)
Space - O(n)

#### CS's soln - frequency counter

function areThereDuplicates() {
  let collection = {}
  for(let val in arguments){
    collection[arguments[val]] = (collection[arguments[val]] || 0) + 1
  }
  for(let key in collection){
    if(collection[key] > 1) return true
  }
  return false;
}

#### CS's soln - multiple pointers

function areThereDuplicates(...args) {
  // Two pointers
  args.sort((a,b) => a > b);
  let start = 0;
  let next = 1;
  while(next < args.length){
    if(args[start] === args[next]){
        return true
    }
    start++
    next++
  }
  return false
}


#### mysoln - frequency counter pattern

areThereDuplicates(...arr) {
	let dups = arr.filter((ele,ind) => arr.includes(ele,ind+1));
	return dups.length ? true : false;
}

function areThereDuplicates(...a) {
  let isDup = a.filter((ele,ind) => a.includes(ele, ind+1));
  return isDup.length ? true : false;
}

function areThereDuplicates(...a) {
    let count = a.reduce((obj,ele) => {
        obj[ele] = obj[ele] ? ++obj[ele] : 1;
        return obj;
    }, {});
    let keys = Object.keys(count);
    return keys.some((key) => {
        return count[key] > 1;
    });
}


///////////////////////////////////
## Multiple Pointers - 
///////////////////////////////////

1. sumZero: write a function which accepts a sorted array of integers. The function should find the first pair where the sum is 0. Return an array that includes both values that sum to zero or undefined if the pair dne.

#### my soln

function sumZero(arr) {
	
}

#### CS's naive soln

function sumZero(arr){
    for(let i = 0; i < arr.length; i++){
        for(let j = i+1; j < arr.length; j++){
            if(arr[i] + arr[j] === 0){
                return [arr[i], arr[j]];
            }
        }
    }
}

#### CS's good soln

function sumZero(arr) {
	let left = 0;
	let right = arr.length-1;
	while(left < right) {
		let sum = arr[left] + arr[right];
		if (sum === 0) {
			return [arr[left], arr[right]];
		} else if (sum>0) {
			right--;
		} else if (sum<0) {
			left++;
		}
	}
	return undefined;
}


sumZero([-4,-3,-2,-1,0,1,2,5])


2. countUniqueValues: function accepts sorted array, and counts the unique values in the array. There can be negative numbers in the array, but always sorted


#### my soln

//// error was from 

function countUniqueValues(arr) {
	if (arr.length == 0) return 0;
	let i = 0;
	let j = 1;
	while (j < arr.length) {
		if (arr[i] !== arr[j]) {
			i++;
			arr[i] = arr[j];			
			j++;
		} else {
			j++;
		}
	}
	return i+1;
}

function countUniqueValues(arr) {
	if (arr.length == 0) return 0;
	if (arr.length == 1) return 1;
	let trimmedArr = arr.filter((ele, ind) => arr.indexOf(ele) == ind);
	let arrCount = trimmedArr.reduce((obj,ele) => {
		obj[ele] = obj[ele] ? ++obj[ele] : 1;
		return obj;
	}, {})
	return trimmedArr.filter((ele) => {
		return arrCount[ele] == 1;
	}).length;
}


#### CS's soln

function countUniqueValues(arr) {
	var i = 0;
	for (var j = 1; j < arr.length; j++) {
		if (arr[i] !== arr[j]) {
			i++;
			arr[i] = arr[j];
		}
	}
	return i+1;
}

3. averagePair - Write a function called averagePair. Given a sorted array of integers and a target average, determine if there is a pair of values in the array where the average of the pair equals the target average. There may be more than one pair that matches the target average.

Time: O(N)
Space: O(1)

averagePair([1,2,3], 2.5)  // true
averagePair([1,3,3,5,6,7,10,12,19], 8)  // true
averagePair([-1,0,3,4,5,6], 4.1)  // false
averagePair([], 4)  // false


#### my soln

function averagePair(arr,target){
  let i = 0;
  let j = arr.length - 1;
  let temp = 0;
  let values = [];
  while (i < j) {
      temp = (arr[i] + arr[j]) / 2;
      if (temp > target) {
          j--;
      } else if (temp < target) {
          i++;
      } else {
          values.push(i,j);
          break;
      }
  }
    return values.length ? true : false;
}

#### CS's soln

function averagePair(arr, num){
  let start = 0
  let end = arr.length-1;
  while(start < end){
    let avg = (arr[start]+arr[end]) / 2 
    if(avg === num) return true;
    else if(avg < num) start++
    else end--
  }
  return false;
}



4. isSubsequence - Write a function called isSubsequence which takes in two strings and checks whether the characters in the first string form a subsequence of the characters in the second string. In other words, the function should check whether the characters in the first string appear somewhere in the second string, without their order changing

isSubsequence("hello", "hello world") // true
isSubsequence("sing", "sting") // true
isSubsequence("abc", "abracadabra") // true
isSubsequence("abc", "acb") // false (order matters)


#### mysoln

function isSubsequence(str1, str2) {
    let i = 0;
    let j = 0;
    while (j < str2.length) {
        if (str1.charAt(i) === str2.charAt(j)) i++;
        if (str1.length === i) return true;
        j++;
    }
    return false;
}



#### CS's soln

function isSubsequence(str1, str2) {
  var i = 0;
  var j = 0;
  if (!str1) return true;
  while (j < str2.length) {
    if (str2[j] === str1[i]) i++;
    if (i === str1.length) return true;
    j++;
  }
  return false;
}


///////////////////////////
## Sliding Window Pattern - 

//////////////////////////


1. maxSubarraySum - Write a function called maxSubarraySum which accepts an array of integers and a number called n. The function should calculate the maximum sum of n consecutive elements in the array.

maxSubarraySum([100,200,300,400],2) // 700
maxSubarraySum([1,4,2,10,23,3,1,0,20],4) // 39
maxSubarraySum([-3,4,0,-2,6,-1],2) // 5
maxSubarraySum([3,-2,7,-4,1,-1,4,-2,1],2) // 5
maxSubarraySum([2,3],3) // null

#### my soln

function maxSubarraySum(arr, length){
  if (arr.length < length) return null;
  let max = arr.slice(0, length).reduce((sum,ele) => sum+ele,0);
  let tempMax = max;
  for (let i = length; i < arr.length; i++) {
      tempMax = tempMax - arr[i-length] + arr[i];
      if (tempMax > max) {
          max = tempMax;
      }
  }
  return max;
}


#### CS's soln

***Naive bad***

function maxSubarraySum(arr, num) {
	if (num > arr.length) {
		return null;
	}
	var max = -Infinity;
	for (let i = 0; i < arr.length - num + 1; i++) {
		temp = 0;
		for (let j = 0; j < num; j++) {
			temp += arr[i+j];
		}
		if (temp>max) {
			max = temp;
		}
	}
	return max;
}

Good

function maxSubarraySum(arr,num) {
	let maxSum = 0;
	let tempSum = 0;
	if (arr.length < num) return null;
	for (let i = 0; i < num; i++) {      // sum first 3 digits
		maxSum += arr[i];
	}
	tempSum = maxSum;
	for (let i = num; i < arr.length; i++) {    // start another loop
		tempSum = tempSum - arr[i - num] + arr[i];    // start from num
		maxSum = Math.max(maxSum, tempSum);
	}
	return maxSum;
}



2. minSubArrayLen - write a function called minSubArrayLen which accepts two parameters - an array of positive integers and a positive inger. 
The function should return the minimal length of a contiguous subarray of which the sum is greater than or equal to the integer passed to the function.
If there isn't one, return 0 instead.

minSubArrayLen([2,3,1,2,4,3], 7) // 2 -> because [4,3] is the smallest subarray
minSubArrayLen([2,1,6,5,4, 9) // 2 -> because [5,4] is the smallest subarray
minSubArrayLen([3,1,7,11,2,9,8,21,62,33,19], 52) // 1 -> because [62] is greater than 52
minSubArrayLen([1,4,16,22,5,7,8,9,10], 39) // 3
minSubArrayLen([1,4,16,22,5,7,8,9,10], 55) // 5
minSubArrayLen([4,3,3,8,1,2,3], 11) // 2
minSubArrayLen([1,4,16,22,5,7,8,9,10], 95) // 0


#### my soln



#### CS's soln 

function minSubArrayLen(nums, sum) {
  let total = 0;
  let start = 0;
  let end = 0;
  let minLen = Infinity;
 
  while (start < nums.length) {
    // if current window doesn't add up to the given sum then 
		// move the window to right
    if(total < sum && end < nums.length){
      total += nums[end];
			end++;
    }
    // if current window adds up to at least the sum given then
		// we can shrink the window 
    else if(total >= sum){
      minLen = Math.min(minLen, end-start);
			total -= nums[start];
			start++;
    } 
    // current total less than required total but we reach the end, need this or else we'll be in an infinite loop 
    else {
      break;
    }
  }
 
  return minLen === Infinity ? 0 : minLen;
}



3. findLongestSubstring - write a function called findLongestSubstring which accepts a string and returns the length of the longest substring with all distinct characters

findLongestSubstring('')   // 0
findLongestSubstring("rithmschool")   // 7
findLongestSubstring("thisisawesome")   // 6
findLongestSubstring("thecatinthehat")   // 7
findLongestSubstring('bbbbbb')   // 1
findLongestSubstring('longestsubstring')   // 8
findLongestSubstring('thisishowwedoit')   // 6


#### my soln


#### CS's soln 

function findLongestSubstring(str) {
  let longest = 0;
  let seen = {};
  let start = 0;
 
  for (let i = 0; i < str.length; i++) {
    let char = str[i];
    if (seen[char]) {
      start = Math.max(start, seen[char]);
    }
    // index - beginning of substring + 1 (to include current in count)
    longest = Math.max(longest, i - start + 1);
    // store the index of the next char so as to not double count
    seen[char] = i + 1;
  }
  return longest;
}



///////////////////////////////////////

## Divide and Conquer - this pattern involves dividing a data set into smaller chunks, and then repeating a process with a subset of data

very common, many types of searches and sorts are divide and conquer

naive - array, str, left to right
d&c - break into smaller pieces, repeat process

///////////////////////////////////////

1. given sorted array of integers, write a function called search, that accepts a value and returns the index where the value passed to the function is located. If the value is not found, return -1.

search([1,2,3,4,5]) //3
search([1,2,3,4,5,6]) // 5


naive: looping through left to right, O(n)
Linear search


#### CS's Soln

function search(arr, val) {
	let min = 0;
	let max = arr.length-1;
	while (min <= max) {
		let middle = Math.floor((min+max) / 2);
		let currentElement = arr[middle];
		if (arr[middle] < val) {
			min = middle + 1;
		}
		else if (arr[middle] > val) {
			max = middle + 1;
		}
		else {
			return middle;
		}
	}
	return -1;
}

Binary Search is divide and conquer algorithm, must be sorted 

     1. start at midpoint
     2. check if midpoint is < > search int
     3. if greater, we look at bottom
     4. if smaller, look at top


///////////////////////////////////////

## Recursion - 

///////////////////////////////////////

1. countdown

function countDown(n) {
	if (n<=0) {
		console.log("all done!");
		return;
	}
	console.log(n);
	countDown(n-1);
}

countDown(5);

2. sumRange

function sumRange(num) {
	if (num === 1) return 1;
	return num + sumRange(num-1);
}


3. factorial

function factorial(num) {
	if (num < 1) return "Enter positive int";
	if (num === 1) return 1;
	return num * factorial(num-1);
}
factorial(5);


4. collectOddValues

function collectOddValues(arr) {
	let result = [];
	function helper(input) {
		if (input.length <= 0) return;
		if (input[0]%2 === 1) result.push(input[0]);
		helper(input.slice(1));
	}	
	helper(arr);
	return result;
}

collectOddValues([1,2,3,4,5]);

5. collectOddValues - without helper function/pure recursion

function collectOddValues(arr) {
	let newArr = [];
	if (arr.length === 0) {
		return newArr;
	}
	if (arr[0]%2 !== 0) {
		newArr.push(arr[0]);
	}
	newArr = newArr.concat(collectOddValues(arr.slice(1)));
	return newArr;
}

collectOddValues([1,2,3,4,5]);


### Recursion Set 1

6. power 

function power(base,exp){
    if (exp === 0) return 1;
    if (exp < 1) return base;
    return base* power(base,exp-1);
}

// power(2,0) // 1
// power(2,2) // 4
// power(2,4) // 16


7. factorial

function factorial(n) {
	if (n<=1) return 1;
	return n * factorial(n-1);
}


//factorial(1) // 1
// factorial(2) // 2
// factorial(4) // 24
// factorial(7) // 5040



8. productOfArray

function productOfArray(arr) {
    if (arr.length === 0) {
        return 1;
    }
    return arr[0] * productOfArray(arr.slice(1));
}


// productOfArray([1,2,3]) // 6
// productOfArray([1,2,3,10]) // 60



9. recursiveRange


function recursiveRange(n){
   if (n === 1) return 1;
   return recursiveRange(n-1) + n;
}


// SAMPLE INPUT/OUTPUT
// recursiveRange(6) // 21
// recursiveRange(10) // 55 


10. fib

function fib(num){
  let seq;
  function recur(n) {
      if (n === 1) return [1,1];
      let newSeq = recur(n-1);
      newSeq.push(
          newSeq[newSeq.length -1] + newSeq[newSeq.length-2]
          );
      return newSeq;
  } 
  return recur(num)[num-1];
  
}

// fib(4) // 3
// fib(10) // 55
// fib(28) // 317811
// fib(35) // 9227465


//////////////////////////////
### Recursion Set 2 (Advanced)
//////////////////////////////



11. reverse - write a recursive function called reverse which accepts a string and returns a new string in reverse


#### my soln

function reverse(str) {
	if (str.length === 0) return "";
	return reverse(str.slice(1)) + str.charAt(0);
}

reverse("abc");

// reverse('awesome') // 'emosewa'
// reverse('rithmschool') // 'loohcsmhtir'


#### CS's soln

function reverse(str){
	if(str.length <= 1) return str;
	return reverse(str.slice(1)) + str[0];
}



12. isPalindrome - write a recursive function called isPalindrome which returns true if the string passed to it is a palindrome. Otherwise return false;


#### my soln

function isPalindrome(str){
    function reverse(str) {
    	if (str.length === 0) return "";
    	return reverse(str.slice(1)) + str.charAt(0);
    }  
    let strRev = reverse(str);
    return strRev === str;
}

// isPalindrome('awesome') // false
// isPalindrome('foobar') // false
// isPalindrome('tacocat') // true
// isPalindrome('amanaplanacanalpanama') // true
// isPalindrome('amanaplanacanalpandemonium') // false



#### CS's soln

function isPalindrome(str){
    if(str.length === 1) return true;
    if(str.length === 2) return str[0] === str[1];
    if(str[0] === str.slice(-1)) return isPalindrome(str.slice(1,-1))
    return false;
}



13. someRecursive - write a function called someRecursive which accepts an array and a callback. The function returns true if a single value in the array returns true when passed to the callback. Otherwise it returns true


#### my soln

function someRecursive(arr,f){
  if (arr.length === 0) return false;
  if (f(arr[0])) return true;
  return someRecursive(arr.slice(1),f);
}


// SAMPLE INPUT / OUTPUT
// const isOdd = val => val % 2 !== 0;

// someRecursive([1,2,3,4], isOdd) // true
// someRecursive([4,6,8,9], isOdd) // true
// someRecursive([4,6,8], isOdd) // false
// someRecursive([4,6,8], val => val > 10); // false



#### CS's soln

function someRecursive(array, callback) {
    if (array.length === 0) return false;
    if (callback(array[0])) return true;
    return someRecursive(array.slice(1),callback);
}


14. flatten - write a recursive function which accepts an array of arrays and returns a new array with all values flattened

#### my soln

function flatten(arr){
    let newArr = [];
    for (let i = 0; i < arr.length; i++) {
        if (typeof arr[i] == "object" && arr[i].constructor == Array) {
          newArr = newArr.concat(flatten(arr[i]));
      } else {
          newArr.push(arr[i]);
      }
  } 
  return newArr;
}


// flatten([1, 2, 3, [4, 5] ]) // [1, 2, 3, 4, 5]
// flatten([1, [2, [3, 4], [[5]]]]) // [1, 2, 3, 4, 5]
// flatten([[1],[2],[3]]) // [1,2,3]
// flatten([[[[1], [[[2]]], [[[[[[[3]]]]]]]]]]) // [1,2,3


#### CS's soln

function flatten(oldArr){
  var newArr = []
  	for(var i = 0; i < oldArr.length; i++){
    	if(Array.isArray(oldArr[i])){
      		newArr = newArr.concat(flatten(oldArr[i]))
    	} else {
      		newArr.push(oldArr[i])
    	}
  } 
  return newArr;
}




15. Deep clone an object - this means to make a copy of all the objects wihin objects, instead of sharing a reference to the object

#### my soln


16. capitalizeFirst - write a recursive function called capitalizeFirst. Given an array of strings, capitalize the first letter of each string in the array


// capitalizeFirst(['car','taco','banana']); // ['Car','Taco','Banana']


#### my soln

function capitalizeFirst (arr) {
    let list = [];
    function helper(strings) {
        if (strings.length === 0) return;
        let string = strings[0];
        list.push(
            string.charAt(0).toUpperCase() + string.slice(1)
        );
        return helper(strings.slice(1));
    }
    helper(arr);
    return list;
}

// capitalizeFirst(['car','taco','banana']); // ['Car','Taco','Banana']




#### CS's soln

function capitalizeFirst (array) {
  if (array.length === 1) {
    return [array[0][0].toUpperCase() + array[0].substr(1)];
  }
  const res = capitalizeFirst(array.slice(0, -1));
  const string = array.slice(array.length - 1)[0][0].toUpperCase() + array.slice(array.length-1)[0].substr(1);
  res.push(string);
  return res;
}


17. nestedEvenSum - write a recursive function called nestedEvenSum. Return the sum of all even numbers in an object which may contain nested objects


#### my soln

function nestedEvenSum (obj) {
    let sum = 0;
    function helper(object) {
        for (let key in object) {
            if (typeof object[key] === "object"
                && object[key].constructor === Object
            ) {
                helper(object[key]);
            }
            else if (typeof object[key] == "number"
                && object[key]%2 === 0
            ) {
                sum += object[key];
            }
        }
        return;
    }
    helper(obj);
    return sum;
}


var obj1 = {
  outer: 2,
  obj: {
    inner: 2,
    otherObj: {
      superInner: 2,
      notANumber: true,
      alsoNotANumber: "yup"
    }
  }
}

var obj2 = {
  a: 2,
  b: {b: 2, bb: {b: 3, bb: {b: 2}}},
  c: {c: {c: 2}, cc: 'ball', ccc: 5},
  d: 1,
  e: {e: {e: 2}, ee: 'car'}
};

nestedEvenSum(obj1); // 6
nestedEvenSum(obj2); // 10


#### CS's soln

function nestedEvenSum (obj, sum=0) {
    for (var key in obj) {
        if (typeof obj[key] === 'object'){
            sum += nestedEvenSum(obj[key]);
        } else if (typeof obj[key] === 'number' && obj[key] % 2 === 0){
            sum += obj[key];
        }
    }
    return sum;
}




18. capitalizeWords - write a recursive function, that, given an array of words, return a new array containing each word capitalized.


#### my soln

function capitalizeWords (arr) {
  let list = [];
  function helper(words) {
      if (words.length === 0) return;
      list.push(words[0].toUpperCase());
      helper(words.slice(1));
      return;
  }
  helper(arr);
  return list;
}

// let words = ['i', 'am', 'learning', 'recursion'];
// capitalizedWords(words); // ['I', 'AM', 'LEARNING', 'RECURSION']


#### CS's soln

function capitalizeWords (array) {
  if (array.length === 1) {
    return [array[0].toUpperCase()];
  }
  let res = capitalizeWords(array.slice(0, -1));
  res.push(array.slice(array.length-1)[0].toUpperCase());
  return res;
 
}



19. stringifyNumbers - write a function called stringifyNumbers whicch takes in an object and finds all of the values which are numbers and converts them to strings. Recursion would be a great way to solve this!

#### my soln
// wrong because modifies object, we want copy

function stringifyNumbers(obj) {
    for (let key in obj) {
        if (typeof obj[key] === "object" && obj[key].constructor === Object) {
            obj[key] = stringifyNumbers(obj[key]);
        } else if (typeof obj[key] === "number") {
            obj[key] = String(obj[key]);
        }
    }   
    return obj;
}


//nonmodifying

function stringifyNumbers(obj) {
    let newObj = {};
    for (let key in obj) {
        if (typeof obj[key] === "object" && obj[key].constructor === Object) {
            newObj[key] = stringifyNumbers(obj[key]);
        } else if (typeof obj[key] === "number") {
            newObj[key] = String(obj[key]);
        } else {
            newObj[key] = obj[key];
        }
    }
    return newObj;
}




#### CS's soln

function stringifyNumbers(obj) {
  var newObj = {};
  for (var key in obj) {
    if (typeof obj[key] === 'number') {
      newObj[key] = obj[key].toString();
    } else if (typeof obj[key] === 'object' && !Array.isArray(obj[key])) {
      newObj[key] = stringifyNumbers(obj[key]);
    } else {
      newObj[key] = obj[key];
    }
  }
  return newObj;
}

20. collectStrings - write a function called collectStrings which accepts an object and returns an array of all the values in the object that have a typeof string

#### my soln



#### CS's soln - helper

function collectStrings(obj) {
    var stringsArr = [];
    function gatherStrings(o) {
        for(var key in o) {
            if(typeof o[key] === 'string') {
                stringsArr.push(o[key]);
            }
            else if(typeof o[key] === 'object') {
                return gatherStrings(o[key]);
            }
        }
    }
    gatherStrings(obj);
    return stringsArr;
}

#### CS's soln - pure

function collectStrings(obj) {
    var stringsArr = [];
    for(var key in obj) {
        if(typeof obj[key] === 'string') {
            stringsArr.push(obj[key]);
        }
        else if(typeof obj[key] === 'object') {
            stringsArr = stringsArr.concat(collectStrings(obj[key]));
        }
    }
    return stringsArr;
}



21.

#### my soln

#### CS's soln



22.

#### my soln

#### CS's soln

