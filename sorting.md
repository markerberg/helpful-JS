coding interview bootcamp - algorithms & data structures

### BubbleSort - return array sorted from least to greatest
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
 
 ### Selectionsort
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
 
 ### MergeSort- take two sorted arrays and joing them together in the correct order
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