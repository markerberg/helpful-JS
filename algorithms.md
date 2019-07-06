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
