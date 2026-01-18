## Day 2

- Learned about the Multiple Pointers algorithm
  - Creating pointers or values that correspond to an index or position and move towards the beginning, end or middle
    based on a certain condition.

Let's say we have an array [-4, -3, -2, -1, 0, 1, 2, 5]

And, we get a challenge to write a function sumZero which accepts a sorted array of integers. The function should find
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
