## Day 3

- Learned about the Sliding Window
  - This pattern involves creating a window which can either be an array or number from one position to another
  - Depending of the condition, the window increases or closes (and a new window is created)
  - Very useful for keeping track of a subset of data in an array/string etc

Example

Write a function called `maxSubarraySum` which accepts an array of integers and a number called `n`. The function should
calculate the maximum sum of `n` consecutive elements in the array.

```
maxSubarraySum([1,2,5,2,8,1,5], 2) // 10
maxSubarraySum([1,2,5,2,8,1,5], 4) // 17
maxSubarraySum([4,2,1,6], 1) // 6
maxSubarraySum([], 4) // null
```

There is a naive solution, which creates a temp variable, loops through the items, and then matches if the temp is more
than the max, if it is, then set the max and repeat. This is not a good solution because it creates the O(n²)
complexity, as long as the `n` grows, it grows exponentially.

```
function maxSubarraySum(arr, num) {
  if ( num > arr.length){
    return null;
  }
  var max = -Infinity;
  for (let i = 0; i < arr.length - num + 1; i ++){
    temp = 0;
    for (let j = 0; j < num; j++){
      temp += arr[i + j];
    }
    if (temp > max) {
      max = temp;
    }
  }
  return max;
}

maxSubarraySum([2,6,9,2,1,8,5,6,3],3)
```

Here comes the sliding window technique, which I'll explain below:

```
function maxSubarraySum(arr, num) {
  let maxSum = 0;
  let tempSum = 0;
  if (num > arr.length) {
    return null;
  }

  for (let i = 0; i < num; i++) {
    maxSum += arr[i];
  }

  tempSum = maxSum;

  for (let i = num; i < arr.length; i++) {
    tempSum = tempSum - arr[i - num] + arr[i];
    maxSum = Math.max(maxSum, tempSum);
  }

  return maxSum;

}
```

What happens is let's say we have:

`maxSubarraySum([2,6,9,2,1,8,5,6,3])`

Based of this array:

`[2,6,9,2,1,8,5,6,3]`

We don't have to go through 2, 6, 9, and then 6, 9, 2 etc.

But we calculate the sum of:

`[2,6,9...]`

Then, we just remove the first `2`, and add the next item in the array so:

`[-,6,9,2]`

If the next one is larger than the last, the `Math.max` will replace it.

At the end, we return the maxSum.
