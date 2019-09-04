```
var fruitarray = [];
fruitarray[0] = ['strawberry-','orange', 'peach','raspberry'];
fruitarray[1] = ['lime', 'peach', 'peach','banana','raspberry'];
fruitarray[2] = ['tangerine','apricot','peach'];
fruitarray[3] = ['raspberry','raspberry','raspberry','kiwi', 'apricot'];
```

### flatten complex array to simple array
```
var flattenedFruits = fruitarray.concat.apply([], fruitarray);
```

### remove duplicates so only unique values are in array
```
var nonDuplicatedFruits = flattenedFruits.reduce((result,nextItem)=>result.includes(nextItem) ? result : result.concat(nextItem),[]);
```

can also remove duplicates with Set
```
var nonDuplicatedFruits = Array.from(new Set(flattenedFruits));   OR    [...new Set(flattenedFruits)]
```

### push all duplicated fruits into a nested object where the key is the fruit and the value is an array of the duplicated fruits
```
var formattedFruits = flattenedFruits.reduce((allFruits, fruit) => {
  allFruits[fruit] = allFruits[fruit] || [];
  allFruits[fruit].push(fruit);
  return allFruits;
}, {});
```

`console.log(flattenedFruits);`
`console.log(nonDuplicatedFruits);`
`console.log(formattedFruits);`

### use .sort() on array of numbers
```
[6,7,22,12,334,56,88,9,1,12,41,78,55,2,95,23].sort((num1, num2) => {
  return num1 - num2; // for low to high
  // return num2 - num1 // for high to low
});
```
