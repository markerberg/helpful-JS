### linkedlist
```
class Node {
  constructor(data, next = null) {
    this.data = data;
    this.next = next;
  }
}

class Linkedlist {
  constructor() {
    this.head = null;
  }

  // we insert the first node but dont replace the current head node
  // we need to make a new node with our data, set the new node.next to the current head
  // then set the head to point to the new node
  insertFirst(data) {
    const node = new Node(data, this.head);
    this.head = node;
  }

  // we get a refernece to the first node in our linkedlist
  // if there is a headnode, we keep looking through node.next until we reach the end and 
  // node.next is equal to null
  size() {
    let count = 0;
    let node = this.head;

    while(node) {
      counter++;
      node = node.next;
    }

    return counter;
  }
  // this.head will always point to the very first node in our linked list
  getFirst() {
    return this.head;
  }

  // we start with checking our first node. We go through the nodes and check if the 
  // .next value is defined or not
  getLast() {
    if (!this.head) {
      return null;
    }

    while(node) {
      if (!node.next) {
        // after we update the value of node, check if the current iteratee has null for the .next
        // that means were on our tail node...or the ending node
        return node;
      }
      node = node.next; // we start looking at EACH node
    }
  }

  // since linkedlist knows if any nodes exists via the head. if we set the head to null, the linkedlist
  // wont see or notice any nodes....as if it were cleared 
  clear() {
    this.head = null;
  }
  // we just need to point our head to the second node 
  removeFirst() {
    if (!this.head) {
      return;
    }

    // this.head returns a node and calling .next on the head node gives access to second node
    this.head = this.head.next; 
  }
}
```
