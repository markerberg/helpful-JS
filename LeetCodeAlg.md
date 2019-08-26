## Two Sum
```
/** Idea is to iterate over our array once and use a hash to store all the values we've already gone over. 
Each time we iterate we push our value into a hash so we know that we already looped through this item in our array.
Two Sum means we need to find values that add together to make up our target. So if we subtract each item in the array 
from our target, we know EXACTLY what diffNumer in our array we need to look for(what number in our hash we need to look for).
So after each time we iterate, check if the current diffNumber exists within our hash, if so that means we found the other num
within our array (that was already iterated over) that adds with our current value to equal our target. **/

var twoSum = function(nums, target) {
    var hash = {};
    var sums = [];

    for (var i = 0; i< nums.length; i++) {
      var difference = target - nums[i];
      
      if(hash[difference] !== undefined) {
          sums.push(nums[i], difference);
      }
        
      hash[nums[i]] = nums[i];
    }
    
    return sums;
};

```
