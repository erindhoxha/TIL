## Day 4

- Challenges

Frequency Counter / Multiple Pointers - `areThereDuplicates`

Implement a function called, areThereDuplicates which accepts a variable number of arguments, and checks whether there
are any duplicates among the arguments passed in.

Examples:

```
areThereDuplicates(1, 2, 3) // false
areThereDuplicates(1, 2, 2) // true
areThereDuplicates('a', 'b', 'c', 'a') // true
```

My solution:

```
function areThereDuplicates(...args) {
    let looker = {};
    for (const char of args) {
       if (looker[char]) {
         return true;
       } else {
         looker[char] = true;
       }
    }
    return false
}
```

There is another challenge:

Frequency Counter - constructNote Write a function called constructNote, which accepts two strings, a message and some
letters. The function should return true if the message can be built with the letters that you are given, or it should
return false.

Assume that there are only lowercase letters and no space or special characters in both the message and the letters.

My solution:

```
function constructNote(note, letters){
  let looker = {};

  for (const char of letters) {
    looker[char] = (looker[char] || 0) + 1;
  }

  for (const char of note) {
    if (!looker[char]) {
      return false;
    }
    looker[char]--;
  }
  return true;
}
```

Frequency Counter - findAllDuplicates Given an array of positive integers, some elements appear twice and others appear
once. Find all the elements that appear twice in this array. Note that you can return the elements in any order.

```
function findAllDuplicates(arr){
  let freq = {};
  let dupes = [];
  for (const char of arr) {
    freq[char] = freq[char] ? freq[char] + 1 : 1;
  }

  for (let key in freq) {
    if (freq[key] > 1) {
      dupes.push(Number(key));
    }
  }
  console.log(dupes);
  return dupes;
}
```

Multiple Pointers - averagePair Write a function called averagePair. Given a sorted array of integers and a target
average, determine if there is a pair of values in the array where the average of the pair equals the target average.
There may be more than one pair that matches the average target.

My solution:

```
function averagePair(arr, avgParam){
  let left = 0;
  let right = arr.length - 1;

  while (left < right) {
    if (left === right) {
      return false;
    }
    let avg = (arr[left] + arr[right]) / 2;
    if (avg === avgParam) {
      return true;
    }
    if (avg > avgParam) {
      right--;
    } else {
      left++;
    }
  }

  return false;
}

averagePair([1,1,2,4,5], 3);
```

Multiple Pointers - isSubsequence Write a function called isSubsequence which takes in two strings and checks whether
the characters in the first string form a subsequence of the characters in the second string. In other words, the
function should check whether the characters in the first string appear somewhere in the second string, without their
order changing.

My solution:

```
function isSubsequence(sub, sequence) {
  let left = 0;
  let right = 0;

  while (left < sub.length && right < sequence.length) {
    if (sub[left] === sequence[right]) {
      left++;
    }
    right++;
  }

  return left === sub.length;
}
```

Frequency Counter / Multiple Pointer - findPair Given an unsorted array and a number n, find if there exists a pair of
elements in the array whose difference is n. This function should return true if the pair exists or false if it does
not.

```
function findPair(arr, num) {
  let sortedArr = arr.sort((a, b) => a - b)
  let left = 0;
  let right = 1;

  while (left < arr.length && right < arr.length) {
    let leftValue = sortedArr[left];
    let rightValue = sortedArr[right];

    if (left !== right && Math.abs(rightValue - leftValue) === Math.abs(num)) {
      return true;
    }
    else if (Math.abs(rightValue - leftValue) < Math.abs(num)) {
      right++;
    } else {
      left++;
    }
  }

  return false;
}
```

With frequency (also x - num = y checker)

```
function findPair(arr, num) {
  if (!arr.length) return false;

  if (num === 0) {
    const seen = new Set();
    for (const x of arr) {
      if (seen.has(x)) return true;
      seen.add(x);
    }
    return false;
  }

  const set = new Set(arr);
  for (const x of set) {
    if (set.has(x - num)) return true;
  }

  return false;
}
```
