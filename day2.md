## Day 2

- Learned about the Multiple Pointers algorithm
  - Creating pointers or values that correspond to an index or position and move towards the beginning, end or middle
    based on a certain condition.

Let's say we have an array `[-4, -3, -2, -1, 0, 1, 2, 5]`

And, we get a challenge to write a function `sumZero` which accepts a sorted array of integers. The function should find
the first pair, where the sum is 0. Return an array that includes both values that sum to zero or undefined if a pair
doesn't exist.

```
  sumZero([-3, -2, -1, 0, 1, 2, 3]) // [-3, 3]
  sumZero([-3, -1, 0, 1, 2]) // [-1, 1]
  sumZero([-2, -1, 0, 1, 3]) // undefined
```

We could add a naive solution, looping and then adding a nested loop as well, which creates the O(n²) complexity.

Example:

```
function sumZero(arr){
  for (let i = 0; i < arr.length; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[i] + arr[j] === 0) {
        return [arr[i], arr[j]];
      }
    }
  }
}
```

This would have the O(n²) complexity.

A more robust solution would be using the multiple pointers, which moves the index either from the start, or the end,
eventually they'll catch up and find the pair if the pair exists.

```
function sumZero(arr){
    let left = 0;
    let right = arr.length - 1;
    while(left < right){
        let sum = arr[left] + arr[right];
        if(sum === 0){
            return [arr[left], arr[right]];
        } else if(sum > 0){
            right--;
        } else {
            left++;
        }
    }
}
```

Also, there's a challenge for example `countUniqueValues` which has this challenge:

Implement a function called countUniqueValues, which accepts a sorted array, and counts the unique values in the array.
There can be negative numbers in the array, but it will always be sorted.

```
countUniqueValues([1,1,1,1,1,2]) // 2
countUniqueValues([1,2,3,4,4,4,7,7,12,12,13]) // 7
countUniqueValues([]) // 0
countUniqueValues([-2,-1,-1,0,1]) // 4
```

Time Complexity - O(n) Space Complexity - O(n)

A solution would be to start with left with an index of 0, and right with 1, then move right until they don't match, if
they match, replace the item e.g.

```
 i
[1,1,2,2,3,4]
   j

 i
[1,1,2,2,3,4] // Found the mismatch!
     j

   i
[1,2,2,2,3,4] // i is now 1 (i++) and replaces the item
       j
```

We do this incrementally, until we reach to the end, then we return the `i` index + 1, which shows the length of the
unique array.
