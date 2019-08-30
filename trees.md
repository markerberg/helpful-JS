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
