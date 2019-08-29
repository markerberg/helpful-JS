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

## LinkedList Interview Question
Find the middle point of a linkedlist without using a counter or retreiving the size of the list. Only iterate.
But If even number of elements, return node at the end of first half of list
```
// use two vars. slow travels 1 space and the fast travels twice as fast. When the fast reaches the end(bc next is equal to null and breaks the loop), slow is at the middle of the list since it travels half as fast as fast does

function midpoint(list) {
  // both vars start at the same point but move at different speeds
  var slow = list.getFirst();
  var fast = list.getFirst();

  while(fast.next && fast.next.next) {
    slow = slow.next; // move slow over 1 space to the next variable
    fast = fast.next.next // move fast over twice as fast as slow moves
  }

  // since slow moves half the speed of fast, when fast determines the end of list is coming up
  // we just need to return the value of slow, to know the middle. Since its half of what fast is
  return slow; 
}
```
Given a linked list, return true if its circular(meaning theres no tail)
```
// use same approach of using two seperate vars starting at same position that will move differently. Slow which moves 1. Fast which moves 2. Now we loop through and move each vars along. If we get to a point where Slow === Fast, its a circular list because the two vars (moving at seperate speeds) point to the same node.
function circular(list) {
  let slow = list.getFirst();
  let fast = list.getFirst();

  while (fast.next && fast.next.next) { //test for circular list. nothing should point to null
    slow = slow.next;
    fast = fast.next.next;

    if (slow === fast) { // if slow is same object in mem as fast, its a cirular list
      return true;
    } 
  }
  return fasle; // if our next values return null...we dont have a circular list
}
```
Given a linked list and an integer, n. return el that is n spaces from last node in list. Dont use size method
```
// use two seperate vars, slow and fast. Point them at first node. Move fast over n positions and then move both fast and slow over 1 position each until fast is at the end. When fast is at the end, slow will be n positions from the end as we wanted

function fromLast(list, n) {
  let slow = list.getFirst();
  let fast = list.getFirst();

  while(n>0) { // we move the fast var over n nodes
    fast = fast.next;
    n--;
  }

  while(fast.next) { // while the fast var hasn't reached the end of list, move both vars over 1 space togehter
    slow = slow.next; // we set slow equal to next node
    fast = fast.next; // set fast equal to next node
  }
  // when we break out of the loop bc fast is at the end of the list,
  // slow will be at n positions from the end. Bc we first moved fast over n positions
  // then we moved fast and slow over at the same pace until we got fast to be at the end
  return slow;
}
```
