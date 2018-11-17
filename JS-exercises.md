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






2. Make this work: duplicate([1,2,3,4,5]); // [1,2,3,4,5,1,2,3,4,5]

function duplicateArray(array) {
	return array.concat(array);
}



3. Explain why the following doesn't work as an IIFE: function foo(){ }();. What needs to be changed to properly make it an IIFE?


simple function?
most function require extra to input var