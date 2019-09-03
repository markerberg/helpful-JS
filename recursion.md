### power of recursion
```
function power(base, exponent){
    if(exponent === 0) return 1;
    return base * power(base,exponent-1);
}
```

### factorial recursion
```
function factorial(x){
   if (x < 0 ) return 0;
   if (x <= 1 ) return 1;
   return x * factorial(x-1);
}
```

### take array and return product of all of them
```
function productOfArray(arr) {
    if(arr.length === 0) {
        return 1;
    }
    return arr[0] * productOfArray(arr.slice(1));
}
```

### recursive add from 0 to number
```
function recursiveRange(x){
   if (x === 0 ) return 0;
   return x + recursiveRange(x-1);
}
```

### reverse string
```
function reverse(str){
	if(str.length <= 1) return str;
	return reverse(str.slice(1)) + str[0];
}
```

### palindrone
```
function isPalindrome(str){
    if(str.length === 1) return true;
    if(str.length === 2) return str[0] === str[1];
    // if first and last same, slice everything betweena nd check first and last again and again
    if(str[0] === str.slice(-1)) return isPalindrome(str.slice(1,-1));
    return false;
}
```

### check if the callback works on any arr item
```
function someRecursive(array, callback) {
    if (array.length === 0) return false;
    if (callback(array[0])) return true;
    // take out first item and call again to check
    return someRecursive(array.slice(1),callback);
}
```

### return sum of all even numbers in an object (the obj might be nested)
```
function nestedEvenSum (obj, sum=0) {
    for (var key in obj) {
        if (typeof obj[key] === 'object'){
            sum += nestedEvenSum(obj[key]);
        } else if (typeof obj[key] === 'number' && obj[key] % 2 === 0){
            sum += obj[key];
        }
    }
    return sum;
}
```
