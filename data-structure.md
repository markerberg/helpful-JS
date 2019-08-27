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

```
class Stack() {
  constructor() {
    this.data = [];
  }
  
  push(record) {
    this.data.push(record);
  }
  
  pop() {
    return this.data.pop();
  }
  
  peek() {
    return this.data[this.data.length - 1];
  }
}
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
  
  peek() {
    return this.data[this.data.length - 1];
  }
}
```
## weave 2 queues
```
const weave = (sourceOne, sourceTwo) => {
  // create a queue container
  let q = new Queue();
  
  // while there is an item in first source or an item in second source
  while (sourceOne.peek() || sourceTwo.peek()) {
    // if there is an item in source one 
    if (sourceOne.peek()) {
      // remove the item from source one and add it to queue 
      q.add(sourceOne.remove());
    }
    
    // if there is an item in source two
    if (sourceTwo.peek()) {
      // remove the item from source two and add it to queue 
      q.add(sourceTwo.remove());
    }
  }
  
  // return the queue
  return q;
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

### create a queue using stacks
```
// we have two stacks and we pop over stacks and push those values between eachother
// we keep doing this so we mimic the FIFO style of queues
class QueueFromStacks () {
  constructor() {
    this.first = new Stack();
    this.second = new Stack();
  }
  
  add(record) {
    this.first.push(record);
  }
  
  remove() {
    while (this.first.peek()) {
      this.second.push(this.first.pop());
    }
    
    const record = this.second.pop();
    
    while (this.second.peek()) {
      this.first.push(this.second.pop());
    }
    
    return record;
  }
  
  peek() {
    while (this.first.peek()) {
      this.second.push(this.first.pop());
    }
    
    const record = this.second.peek();
    
    while (this.second.peek()) {
      this.first.push(this.second.pop());
    }
    
    return record;
  }
}
```
### Linked List
https://www.udemy.com/coding-interview-bootcamp-algorithms-and-data-structure/learn/lecture/8547074#overview
