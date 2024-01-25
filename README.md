# Leetcode solutions

I am following [neetcode](https://neetcode.io/practice).

- [Arrays and hashing](#arrays-and-hashing)
    - [217. Contains duplicate](#217-contains-duplicate) - easy
    - [242. Valid anagram](#242-valid-anagram) - easy
    - [1. Two sum](#1-two-sum) - easy

## Arrays and hashing

### 217. Contains duplicate

#### The problem

Given an integer aray `nums`, return `true` if any value appears at least twice in the array, and return `false` if every element is distinct.

#### Brute force

- time complexity: `O(n**2)` - nested loops iterating through the array
- space complexity: `O(1)` - constant space, no additional data structures used.

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        for i in range (0, len(nums)-1):
            for j in range(1, nums):
                if i == j:
                    return True
        return False
```

#### Sort

- at first, we will sort the array, and then check if any adjacent elements are equal, if it is equal we can return `True`
- time complexity: `O(n*logn)` - due to the sorting operation
- space complexity: `O(1)` - constant space, no additional data structures used (assuming in-place sorting)

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        nums = sorted(nums)
        for i n range(0, len(nums)-1):
            if nums[i] == nums[i+1]:
                return True
        return False
```

#### Hash set

- I create a set that keeps track of numbers that I have seen
- I have a pointer starting at the beggining and I add the number that is not in the set yet to the set, if it is there already we can return `True`
- time complexity: `O(n)` - single pass through the array
- space complexity: `O(n)` - space required for the set to store unique elements

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        my_set = set()
        for num in nums:
            if num in my_set:
                return True
            my_set.add(num)
        return False
```

#### Hash map

- the hash map approach is similar to the hash set approach but also keeps track of the count of occurences for each element
- it uses a hash map to store the elements as keys and their counts as values
- if a duplicate element is encountered (count greated than or equal to 1) it returns `True`
- time complexity: `O(n)` - single pass through the array
- space complexity: `O(n)` - space required for the set to store unique elements and their counts

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        my_dict = {}
        for num in nums:
            if num in my_dict and my_dict[num]>=1:
                return True
            my_dict[num] = my_dict.get(num, 0) + 1
        return False
```

### 242. Valid anagram

#### The problem

Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

#### Sorting

- the most straightforward approach is to compare if the sorted versions of both strings are equal
- if the sorted strings are the same, it means they are anagrams
- time complexity: `O(n*logn)` - due to the sorting operation
- space complexity: `O(n)` - space to store the sorted versions of the strings

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return sorted(s) == sorted(t)
```

#### Counter

- build a counter dictionary for string `s` by counting the occurrences of each character
- time complexity: `O(n)` - building the counters for both strings requires iterating through each character once
- space complexity: `O(n)` - space required for the counters

```python
from collections import Counter

class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return Counter(s) == Counter(t)
```

#### Hash map

- we can use hash maps to keep track of the frequency of each character in both strings
- if the frequencies are the same for both strings, they are anagrams
- time complexity: `O(n)` - iterating through both strings once
- space complexity: `O(n)` - space required for the hash map to store the frequency of characters

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False

        char_count = {}

        for char in s:
            char_count[char] = char_count.get(char, 0) + 1

        for char in t:
            if char not in char_count or char_count[char] == 0:
                return False
            char_count[char] -= 1

        return True
```

### 1. Two sum

#### The problem

Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`.

You may assume that each input would have exactly one solution, and you may not use the same element twice. You can return the answer in any order.

#### Brute force

- iterate through each element in the array
- for each element, iterate through the rest of the array to find a pair that adds up to the target
- if found, return the indices of the two elements
- time complexity: `O(n**2)` - the nested loops iterate through the entire array.
- space complexity: `O(1)` - no additional space is used.

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(0, len(nums) - 1):
            for j in range(1, len(nums)):
                if target == nums[i] + nums[j]:
                    return i, j
```

#### Hash map

 - use a hash map to store the elements and their indices as we iterate through the array
 - for each element, check if the complement (target - current element) is already in the hash map
 - if found, return the indices
 - time complexity: `O(n)` - we iterate through the array once
 - space complexity: `O(n)` - we might need to store all elements in the array

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        searched = {}
        for index, num in enumerate(nums):
            comlement = target - num
            if wanted in searched:
                return index, searched[complement]
            searched[num] = index
```