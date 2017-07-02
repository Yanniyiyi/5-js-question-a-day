# Question 1
## The museum of incredible dull things

The museum of incredible dull things wants to get rid of some exhibitions. Miriam, the interior architect, comes up with a plan to remove the most boring exhibitions. She gives them a rating, and then removes the one with the lowest rating.

However, just as she finished rating all exhibitions, she's off to an important fair, so she asks you to write a program that tells her the ratings of the items after one removed the lowest one. Fair enough.

## Task

Given an array of integers, remove the smallest value. Do not mutate the original array/list. If there are multiple elements with the same value, remove the one with a lower index. If you get an empty array/list, return an empty array/list.

Don't change the order of the elements that are left.

## Examples
```js
removeSmallest([1,2,3,4,5]) = [2,3,4,5]
removeSmallest([5,3,2,1,4]) = [5,3,2,4]
removeSmallest([2,2,1,2,1]) = [2,2,2,1]
```
## Solution
```js
function removeSmallest(nums){
  if(!nums){
    return [];
  }
  var smallest = Math.min.apply(null,nums);
  nums.splice(nums.indexOf(smallest),1);
  return nums;
}
```
# Question 2
You are going to be given a word. Your job is to return the middle character of the word. If the word's length is odd, return the middle character. If the word's length is even, return the middle 2 characters.

## Examples:

Kata.getMiddle("test") should return "es"

Kata.getMiddle("testing") should return "t"

Kata.getMiddle("middle") should return "dd"

Kata.getMiddle("A") should return "A"
## Input

A word (string) of length 0 < str < 1000

## Output

The middle character(s) of the word represented as a string.
## Solution
```js
function getMiddle(s)
{
  if(s.length == 1){
    return s;
  }
  
  if(s.length % 2 == 0){  
    return s.substr((s.length-2)/2,2);
  }
  
 if(s.length % 2 != 0){
    return s.substr((s.length-1)/2,1);
  }
}
```
# Question 3
Implement the function unique_in_order which takes as argument a sequence and returns a list of items without any elements with the same value next to each other and preserving the original order of elements.

For example:
```js
uniqueInOrder('AAAABBBCCDAABBB') == ['A', 'B', 'C', 'D', 'A', 'B']
uniqueInOrder('ABBCcAD')         == ['A', 'B', 'C', 'c', 'A', 'D']
uniqueInOrder([1,2,2,3,3])       == [1,2,3]
```
## Solution
```js
var uniqueInOrder=function(iterable){
  var result = [];

  if(iterable.length == 0){
    return result;
  }
  result.push(iterable[0]);
  Array.prototype.reduce.call(iterable,function(a,b){
    if(a !== b){
      result.push(b);
    }
    return b;
  },result[0]);
  
  return result;
}
```
# Question 4
The goal of this exercise is to convert a string to a new string where each character in the new string is '(' if that character appears only once in the original string, or ')' if that character appears more than once in the original string. Ignore capitalization when determining if a character is a duplicate.

Examples:

"din" => "((("

"recede" => "()()()"

"Success" => ")())())"

"(( @" => "))(("

```js
function duplicateEncode(word){
   var hash = {};
   var result = [];
   word.split('').forEach(function(item,index){
     var item = item.toLowerCase();
     if(hash[item]){
       result[hash[item].lastIndex] = ')';
       result.push(')');
     }
     else{
       result.push('(');
     }
     hash[item] = {lastIndex: index};  
   });
   
   return result.join("");
}
```
# Question 5
Given: an array containing hashes of names

Return: a string formatted as a list of names separated by commas except for the last two names, which should be separated by an ampersand.

Example:
```js
list([ {name: 'Bart'}, {name: 'Lisa'}, {name: 'Maggie'} ])
// returns 'Bart, Lisa & Maggie'

list([ {name: 'Bart'}, {name: 'Lisa'} ])
// returns 'Bart & Lisa'

list([ {name: 'Bart'} ])
// returns 'Bart'

list([])
// returns ''
```
*Note: all the hashes are pre-validated and will only contain A-Z, a-z, '-' and '.'.*
```js
function list(names){
  var result = "";
  var length = names.length;
  if(length  == 0){
    return result;
  }
  
  if(length == 1){
    return names[0].name;
  }
  
  if(length == 2){
    return names[0].name  + " & " + names[1].name;
  }
  
  names.forEach(function(item,index){
    if(index == length - 2){
      result += item.name + " ";
    }
    else if(index == length - 1){
      result += '& ' + item.name;     
    } else {
      result += item.name + ", ";
    }
  });
  
  return result;
  
}
```