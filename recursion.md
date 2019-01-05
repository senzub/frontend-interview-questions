

#### fibonacci

#### pascal

#### factorial

#### string reverse




#### array flatten

// with concat

function flattenArray(array) {
	let newArray = [];
	for (let i = 0; i < array.length; i++) {
		if (array[i].constructor == Array) {
			newArray = newArray.concat(flattenArray(array[i]));
		}
		else {
			newArray.push(array[i]);
		}
	}	
	return newArray;

}

// with ...

function flattenArray(array) {
	let newArray = [];
	for (let i = 0; i < array.length; i++) {
		if (array[i].constructor == Array) {
			newArray = [...newArray, ...flattenArray(array[i])];
		}
		else {
			newArray.push(array[i]);
		}
	}	
	return newArray;

}



#### array sum




#### Digit counter

// breaks down with 0 counting in 000 string, due to coercion to string cuts off all zeroes

function digitCount(num, digit) {
	let count = 0;
	let stringNum = String(num);
	function counter(stringNum, digit) {
		if (stringNum.length == 0) {
			return;
		}
		if (stringNum.charAt(0) == digit) {
			count++;
		}
		return counter(stringNum.slice(1), digit);
	}
	counter(stringNum, digit);
	return count;
}

#### Remove char that occur more than once




#### Find greatest common divisor between 2 num


function GCD(a,b) {
	if (typeof a != "number" || typeof b != "number" 
		|| isNaN(a) || isNaN(b)) {
		return false;
	}
	let gcd = a < b ? a : b;
	function findGCD(a,b,g) {
		if (g == 1) {
			gcd = 1;
			return;
		}
		else if (a%g == 0 && b%g == 0) {
			gcd = g;
			return;
		}
		else {
			findGCD(a,b, g-1);
		}
	}
	findGCD(a,b,gcd);
	return gcd;
}


#### Find Lowest common multiple between two numbers

function LCM(a,b) {
	if (typeof a != "number" || typeof b != "number" 
		|| isNaN(a) || isNaN(b)) {
		return false;
	}
	let lcm = a < b ? a : b;
	function findLCM(a,b,l) {
		if (l == 1) {
			lcm = 1;
			return;
		}
		else if (a%l == 0 && b%l == 0) {
			lcm = l;
			return;
		}
		else {
			findLCM(a,b, l-1);
		}
	}
	findLCM(a,b,lcm);
	return lcm;
}



