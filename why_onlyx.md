## Why onlyx?
In 2015 I was pleased to add the [onlyx](https://docs.hhvm.com/hsl/reference/function/HH.Lib.C.onlyx/) function to the FB Hack standard library. It extended a family of array helper functions featuring old favourites like:
* **first**: get the first element of an array, or any Traversable - return null if the array is empty
* **firstx**: get the first element of an array, or any Traversable - throw an exception if the array is empty
* **last**: get the last element of an array, or any Traversable - return null if the array is empty

I often found myself writing code that ended up with an array that (should!) have a single element in it[^1]. If the array is empty OR if there's more than 1 object then something has gone horribly wrong with the logic. firstx raises hell for the empty case, but would ignore any extras.

My diff summary read:
> To return the one and only value in an array, throws for empty arrays ro arrays with more than one element.

I'm delighted that this function has made it to the public release of the hack standard library and has found many thousands of uses in the Meta website codebase. It's even been ported to the Meta python & js utils. There's a pretty high chance that this is the longest lived thing I will ever create in my tech career :-/.

[^1]: As an aside, something has probably gone wrong with the structure of the program that features an array that should have 1 (no more, no less) elements in it, but we live in an imperfect world.
