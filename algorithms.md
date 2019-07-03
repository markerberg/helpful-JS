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
    return x === str[str.length - 1 - i]; // or use reverseString() from above
  })
}
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
