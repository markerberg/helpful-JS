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

### character map..key is the letter, value is the amount of times they appear in string
```
var str = "he3llllo0ooo0o",
  chars = {},
  max = 0,
  maxChar;

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
