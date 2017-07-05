## Question 1

ROT13 is a simple letter substitution cipher that replaces a letter with the letter 13 letters after it in the alphabet. ROT13 is an example of the Caesar cipher.

Create a function that takes a string and returns the string ciphered with Rot13. If there are numbers or special characters included in the string, they should be returned as they are. Only letters from the latin/english alphabet should be shifted, like in the original Rot13 "implementation".

## Solution

```js
var alphabet = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXWZ";
var cipher   = "nopqrstuvwxyzabcdefghijklmNOPQRSTUVWXWZABCDEFGHIJKLM";

function rot13(message){
  return message.split('').map(function(c) {
    var i = alphabet.indexOf(c);
    if (i < 0) {
      // not in alphabet, return char
      return c;
    }
    
    return cipher[i];
  }).join('');
}
```

# Question 2

We want to create a function that will add numbers together when called in succession.

```
add(1)(2);
// returns 3

```

We also want to be able to continue to add numbers to our chain.

```
add(1)(2)(3); // 6
add(1)(2)(3)(4); // 10
add(1)(2)(3)(4)(5); // 15

```

and so on.

A single call should return the number passed in.

```
add(1); // 1

```

We should be able to store the returned values and reuse them.

```
var addTwo = add(2);
addTwo; // 2
addTwo + 5; // 7
addTwo(3); // 5
addTwo(3)(5); // 10

```

We can assume any number being passed in will be valid whole number.

## Solution

```js
function add(n){
  var fn = function(x){
    return add(n + x);
  }
  fn.valueOf = function(){
    return n;
  }
  
  return fn;
}
```

# Question 3

Pete likes to bake some cakes. He has some recipes and ingredients. Unfortunately he is not good in maths. Can you help him to find out, how many cakes he could bake considering his recipes?

Write a function `cakes()`, which takes the recipe (object) and the available ingredients (also an object) and returns the maximum number of cakes Pete can bake (integer). For simplicity there are no units for the amounts (e.g. 1 lb of flour or 200 g of sugar are simply 1 or 200). Ingredients that are not present in the objects, can be considered as 0.

Examples:

```
// must return 2
cakes({flour: 500, sugar: 200, eggs: 1}, {flour: 1200, sugar: 1200, eggs: 5, milk: 200}); 
// must return 0
cakes({apples: 3, flour: 300, sugar: 150, milk: 100, oil: 100}, {sugar: 500, flour: 2000, milk: 2000});
```

## Solution

```js
function cakes(recipe, available) {
  var ingredients = [];
  for(var recipeItem in recipe){
    if(typeof available[recipeItem] === 'undefined'){
      return 0;
    }
    ingredients.push(Math.floor(available[recipeItem]/recipe[recipeItem]));
  }
  return ingredients.sort(function(a,b){return a - b;})[0];
}
```

# Question 4

Given an `n x n` array, return the array elements arranged from outermost elements to the middle element, traveling clockwise.

```
array = [[1,2,3],
         [4,5,6],
         [7,8,9]]
snail(array) #=> [1,2,3,6,9,8,7,4,5]

```

For better understanding, please follow the numbers of the next array consecutively:

```
array = [[1,2,3],
         [8,9,4],
         [7,6,5]]
snail(array) #=> [1,2,3,4,5,6,7,8,9]
```

## Solution

```js
snail = function(array) {
  var result = null;
  while(array.length){
    result = (result ? result.concat(array.shift()) : array.shift());
    for(var i = 0; i < array.length; i++){
      result.push(array[i].pop());
    }
    result = result.concat((array.pop() || []).reverse());
    for(var i = array.length - 1; i >= 0; i--){
      result.push(array[i].shift());
    }
  }
  return result;
}
```

# Question 5

Given two arrays of strings `a1` and `a2` return a sorted array `r` in lexicographical order of the strings of `a1` which are substrings of strings of `a2`.

\#Example 1: `a1 = ["arp", "live", "strong"]`

`a2 = ["lively", "alive", "harp", "sharp", "armstrong"]`

returns `["arp", "live", "strong"]`

\#Example 2: `a1 = ["tarp", "mice", "bull"]`

`a2 = ["lively", "alive", "harp", "sharp", "armstrong"]`

returns `[]`

## Solution

```js
function inArray(array1,array2){
  return array1.filter(function(item){
    return array2.some(function(arr2item){
      return arr2item.includes(item);
    });
  }).sort();
}
```

