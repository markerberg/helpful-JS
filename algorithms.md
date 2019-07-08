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

fib = memoize(fib);
```
