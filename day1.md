## Day 1

- Learned about the **Frequency Counter** pattern.
  - Example: using objects like `freq1`, `freq2` to count occurrences.
  - This approach is more efficient (O(3n)) compared to using nested loops (O(n²)).

- Learned more about the **complexity of O(n)** (linear time) and **O(n²)** (quadratic time).
  - O(4n) is considered the same as O(n) in Big O notation (constants are ignored).
  - Nested loops usually result in O(n²) complexity.

- Learned about **O(log n)** (logarithmic time) and why it's efficient.
  - Algorithms like binary search use O(log n) time.
  - With each step, the problem size is divided (e.g., in half), making it much faster for large inputs.

I added this solution for the anagram challenge:

```
function validAnagram(str1, str2) {
  const freq1 = {};
  const freq2 = {};

  for (const char of str1) {
    freq1[char] = freq1[char] + 1 || 0;
  }

  for (const char of str2) {
    freq2[char] = freq2[char] + 1 || 0;
  }

  for (let key in freq1) {
    if (!(key in freq2)) {
      return false;
    }
    if (freq2[key] !== freq1[key]) {
      return false;
    }
  }
  return true;
}
```

There's another more efficient solution that is:

```
function validAnagram(first, second) {
  if (first.length !== second.length) {
    return false;
  }

  const lookup = {};

  for (let i = 0; i < first.length; i++) {
    let letter = first[i];
    // if letter exists, increment, otherwise set to 1
    lookup[letter] ? lookup[letter] += 1 : lookup[letter] = 1;
  }
  console.log(lookup)

  for (let i = 0; i < second.length; i++) {
    let letter = second[i];
    // can't find letter or letter is zero then it's not an anagram
    if (!lookup[letter]) {
      return false;
    } else {
      lookup[letter] -= 1;
    }
  }

  return true;
}

// {a: 0, n: 0, g: 0, r: 0, m: 0,s:1}
validAnagram('anagrams', 'nagaramm')
```

This explains that we don't have to check for the character itself, but the frequency of it, which if the frequency
doesn't match, then the anagram doesn't match as well.
