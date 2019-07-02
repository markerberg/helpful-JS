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
const str = "hello";
const chars = {};

for (let x of str) {
  chars[x] = chars[x] + 1 || 1;
}

console.log(chars);
```
