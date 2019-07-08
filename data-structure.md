# Data structure- stack
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

# Data structure- Queue
```
function priorityQueue() {
  var collection = [];
}

priorityQueue.prototype.printCollection = () => {
    console.log(this.collection);
  };
  
  // add to the queue based on the priority we assign
  priorityQueue.prototype.enqueue = (el) => {
    if(this.collection.length < 1) {
      this.collection.push(el);
    } else {
      // if its filled, push in the value based on priority
      for (var i=0; i<this.collection.length; i++) {
        var added=false;
        // check if the priority is more(less than) other elements
        if(el[1] < this.collection[i][1]) {
          this.collection.splice(i,0,el);
          added=true;
          break;
        }
      }
      if (!added) {
        this.collection.push(el);
      }
    }
  };
  
  priorityQueue.prototype.dequeue = () => {
    this.collection.pop();
  }
 ```
 ```
 class Queue {
  constructor() {
    this.data = [];
  }
  
  add(record) {
    this.data.unshift(record);
  }
  
  remove() {
    this.data.pop();
  }
}
```

# Data-structure Map
```
function myMap() {
  var collection = {};
  var count=0;

  // set
  this.set = (key, value) => {
    this.collection[key] = value;
  }
  // has
  this.has = (key) => {
    return (key in this.collection);
  }
  // get
  this.get = (key) => {
    return (key in this.collection) ? this.collection[key] : null;
  }
  // delete
  this.delete = (key) => {
    if (key in this.collection) {
      delete collection[key];
    }
  }
  // values
  this.values = (key) => {
    var results = new Array();
    for(let key of Object.keys(this.collection)) {
      results.push(this.collection[key]);
    }
    return (results.length > 0) ? results : '0';
  }
}
```
