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
# Data structure - Set
```
function mySet() {
  var collection = [];
  // has
  this.has = (x) => {
    return collection.includes(x);
  }
  // values
  this.values = () => {
    return collection;
  }
  // add if the value doesnt exist already
  this.add = (y) => {
    if(!this.has(y)) {
      collection.push(y);
      return true;
    }
    return false
  }
  // remove
  this.remove = (r) => {
    if(this.has(r)) {
      let index = collection.indexOf(r);
      collection.splice(index, 1);
      return true;
    }
    return false;
  }
}

  // union -> combine all in one, no repeats
  mySet.prototype.union = (otherSet) => {
    var newUnion = [...new Set([...otherSet, ...collection])];
    return newUnion;
  }
  
  // intersection -> grab elements from both arrays
  mySet.prototype.intersection = (otherSet) => {
    var interSet;
    return interSet = otherSet.filter(x => collection.includes(x));
  }
  
  // difference
  mySet.prototype.difference = (otherSet) => {
    var diff;
    return diff = otherSet.filter(x => !collection.includes(x));
  }
  
  // symmetrical difference
  mySet.prototype.symDiff = (otherSet) => {
    var symdiff;
    return symDiff = otherSet.filter(x => !collection.includes(x))
                             .concat(collection.filter(y => !otherSet.includes(y)));
  }
```