coding interview bootcamp - algorithms & data structures

## BubbleSort - return array sorted from least to greatest
 ```
 // loop through array using nested forloops. Where the nested loop is smaller thant he first loop. We compare each value next to adjacent
 // value and swap the left side for the right side to make sure it sorts from least to greatest
 function bubbleSort(arr) {
  for (var i = 0; i < arr.length; i++) {
    for ( var j = 0; j < (arr.length - i -1); j++) {
      if (arr[j] > arr[j+1]) {
        var lesser = arr[j+1];
        arr[j+1] = arr[j];
        arr[j] = lesser;
      }
    }
  }

  return arr;
}
 ```
 
 ## Selectionsort
 ```
 // assume some value is the lowest. We then compare values in array to see which is actually lower
 function selectionSort(arr) {
  for (var i = 0; i < arr.length; i++) {
    let indexOfMin = i; // assume the lowest

    for (var j = i+1; j < arr.length; j++) {
      if (arr[j] < arr[indexOfMin]){
        indexOfMin = j;
      }
    }

    if (indexOfMin !== i) {
      let lesser = arr[indexOfMin];
      arr[indexOfMin] = arr[i];
      arr[i] = lesser;
    }
  }

  return arr;
}
 ```
 
 ## MergeSort- take two sorted arrays and joing them together in the correct order
 ```
 function merge(left, right) {
  var results = [];

  while (left.length && right.length) {
    if (left[0] < right[0]) {
      results.push(left.shift());
    } else {
      results.push(right.shift());
    }
  }

  return [...results, ...left, ...right];
}

function mergeSort(arr) {
  if(arr.length === 1) {
    return arr;
  }

  // split arr in half
  const center = Math.floor(arr.length/2);
  const left = arr.slice(0, center);
  const right = arr.slice(center);

  return merge(mergeSort(left), mergeSort(right));

}
 ```
 
 #### Another merge sort. we first make our merge() to combine and sort two arrays
 ```
 //  Step 1
 function merge(arr1, arr2) {
  let results = [];

  // start at beginning of each array arg
  let i = 0;
  let j = 0;

  // while theres data in both args, look for smaller value
  while (i < arr1.length && j < arr2.length) {
    if (arr2[j] > arr1[i]) {
      results.push(arr1[i]);
      i++;
    } else {
      results.push(arr2[j]);
      j++;
    }
  }
  // these two while loops cover case if there are extra values in an arg. Just push them to results
  return [...results, ...arr1, ...arr2];
}

// step 2
function mergeSort(arr) {
  // recursively split sorted arr into smaller arrays until length is 0 or 1
  // this allows us to split our arr into small values of 0 or 1
  if (arr.length <= 1) return arr;
  let mid = Math.floor(arr.length/2);
  let left = mergeSort(arr.slice(0, mid));
  let right = mergeSort(arr.slice(mid));
  // call our helper func to take the split arr and sort and merge them
  return merge(left, right);
}
 ```

## Quicksort - we grab a value and compare it, small nums go left. bigger nums go right. Repeat this process
```
// loop, if el less than pivot, swap it to left
// each loop that has value < pivot, increment counter
// we set the pivot to index[counter] so it right side of all lesser values

function swap(arr, i, j) {
  let temp = arr[i];
  arr[i] = arr[j];
  arr[j] = temp;
}

function pivot (arr, start=0, end=arr.length+1) {
  var pivot = arr[start];
  var swapIndex = 0; // keep track of the index to return

  // start loop after current value bc we dont need to compare them
  for (var i = 1; i < arr.length; i++) {
    if (pivot > arr[i]) { // check if pivot greater than each item and increment count
      swapIndex++;
      // whn we find item less than pivot, we increment swapIndex. and move
      // its index to our swapIndex value
      swap(arr, swapIndex, i);
    }
  }
  // at the end we swap start index with swapindex. so we put our number after "n" smaller indexes
  swap(arr, start, swapIndex); 
}

function quickSort(arr, left = 0, right = arr.length-1) {
  if (left < right) { // run loop until we break down to one arr length
    let pivotIndex = pivot(arr, left, right);
    // left
    quickSort(arr, left, pivotIndex-1);
    // right
    quickSort(arr, pivotIndex+1, right);
  }
  return arr;
}
```
