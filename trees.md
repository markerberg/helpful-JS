## Trees
we can create nodes that reference its own data and its children. We know a node is a child of another node if it exists within the other
nodes children array
```
class Node {
  constructor(data) {
    this.data = data;
    this.children = [];
  }

  add(data) { // add child nodes and push to this node children[]
    this.children.push(new Node(data));
  }
  
  remove(data) {
    this.children = this.children.filter(node => {
      return node.data !== data;
    });
  }
}

class Tree {
  constructor() {
    this.root = null;
  }
}

traverseBF(fn) {
  const arr = [this.root]; // set root node in out arr to first node
  while(arr.length) {
    const node = arr.shift(); // pull out the first value in arr
    
    arr.push(...node.children); // push that first values children into arr
    fn(node); // call func on the current node and the while loop will run func on each node hereafter
  }
}

traverseDF(fn) { // depth first is the same process as bf, but we place children differently
  const arr = [this.root];
  while(arr.length) {
    const node = arr.shift()
    arr.unshift(...node.children); // push children to FRONT of arr so we process depth before the other levels
    fn(node);
  }
}
```

### Tree Interview Questions
given a root node, return array where each element is the number of nodes on each level
when we see something related to `the width of nodes at` each level. Its breadth first traverse
```
// we have to collections, one to store the width. The other to store the nodes at each level...as we loop through tree
function levelWidth(node) {
  const arr = [node, 'cliff'];
  const counters = [0];

  while (arr.length > 1) { // run when theres more than one node in here
    const node = arr.shift();

    // when the node we shift off is 'cliff', counters needs to know we've encountered the end of the row
    // so push a 0 on counters to symbolize a brand new level in our tree to increment after each node iterates
    if (node === 'cliff') {
      counters.push(0);
      arr.push('cliff'); // push cliff back on arr to seperate other incomming child nodes (on new levels)
    } else { // when node is an actual node and not a cliff, render children
      arr.push(...node.children); // push child values of node AFTER the cliff
      counters[counters.length - 1]++; // increament the counter after we shift off an actual node
    }
  }

  return counters;
}
```

### Binary Search Tree
```
class Node {
  constructor(data) {
    this.data = data;
    this.left = null;
    this.right = null;
  }

  // if we cannot insert new data at root, we recurse through different nodes in tree
  insert(data) {
    // delegate insertion to left side if theres already a left value
    if(data < this.data && this.left) {
      this.left.insert(data);
    } else if (data < this.data) { // case where we reach end of tree and left value dne, just make new node on left side
      this.left = new Node(data);
    } else if (data > this.data && this.right) { // if right side and data is greater than parent, insert on right
      this.right.insert(data);     
    } else if (data > this.data) { // case where reach end and rigth dne, just attach a new node
      this.right = new Node(data);
    }
  }
  
  contains(data) {
    if (this.data === data) {
      return this; // return this node if its the current node data
    }
  
    // start recursion based on value comparisons. Remember smaller child goes left & bigger goes right
    if(this.data < data && this.right) { // if current node is smaller than arg, move to rhs
      return this.right.contains(data);
    } else if (this.data > data && this.left) {
      return this.left.contains(data);
    }
  
    return null;
  }
}

// find if binary search tree contains target. If target number is smaller than node, that target most likely exists on the left side

```
