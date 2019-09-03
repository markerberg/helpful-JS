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
