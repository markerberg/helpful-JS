# Data structure- stack
### Palidrome
```
var word = 'racecar',
  revWord;
  
revWord = [...word].reverse().join('');
word === revWord ? 'Palidrome' : 'not';
```

### Make your own stack
```
var Stack = function() {
  this.count = 0;
  this.storage = {};
  
  // push
  this.push = function(value) {
    this.storage[this.count] = value;
    this.count++;
  }
  
  // pop
  this.pop = function() {
    this.count--;
    var res = this.storage[this.count];
    delete this.storage[this.count];
    return res;
  }
  
  this.size = function() {
    return this.count;
  }
}

var mark = new Stack();
mark.push(85)
mark.pop();
```
