### reverse string
```
function reverseString(value) {
  return [...value].reverse().join('');
}
```
### palindrome
```
function palindrome(str) {
  return [...str].every((x, i) => {
    // check if the value is the same as the value on the other end of the array
    return x === str[str.length - 1 - i];
  })
}
```
### palidrome 2
```
(
var word = 'racecar',
  revWord;

revWord = [...word].reverse().join('');
return word === revWord ? 'Palidrome' : 'not';
)();
```

### reverse int
```
function reverseInt(y) {
  const n = y.toString().split('').reverse().join('');
  return parseInt(n) * Math.sign(y); // preserve the original sign of arg
}
```

### create character map and max chars
```
var str = "he3llllo0ooo0o",
  chars = {},
  max = 0,
  maxChar;

// create character map with key as letters, and values as amount of times those letters appear
for (let x of str) {
  chars[x] = chars[x] + 1 || 1;
}

for (let [k, v] of Object.entries(chars)) {
  if( v > max) {
    max = v;
    maxChar = k;
  }
}
console.log(`${maxChar} shows up ${max} times`);
```
### fizzbuzz
```
function FizzBuzz(n) {
  for (let i=1; i<=n; i++) {
    if(i % 5 === 0 && i % 3 === 0) {
      console.log('FizzBuzz');
    } else if (i % 3 === 0) {
      console.log('fizz');
    } else if (i % 5 === 0) {
      console.log('buzz');
    } else {
      console.log(i);
    }
  }
}
```

### array chunk
```
function chunk(array, size) {
  let chunked = [],
    index = 0;
    
  while (index < array.length) {
    chunked.push(array.slice(index, index + size));
    index += size;
  }
  
  return chunked;
    
}

chunk([1,2,3,4,5,6],4);
```

### Anagram with charMap
```
function anagram(a, b) {
  var aMap = buildCharMap(a),
      bMap = buildCharMap(b);
      
  // check for equality before looping
  if (a.length !== b.length) {
    return false;
  }
  // compare a to b
  for (let i in aMap) {
    // if an aMap value of a key isnt the same as bMap, false
    if (aMap[i] !== bMap[i]) {
      return false;
    }
  }
  
  return true;
}

console.log(anagram('cat', 'act'));
  
function buildCharMap(str) {
  var newCharMap = {};
  
  // build Map
  for (let i of str.replace(/[^\w]/g, '').toLowerCase()) {
    newCharMap[i] = newCharMap[i] + 1 || 1;
  }
  
  return newCharMap;
}
```

### Anagram without loops!
```
function anagram(arrayA, arrayB) {
  return cleanString(arrayA) === cleanString(arrayB);
}

function cleanString(str) {
  return str.replace(/[^\w]/g, '').toLowerCase().split('').sort().join('');
}
```

### Capitalize first letter of words
```
function capitalize(str) {
  let words = [];
  
  words = str.split(' ').map(word => {
    return word[0].toUpperCase() + word.slice(1);
  });
  
  return words.join(' ');
}
```

### Capitalize first letter with loops
```
function capitalize(str) {
  let result = str[0].toUpperCase();
  
  for (var i=1; i<str.length; i++){
    if (str[i-1] === ' ') {
      result += str[i].toUpperCase();
    } else {
      result += str[i];
    }
  }
  
  return result
}
```
### print stairs
```
function steps(n) {
  for (let row = 0; row < n; row++) {
    let stairs = '';
    
    for (let column = 0; column < n; column++) {
      if(column <= row) {
        stairs += '#';
      } else {
        stairs += ' ';
      }
    }
    
    console.log(stairs);
  }
}
```
### print pyramid
```
function pyramid(n) {
  const midpoint = Math.floor((2 * n - 1) / 2);
  
  for (let row = 0; row <= n; row++) {
    let level = '';
    
    for (let column = 0; column <= 2 * n - 1; column++) {
      if (midpoint - row <= column && midpoint + row >= column) {
        level += '#';
      } else {
        level += ' ';
      }
    }
    
    console.log(level);
  }
}
```

### find vowels
```
function checkForVowel(str) {
  var count = 0;
  const vowels = ['a','e','i','o','u'];
  
  for (let char of str.toLowerCase()) {
    if (vowels.includes(char)) {
      count++;
    }
  }
  
  return count;
}

OR

function checkForVowel(str) {
  const matches = str.match(/[aeiou]/gi);
  
  return matches ? matches.length : 0;
}
```

### fibonacci recursive
```
function fib(n) {
  if (n < 2) {
    return n;
  }

  return fib(n - 1) + fib(n - 2);
}
// this runtime will be exponential as every increase in n dramatically increases number of calls
// to increase runtime, we can use memoization...we cache the results of each func call

function memoize(fn) {
  const cache = {};
  return function(...args) {
    // search for a cached value
    if (cache[args]) {
      return cache[args];
    }
    
    // if not found, run code and cache result before returning
    const result = fn.apply(this, args);
    cache[args] = result;
    
    return result;
  };
}

const fib = memoize(fib);
fib(15) // returns the memoized version of fibonacci recursive
```

### build an event system
```
class Events {
  constructor() {
    this.events = {};
  }

  on(eventName, callback) {
    if (this.events[eventName]) {
      // add cb to callback with same key
      this.events[eventName].push(callback);
    } else {
      // or make a new key if it dont exist yet
      this.events[eventName] = [callback];
    }
  }

  trigger(eventName) {
    if (this.events[eventName]) {
      // trigger all callbacks for the event
      for (let cb of this.events[eventName]) {
        cb();
      }
    }
  }

  off(eventName) {
    delete this.events[eventName];
  }
}
```

### sumZero
```
function sumZero(arr) {
  let left = 0,
    right = arr.length - 1;
  
  // we have our pointers set to opposite ends. We now want to make
  // them move to the middle of the sorted arr to check for value
  while (left < right) {
    let sum = arr[left] + arr[right];
    if (sum === 0) {
      return [arr[left], arr[right]];
    } else if (sum > 0) { // sum pos? right too big, move right pointer down 1 space
      right--;
    } else {
      left++; // sum negative? left too big, move left 1 space up
    }
  }
}
```

### count Unique values
```
function countInique (arr) {
  var counts = {};
  for (let i = 0; i < arr.length; i++) {
    counts[arr[i]] = counts[arr[i]] + 1 || 1;
  }
  return Object.keys(counts).length;
}
```

### find max sum for an array of n values
```
// loop through array once, calc the maxSum values
// loop through initial subset and find tempSum
// loop rest of arr starting at subset end and calc new sum
// compare newSum and tempSum to find max
// keep looping through each value to find the max sum
function maxSubarraySum(arr, num) {
  let maxSum = 0,
    tempSum = 0;

  // loop based on num length and calc sum as max sum
  for(let i=0;i<num;i++) {
    maxSum += arr[i];
  } 
  tempSum = maxSum;
  for(let i=num;i<arr.length;i++) {
  // we have a subset of n values. Move that subset over
  // add next value, subtract prev first value (since we need to keep the length the same)
  // compare that sum to the maxSum and set appropriately
    tempSum = tempSum - arr[i-num] + arr[i]
    maxSum = Math.max(maxSum, tempSum);
  }
  return maxSum;
}
```

### find longest distinct substring
```
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
```

### divide and conquer, find value in sorted arr using binary search
```
// divide and conquer, split large sorter arr into subset to find a value
function search(arr, val) {
  let min = 0,
    max = arr.length - 1;

  while(min <= max) { // run this until we reach the end or arr
    // calculate middle point
    let middle = Math.floor((min + max) / 2),
      currentElement = arr[middle];

    // if val is on the right side of midpoint, look at values to the right of midpoint
    if(arr[middle] < val) { 
      min = middle + 1;
    // if val is on the left side of midpoint, look at values to the left of midpoint
    } else if (arr[middle] > val) {
      max = middle - 1;
    } else {
      return middle;
    }
  }
  return -1;
}
```

### check for duplicates
```
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

OR USE A SET

function areThereDuplicates() {
  return new Set(arguments).size !== arguments.length;
}
```

### find values in sorted arr
```
// find pair of values where there avg is equal to target
// we can use divide and conquer using binary search
function averagePair(arr, num){
  let start = 0
  let end = arr.length-1;
  while(start < end){
    let avg = (arr[start]+arr[end]) / 2;
    if(avg === num) return true;
    else if(avg < num) start++
    else end--
  }
  return false;
}
```

### check for substring
```
// check is the char of one arg is a substr of the other arg
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
```

### check for dupe in an unsorted array
```
//since its unsorted, we cant use two pointers. we can push in a hashmap and check for vals > 2
function checkForDupe(str) {
  let hash = {};
  [...str].forEach(x => hash[x] = hash[x]+1 || 1);
  let isDupe = Object.values(hash).some((el) => el % 2 === 0);
  
  return isDupe;
};
```
