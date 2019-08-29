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
```
