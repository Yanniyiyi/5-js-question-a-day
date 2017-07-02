# Question 1

Well met with Fibonacci bigger brother, AKA Tribonacci.

As the name may already reveal, it works basically like a Fibonacci, but summing the last 3 (instead of 2) numbers of the sequence to generate the next. And, worse part of it, regrettably I won't get to hear non-native Italian speakers trying to pronounce it :(

So, if we are to start our Tribonacci sequence with [1,1,1] as a starting input (AKA *signature*), we have this sequence:

```
[1,1,1,3,5,9,17,31,...]

```

But what if we started with [0,0,1] as a signature? As starting with [0,1] instead of [1,1] basically *shifts* the common Fibonacci sequence by once place, you may be tempted to think that we would get the same sequence shifted by 2 places, but that is not the case and we would get:

```
[0,0,1,1,2,4,7,13,24,...]

```

Well, you may have guessed it by now, but to be clear: you need to create a fibonacci function that given a **signature** array/list, returns **the first n elements - signature included** of the so seeded sequence.

Signature will always contain 3 numbers; n will always be a non-negative number; if `n==0`, then return an empty array and be ready for anything else which is not clearly specified ;)

If you enjoyed this kata more advanced and generalized version of it can be found in the [Xbonacci kata](http://www.codewars.com/kata/fibonacci-tribonacci-and-friends)

*[Personal thanks to Professor Jim Fowler on Coursera for his awesome classes that I really recommend to any math enthusiast and for showing me this mathematical curiosity too with his usual contagious passion :)]*

```js
function tribonacci(signature,n){
  if(n < 3){
    return signature.slice(0,n);
  }
  
  var result = signature;
  for(var i = 2; i < n-1; i++){
    result.push(result[i - 2] + result[i - 1] + result[i]);
  }
  
  return result;
}
```

# Question 2

Write a function, `persistence`, that takes in a positive parameter `num` and returns its multiplicative persistence, which is the number of times you must multiply the digits in `num` until you reach a single digit.

For example:

```
 persistence(39) === 3 // because 3*9 = 27, 2*7 = 14, 1*4=4
                       // and 4 has only one digit

 persistence(999) === 4 // because 9*9*9 = 729, 7*2*9 = 126,
                        // 1*2*6 = 12, and finally 1*2 = 2

 persistence(4) === 0 // because 4 is already a one-digit number
```

## Solution

```js
function persistence(num) {
   if(num < 10){
     return 0;
   }
   
   if(num >= 10 && num < 25){
     return 1;
   }
   
   if(num % 10 == 0){
     return 1;
   }
  
   var count = 0;
   var numberArr = num.toString().split('');
   function multiple(numberArr){
      return numberArr.reduce(function(a,b){
       return a*b;
     });
   }
   while(numberArr.length > 1){
     var num =  multiple(numberArr);
     numberArr = num.toString().split('');
     count++;
   }
   return count;
}
```

# Question 3

# Is Prime

Define a function `isPrime` that takes one integer argument and returns `true` or `false` depending on if the integer is a prime.

Per Wikipedia, a prime number (or a prime) is a natural number greater than 1 that has no positive divisors other than 1 and itself.

## Example

```
isPrime(5)
=> true

```

## Assumptions

- You can assume you will be given an integer input.
- You can not assume that the integer will be only positive. You may be given negative numbers.

```js
function isPrime(num) {

  if(num > 1){
    for(var i = 2, sqrt = Math.sqrt(Math.abs(num)); i <= sqrt; i++ )
    {
      if(num % i == 0){
        return false;
      }
    }
    return true;
  }
  
  return false;
}
```

# Question 4

ATM machines allow 4 or 6 digit PIN codes and PIN codes cannot contain anything but exactly 4 digits or exactly 6 digits.

If the function is passed a valid PIN string, return true, else return false.

eg:

```
validatePIN("1234") === true
validatePIN("12345") === false
validatePIN("a234") === false
```

## Solution

```js
function validatePIN (pin) {
  //return true or false
  var reg = /^(\d{4}|\d{6})$/;
  return reg.test(pin);
};
```

# Question 5

Complete the method/function so that it converts dash/underscore delimited words into camel casing. The first word within the output should be capitalized only if the original word was capitalized.

Examples:

```
// returns "theStealthWarrior"
toCamelCase("the-stealth-warrior") 

// returns "TheStealthWarrior"
toCamelCase("The_Stealth_Warrior")
```

## Solution 

```js
function toCamelCase(str){
      var regExp=/[-_]\w/ig;
      return str.replace(regExp,function(match){
            return match.charAt(1).toUpperCase();
       });
}
```

