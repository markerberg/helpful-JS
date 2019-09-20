## Two Sum- using hash map
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

## longest palindrome substring in string- using 
```
/** 
Idea is to loop through each item and call a function on them
the function will check its adjacent values and see if they are equal to eachother
if equal, we start to widen out window and look for more start&end index that are the same
**/
const longestPalindrome = (s) => {
  if (!s || s.length <= 1) {
    return s;
  }
  // temp assign a long value to compare to
  let longest = s.substring(0,1);

  for(let i=0; i < s.length; i++){
    // check the elements around each value for palindrone
    let temp = expand(s, i, i);
    if (temp.length > longest.length) {
      longest = temp;
    }
    // check for palindrones where the middle is the same char repeated 2x
    temp = expand(s, i ,i+1);
    if (temp.length > longest.length) {
      longest = temp;
    }
  }
  return longest;
}

const expand = (str, start, end) => {
  // create a window of text to look at. Keeps growing if the items are equal/palindrone
  while (start >= 0 && end <= str.length -1 && str[start] === str[end]) {
    start--;
    end++;
  }
  return str.substring(start+1, end);
}

console.log(longestPalindrome('banana'));
```
## find the maxSum. find continuous subarray with the largest sum and return value
we could also use divide and conquer here
```
var maxSubArray = function(n) {
  let currentSum = 0;
  let maxSum = 0;
  // loop through and track the current sum compared to finalsum
  for (let i=0; i < n.length; i++) {
    let currentNum = n[i];

    currentSum = Math.max((currentSum + currentNum), 0);
    maxSum = Math.max(currentSum, maxSum);
  }

  return maxSum;
}
```

## length of longest unique substring
```
/**
 * idea is to have a window of unique values. We start at 0, track each char in a map and loop through
 * the array. If we find a iteratee thats already in a map...we know its a duplicate so we calc our current
 * length without the duplicated value to check for maxlength. we also UPDATE the index of the duplicated
 * value in our map to reflect the latest index of the char 
 */
function lengthOfLongestSubstring(s) {
  let charMap = {},
    maxLength = 0,
    windowStart = 0;
   
  for (let i = 0; i < s.length; i++ ) {
    let endChar = s[i];

  if (charMap[endChar] >= windowStart) {
    windowStart = charMap[endChar] + 1;
  }

  charMap[endChar] = i;
  maxLength = Math.max(maxLength, i - windowStart + 1);
  }
  return maxLength;
}

console.log(lengthOfLongestSubstring('abcabcbb')); // 3 for 'abc'
console.log(lengthOfLongestSubstring('bbb')); // 1 for 'b'
```

## Valid parenthesis with a stack solution (lifo)
```
const validParren = s => {
  let stack = [],
    pairsHashMap = {"(":")", "{":"}", "[":"]"};

  for (let i = 0 ; i < s.length; i++) {
    let char = s[i];

    // if the value of iteratee in the hashmap exist, push to stack
    if(pairsHashMap[char]) {
      stack.push(char);
    } else if (pairsHashMap[stack.pop()] !== char) {
      return false;
    }
  }
  return stack.length === 0;
}

console.log(validParren('()[]{}'));
```
## group together anagrams
```
/**
 * we make an obj where key is anagram and val is the words. We need to
 * group together all words under the same anangram
 */
function groupAnagram(str) {
  let grouped = {};

  for (let i = 0; i < str.length; i++) {
    let word = str[i],
      key = word.split('').sort().join('');

      if(!grouped[key]) {
        grouped[key] = []
      };

      grouped[key].push(word);
  }
  return Object.values(grouped);
}

console.log(groupAnagram(['eat','tea','tan','ate']));
```
### isPalindrome
```
// O(n) time complexity
// think of palindrome as words where each half mirrors itself
// we create left and right pointer, left pointer starts at beginning.
// right pointer starts at end. Compare them for palindrome
function isPalindrome(s) {
  // sanitize
  s = s.toLowerCase().replace(/[\W_]/g, ''); //rm all alphanumeric nonchars 
  
  let left = 0;
  let right = s.length - 1;

  while (left < right) {
    if (s[left] !== s[right]) {
      return false;
    }

    left++;
    right--;
  }

  return true;
}
```

### anagram
```
// O(n) time complexity
function isAnagram(s,t) {
  if (s.length !== t.length) {
    return false;
  }

  let sCharMap = {};

  for(let i = 0; i < s.length; i++) {
    let sChar = s[i];

    sCharMap[sChar] = sCharMap[sChar] + 1 || 1;
  }

  for (let i = 0; i < t.length; i++) {
    let tChar = t[i];

    // if char in t isnt in s, return false
    // ALSO we reduce the value by 1 everytime we find a matching char in s
    // so if a t value is found but the s value is at 0 (meaning we've already covered all possible amounts of chars in s)
    // then the 0 value will get reutned here and will return false
    if (!sCharMap[tChar]) {
      return false;
    } else {
      // we found a matching char, so rm one index from that value
      // so we can tell that it was already accounted for in s
      sCharMap[tChar]--;
    }
  }
  return true;
}
```
### meeting rooms
```
// meeting rooms -> we need to check if any intervals intersect with eachother
// put start and end time in two seperate sorted arrays
// loop start arr and check if start arr (1 index ahead of current start) is
// less than the end arr (at the same index of start (not 1 ahead tho))
// if its less, that means they intersect

const canAttendMeeting = interval => {
  const starts = [],
    ends = [];

  for (let i = 0; i < interval.length; i++) {
    const subArray = interval[i];
    starts.push(subArray[0]); // push beginning keys
    ends.push(subArray[1]); // push eng values
  }

  // sort start and end from least to greatest
  starts.sort((a,b) => a - b);
  ends.sort((a,b) => a - b);

  for (let i = 0; i < starts.length; i++) {
    // if start at one index ahead is less than current end index
    if (starts[i+1] < ends[i]) return false;
  }

  return true;
}
```
