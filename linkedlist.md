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
  
  insertFirst2(data){
    this.insertAt(data, 0);
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
  
  getLast2() {
    return this.getAt(this.size() - 1);
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
  
  removeLast() {
    // means list is empty
    if (!this.head) {
      return;
    }

    // means list only has one node, so we just clear the list
    if (!this.head.next) {
      this.head = null;
      return;
    }

    // we have two temp vars that points to 2 adjacent nodes. If the node on right
    // has .next == null, then its the last one. So we just set the node on the left
    // to have next=null and rm last node
    let previous = this.head;
    let node = this.head.next;
    while(node.next) {
      previous = node;
      node = node.next;
    }
    prev.next = null; // when while breaks bc our next node has .next of null, we set prev to null.
  }
  
  insertLast(data) {
    const last = this.getLast(); // get the last node using a method we made
  
    if (last) {
      // if theres last node, set the last node.next to the new current node
      last.next = new Node(data);
    } else {
      // last node DNE so list is empty. Set head to the new current node
      this.head = new Node(data);
    }
  }
  
  getAt(index) {
    let counter = 0;
    let node = this.head;
  
    while (node) {
      if(counter === index) { // return when we loop on a node position === index
        return node;
      }
      counter++; // increment count to continue the loop and mark our position
      node = node.next; // to iterate to the next node, we set current node === .next node
    }
  
    return null; // case if we ask for an index that is greater than our list size
  }
  
  removeAt(index) {
    // we can use getAt method to fetch the node BEFORE our target index. Just set the
    // beforeNode.next to look at the beforeNode.next.next
    if (!this.head) {
      return;
    }
  
    // if we want to remove the head el, just set the head to point to the second el
    if (index === 0) { 
      this.head = this.head.next;
      return;
    }
  
    const previous = this.getAt(index - 1);
    if (!previous || !previous.next) { // handle case where we ask for index greater than size of list
      return;
    }
    previous.next = previous.next.next; // set it to the current next.next so it skips a node
  }
  
  insertAt(data, index) {
    if (!this.head) { // if empty, set head to new node
      this.head = new Node(data);
      return;
    }
  
    // if first index, make new node pointing to the old/current head. And set the head to point to the new node
    if (index = 0) { 
      this.head = new Node(data, this.head);
      return;
    }
    
    // for inserting node, we need to find the index of 1 less than the target index. Then use that prevNode.next to set our new node
    // create new node, point it to the prevNode.next (the node after our previous one) and then point prev to the new node
    const previous = this.getAt(index - 1) || this.getLast(); // OR account for if an index is out of bound. We default to last node in list
    const node = new Node(data, previous.next); // our newNode will go between prev and its .next 
    previous.next = node; // so once we set newNode.next = prev.next, we set prev.next = newNode
  }
  
  forEach(fn) { // we can apply callback func to each node, while there is a node, and goto the next node to run callbcack again
    let node = this.head;

    while (node) {
      fn(node);
      node = node.next;
    }
  }

}
```
