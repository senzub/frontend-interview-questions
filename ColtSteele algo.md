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

3. Write a function called averagePair. Given a sorted array of integers and a target average, determine if there is a pair of values in the array where the average of the pair equals the target average. There may be more than one pair that matches the target average.

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


4. isSubsequence - Write a function called isSubsequence which takes in two strings and checks whether the characters in the first string form a subsequence of the characters in the second string. In other words, the function should check whether the characters in the first string appear somewhere in the second string, without their order changing

isSubsequence("hello", "hello world") // true
isSubsequence("sing", "sting") // true
isSubsequence("abc", "abracadabra") // true
isSubsequence("abc", "acb") // false (order matters)


///////////////////////////
## Sliding Window Pattern - 

//////////////////////////
1. Write a function called maxSubarraySum which accepts an array of integers and a number called n. The function should calculate the maximum sum of n consecutive elements in the array.

#### CS's soln

Naive

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
