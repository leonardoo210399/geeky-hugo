---
title: "Question 242: Valid Anagram"
description: "meta description"
image: "images/post/post-2.png"
date: 2021-01-24T18:19:25+06:00
categories: ["artificial intelligence"]
tags: ["tech", "ai"]
type: "featured" # available types: [featured/regular]
draft: false
---
Sure, here's the final structure with the added option to copy code:

---

*Problem Statement:*

Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

*Example:*

plaintext
```
Input: s = "anagram", t = "nagaram"
Output: true

Input: s = "rat", t = "car"
Output: false
```

*Approach:*

### 1. Sorting Approach

This approach involves sorting both strings and comparing them. If both sorted strings are identical, then one string is an anagram of the other.

#### Algorithm:

1. Convert both strings to a list of characters.
2. Sort both lists.
3. Compare the sorted lists.
4. If they are equal, return `true`; otherwise, return `false`.

#### Code:

**Python:**
```python
def isAnagram(s: str, t: str) -> bool:
    return sorted(s) == sorted(t)
```
<button onclick="copyCode('python-sort')">Copy code</button>

**Javascript:**
```javascript
function isAnagram(s, t) {
    return s.split('').sort().join('') === t.split('').sort().join('');
}
```
<button onclick="copyCode('js-sort')">Copy code</button>

#### Complexity Analysis:

- *Time Complexity:* O(n log n) for sorting both strings, where n is the length of the strings.
- *Space Complexity:* O(n) to store the sorted versions of the strings.

### 2. Counting Characters Using HashMap

This approach counts the frequency of each character in both strings and then compares the counts.

#### Algorithm:

1. Check if the lengths of `s` and `t` are different. If they are, return `false`.
2. Create a dictionary to count the frequency of each character in `s`.
3. Iterate through `t` and decrement the count for each character.
4. If any character count goes below zero, return `false`.
5. After the loop, check if all counts are zero.
6. Return `true` if they are, otherwise return `false`.

#### Code:

**Python:**
```python
def isAnagram(s: str, t: str) -> bool:
    if len(s) != len(t):
        return False
    
    count = {}
    
    for char in s:
        count[char] = count.get(char, 0) + 1
    
    for char in t:
        if char not in count or count[char] == 0:
            return False
        count[char] -= 1
    
    return True
```
<button onclick="copyCode('python-hashmap')">Copy code</button>

**Javascript:**
```javascript
function isAnagram(s, t) {
    if (s.length !== t.length) {
        return false;
    }

    let count = {};

    for (let char of s) {
        count[char] = (count[char] || 0) + 1;
    }

    for (let char of t) {
        if (!count[char]) {
            return false;
        }
        count[char]--;
    }

    return true;
}
```
<button onclick="copyCode('js-hashmap')">Copy code</button>

#### Complexity Analysis:

- *Time Complexity:* O(n), where n is the length of the strings, as we only traverse each string once.
- *Space Complexity:* O(n) for the hashmap to store character counts.

### 3. Counting Characters Using Array

This approach counts the frequency of each character using an array instead of a hashmap.

#### Algorithm:

1. Check if the lengths of `s` and `t` are different. If they are, return `false`.
2. Create an array of size 26 (for each letter in the alphabet) initialized to zero.
3. Increment the count for each character in `s`.
4. Decrement the count for each character in `t`.
5. If any count goes below zero, return `false`.
6. If all counts are zero after processing both strings, return `true`.

#### Code:

**Python:**
```python
def isAnagram(s: str, t: str) -> bool:
    if len(s) != len(t):
        return False
    
    count = [0] * 26
    
    for char in s:
        count[ord(char) - ord('a')] += 1
    
    for char in t:
        count[ord(char) - ord('a')] -= 1
        if count[ord(char) - ord('a')] < 0:
            return False
    
    return True
```
<button onclick="copyCode('python-array')">Copy code</button>

**Javascript:**
```javascript
function isAnagram(s, t) {
    if (s.length !== t.length) {
        return false;
    }

    let count = new Array(26).fill(0);

    for (let i = 0; i < s.length; i++) {
        count[s.charCodeAt(i) - 97]++;
        count[t.charCodeAt(i) - 97]--;
    }

    for (let i = 0; i < 26; i++) {
        if (count[i] !== 0) {
            return false;
        }
    }

    return true;
}
```
<button onclick="copyCode('js-array')">Copy code</button>

#### Complexity Analysis:

- *Time Complexity:* O(n), where n is the length of the strings, as we only traverse each string once.
- *Space Complexity:* O(1), using a fixed size array of 26 elements for character counts.

*Conclusion:*

We explored three different approaches to solve the Valid Anagram problem. The sorting approach is simple but less efficient. The hashmap and array-based counting approaches offer linear time complexity and are more efficient. The array-based counting method is the most space-efficient solution, making it optimal among the three approaches.

<script>
function copyCode(id) {
    var code = document.getElementById(id).innerText.trim();
    navigator.clipboard.writeText(code).then(function() {
        alert("Code copied to clipboard!");
    }, function() {
        alert("Copy failed. Please try again.");
    });
}
</script>
