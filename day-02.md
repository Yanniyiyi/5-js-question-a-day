# Question 1

Return the number (count) of vowels in the given string.

We will consider a, e, i, o, and u as vowels for this Kata.

## Solution

```js
function getCount(str) {
  var vowelsCount = 0;
  
  var hash = {
    a:{},
    e:{},
    i:{},
    o:{},
    u:{}
  };
  
  var strArr = str.toLowerCase().split("");
  strArr.forEach(function(item){
    if(hash[item]){
      vowelsCount += 1;
    }
  }); 
  return vowelsCount;
}
```

# Question 2

Implement a function that adds two numbers together and returns their sum in binary. The conversion can be done before, or after the addition.

The binary number returned should be a string.

```js
function addBinary(a,b) {
  return Math.floor(a+b).toString(2);
}
```

# Question 3

Deoxyribonucleic acid (DNA) is a chemical found in the nucleus of cells and carries the "instructions" for the development and functioning of living organisms.

If you want to know more [http://en.wikipedia.org/wiki/DNA](http://en.wikipedia.org/wiki/DNA)

In DNA strings, symbols "A" and "T" are complements of each other, as "C" and "G". You have function with one side of the DNA (string, except for Haskell); you need to get the other complementary side. DNA strand is never empty or there is no DNA at all (again, except for Haskell).

```
DNAStrand ("ATTGC") # return "TAACG"

DNAStrand ("GTAT") # return "CATA"
```

## Solution

```js
function DNAStrand(dna){
  return [].map.call(dna,function(prev,next){
    switch(prev){
      case 'A':
        return 'T';
      case 'T':
        return 'A';
      case 'C':
        return 'G';
      case 'G':
        return 'C';
    }
  }).join('');
}
```

# Question 4

Write a function that takes in a string of one or more words, and returns the same string, but with all five or more letter words reversed (Just like the name of this Kata). Strings passed in will consist of only letters and spaces. Spaces will be included only when more than one word is present.

Examples:

`spinWords( "Hey fellow warriors" )` => returns "Hey wollef sroirraw" 
`spinWords( "This is a test")` => returns "This is a test" 
`spinWords( "This is another test" )`=> returns "This is rehtona test"

## Solution

```js
function spinWords(words){

  var wordsArr = words.split(" ").map(function(item){
    if(item.length >= 5){
      return item.split("").reverse().join("");
    }
    return item
  });
  
  return wordsArr.join(" ");
}
```

# Question 5

Your task is to make a function that can take any non-negative integer as a argument and return it with it's digits in descending order. Essentially, rearrange the digits to create the highest possible number.

## Examples:

Input: `21445` Output: `54421`

Input: `145263` Output: `654321`

Input: `1254859723` Output: `9875543221`

## Solution

```js
function descendingOrder(n){
  var strNumArr = n.toString().split("");
  var strResult = strNumArr.sort(function(a,b){
    return b - a
  }).join("");
  return parseInt(strResult);
}
```

