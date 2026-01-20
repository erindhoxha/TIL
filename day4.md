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
