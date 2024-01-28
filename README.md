# Leetcode solutions

I am following [NeetCode](https://neetcode.io/practice) list of 150 leetcode problems.

Feel free to add any solution that has not been mentioned yet.

## Content

- [Arrays and hashing](#arrays-and-hashing)
    - [217. Contains duplicate](#217-contains-duplicate) - easy
    - [242. Valid anagram](#242-valid-anagram) - easy
    - [1. Two sum](#1-two-sum) - easy
    - [49. Group anagrams](#49-group-anagrams) - medium
- [Two pointers](#two-pointers)
    - [125. Valid palindrome](#125-valid-palindrome) - easy
    - [167. Two sum II - input array is sorted](#167-two-sum-ii---input-array-is-sorted) - medium


## Arrays and hashing

### 217. Contains duplicate 

#### The problem

Given an integer aray `nums`, return `true` if any value appears at least twice in the array, and return `false` if every element is distinct.

```
Input: nums = [1,2,3,1]
Output: true
```

#### Brute force

- **time complexity:** `O(n^2)` - nested loops iterating through the array
- **space complexity:** `O(1)` - constant space, no additional data structures used.

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
- **time complexity:** `O(n*logn)` - due to the sorting operation
- **space complexity:** `O(1)` - constant space, no additional data structures used (assuming in-place sorting)

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
- **time complexity:** `O(n)` - single pass through the array
- **space complexity:** `O(n)` - space required for the set to store unique elements

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
- **time complexity:** `O(n)` - single pass through the array
- **space complexity:** `O(n)` - space required for the set to store unique elements and their counts

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

```
Input: s = "anagram", t = "nagaram"
Output: true
```

#### Sorting

- the most straightforward approach is to compare if the sorted versions of both strings are equal
- if the sorted strings are the same, it means they are anagrams
- **time complexity:** `O(n*logn)` - due to the sorting operation
- **space complexity:** `O(n)` - space to store the sorted versions of the strings

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return sorted(s) == sorted(t)
```

#### Counter

- build a counter dictionary for string `s` by counting the occurrences of each character
- **time complexity:** `O(n)` - building the counters for both strings requires iterating through each character once
- **space complexity:** `O(n)` - space required for the counters

```python
from collections import Counter

class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return Counter(s) == Counter(t)
```

#### Hash map

- we can use hash maps to keep track of the frequency of each character in both strings
- if the frequencies are the same for both strings, they are anagrams
- **time complexity:** `O(n)` - iterating through both strings once
- **space complexity:** `O(n)` - space required for the hash map to store the frequency of characters

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

```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

#### Brute force

- iterate through each element in the array
- for each element, iterate through the rest of the array to find a pair that adds up to the target
- if found, return the indices of the two elements
- **time complexity:** `O(n^2)` - the nested loops iterate through the entire array
- **space complexity:** `O(1)` - no additional space is used

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
 - **time complexity:** `O(n)` - we iterate through the array once
 - **space complexity:** `O(n)` - we might need to store all elements in the array

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

### 49. Group anagrams

#### The problem

Given an array of strings `strs`, group the anagrams together. You can return the answer in any order. An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

```
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```

#### Brute force

- for each word in the input array (`strs`) we count the occurrences of each character in the word
- the code then iterates over each word in the input array (`strs`) and compares it with other words to identify anagrams
- an `char_count_in_words` dictionary is used to store the character counts for each non-empty word
- as words are compared, groups of anagrams are formed and added to the `anagrams` list
- the `processed_words` set is used to keep track of words that have already been processed to avoid redundant comparisons
- special cases, such as empty strings and single-character words, are considered separately and added to the final output (`anagrams`)
- the output is a list of lists, where each inner list represents a group of anagrams
- **time complexity:** `O(n^2)` - the nested loops iterate through the entire array
    - the first loop: `O(n*L)`, where `n` is the length of `strs`, and `L` is the maximum length of a word
    - the second loop: `O(n^2)`
    - handling empty strings and single-character words: `O(n)`
- **space complexity:** `O(n*L)` - space required for the dictionary and outputs lists
    - `char_count_in_words`: `O(n*L)`
    - `processed_words` set: `O(n)`
    - `anagrams` list: `O(n*L)`

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        anagrams = []
        char_count_in_words = {}
        same_letters = {}
        empty = []

        # create dictionary 
        for word in strs:
            if word == '':
                empty.append(word)
            elif len(word)== 1:
                same_letters[word] = same_letters.get(word, 0) + 1
            else:
                char_count = {}
                for char in word:
                    char_count[char] = char_count.get(char, 0) + 1
                char_count_in_words[word] = char_count

        # compare words in dictionary
        processed_words = set()
        for i, word in enumerate(strs):
            if word in processed_words:
                continue
            if word == '':
                continue
            elif len(word) == 1:
                continue
            else:
                output = []
                output.append(word)
                for j, another_word in enumerate(strs):
                    if i == j:
                        continue
                    try:
                        if char_count_in_words[word] == char_count_in_words[another_word]:
                            output.append(another_word)
                            processed_words.add(another_word)
                            continue
                    except:
                        pass
                anagrams.append(output)

        # special cases
        if empty:
            anagrams.append(empty)
        if same_letters:
            for letter in same_letters:
                same_letters_list = []
                how_many = same_letters[letter]
                for i in range(how_many):
                    same_letters_list.append(letter)
                anagrams.append(same_letters_list)

        return anagrams
```

#### Hash map

- initialize an empty dictionary called `anagram`
- iterate through each word in the `strs` list
- for each word, sorts characters alphabetically and creates a `sorted_word` variable.
- if `sorted_word` is already a key in the `anagram` dictionary, it appends the original word to the list associated with that key
- if `sorted_word` is not present in the dictionary, it creates a new key-value pair where the key is `sorted_word` and the value is a list containing the current word
- finally, return the values from the `anagram` dictionary, which represents the grouped anagrams
- **time complexity:** `O(n*L*logL)` - due to the sorting of characters in each word
- **space complexity:** `O(n*L)` - the space required for the `anagram` dictionary

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        anagrams = {}
        for word in strs:
            sorted_word = ''.join(sorted(word))
            if sorted_word in anagrams:
                anagrams[sorted_word].append(word)
            else:
                anagrams[sorted_word] = [word]
        return anagrams.values()
```

The same approach can be implemented as:

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        anagrams = collections.defaultdict(list)
        for word in strs:
            sorted_word = ''.join(sorted(word))
            anagrams[sorted_word].append(word)
        return anagrams.values()
```

We use a `defaultdict` because it allows us to initialize a list for a key that doesn't exist yet. In this case, each key in the `defaultdict` represents a unique sorted representation of characters (anagram group). If we used a regular dictionary and tried to append words to a non-existing key, it would raise a `KeyError`. The defaultdict simplifies the process of creating and updating lists associated with each sorted form.

#### Counter

- use a dictionary to store lists of anagrams based on their character count representation
- calculate the count of each character in the string
    ```python
    for char in word:
        count[ord(char) - ord("a")] += 1
    ```
    - `ord(char)` returns the Unicode code point of the character `char`
    - `ord("a")` returns the Unicode code point of the character `"a"`
    - the subtraction `ord(char) - ord("a")` gives the relative position of the character in the alphabet
    - for example, if `char` is `"a"`, it increments `count[0]`, if `char` is `"b"`, it increments `count[1]`, and so on
- use a tuple of character counts (the `count` array) as a key to group anagrams (tuples are hashable, making them suitable for use as keys in a dictionary)
- finally, return the values (anagram groups) of the dictionary
- **time complexity:** `O(n*L)` - we iterate through each string and, for each character in the string, perform constant-time operations
    - iterating through each word: `O(n)`
    - character counting: `O(L)`
    - tuple of character counts as key: `O(1)`
    - appending to `anagram`: `O(1)`
    - returning values: `O(n)`
- **space complexity:** `O(n*L)` - the space required for the `anagram` dictionary
    - `count` array: `O(1)` since the array has a constant length
    - `anagram` defaultdict: `O(n)` since in the worst case, all words are unique anagrams

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        anagram = collections.defaultdict(list)
        for word in strs:
            # length of 26, assuming the characters
            # are lowercase English letters
            count = [0] * 26
            for char in word:
                count[ord(char) - ord("a")] += 1
            anagram[tuple(count)].append(word)
        return anagram.values()
```

## Two pointers

### 125. Valid palindrome

#### The problem

A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string `s`, return `true` if it is a palindrome, or `false` otherwise.

```
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
```

#### Brute force

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        # Create a cleaned string with only alphanumeric characters in lowercase
        cleaned_s = ''.join(c.lower() for c in s if c.isalnum())
        # Check if the cleaned string is equal to its reverse
        return cleaned_s == cleaned_s[::-1]
```

Possible solution using regular expressions:

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        cleaned_s = re.sub(r'[^a-zA-Z0-9]', '', s).lower()
        return True if cleaned_s == cleaned_s[::-1] else False
```

- time complexity: `O(n)` 
    - constructing the cleaned string takes `O(n)` time
    - comparing the string with its reverse takes `O(n)` time
- space complexity: `O(n)` - due to the size of the cleaned string

#### Two-pointer approach

- the cleaned string is constructed similarly to the first solution
- two pointers (left and right) are used to compare characters from the beginning and end of the cleaned string
- time complexity: `O(n)`
    - constructing the cleaned string takes `O(n)` time.
    - comparing characters using two pointers takes `O(n/2)` time.
- space complexity: `O(n)` - due to the size of the cleaned string

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        # Create a cleaned string with only alphanumeric characters in lowercase
        cleaned_s = ''.join(c.lower() for c in s if c.isalnum())

        # Use two pointers to compare characters from the beginning and end
        left, right = 0, len(cleaned_s) - 1
        while left < right:
            if cleaned_s[left] != cleaned_s[right]:
                return False
            left += 1
            right -= 1
        return True
```

#### Optimized two-pointer approach

- two pointers (left and right) are used to compare characters directly in the original string, skipping non-alphanumeric characters
- time complexity: `O(n)`
    - moving the pointers and comparing characters takes `O(n)` time
    - skipping non-alphanumeric characters without constructing a cleaned string
- space complexity: `O(1)` - constant space, as no additional space is used proportional to the input size

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        # Use two pointers to compare characters, skipping non-alphanumeric characters
        left, right = 0, len(s) - 1
        while left < right:
            while left < right and not s[left].isalnum():
                left += 1
            while left < right and not s[right].isalnum():
                right -= 1
            if s[left].lower() != s[right].lower():
                return False
            left += 1
            right -= 1
        return True
```

### 167. Two sum II - input array is sorted

#### Problem

Given a 1-indexed array of integers `numbers` that is already sorted in non-decreasing order, find two numbers such that they add up to a specific `target` number. Let these two numbers be `numbers[index1]` and `numbers[index2]` where 1 <= `index1` < `index2` <= `numbers.length`.

Return the indices of the two numbers, `index1` and `index2`, added by one as an integer array `[index1, index2]` of length 2.

The tests are generated such that there is exactly one solution. You may not use the same element twice.

Your solution must use only constant extra space.

```
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2. We return [1, 2].
```

#### Brute force

Similarly, as in [1. Two sum](#1-two-sum):
- time complexity: `O(n^2)` - nested loop through the array
- space complexity: `O(1)` - no additional space is used

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(0, len(nums) - 1):
            for j in range(1, len(nums)):
                if target == nums[i] + nums[j]:
                    return [i+1, j+1]
```

#### Binary search

- one-pointer loop to iterate through the array
- within the loop do a binary search to find a pair of numbers
- if the sum of the current number and the middle one is greater than the `target`, decrement `mid` index
- if the sum is less than the `target`, increment `mid` index.
- if the sum is equal to the `target`, return the indices `[curr_num_index + 1, mid + 1]`, as the indices are 1-based
- time complexity: `O(n*logn)` - we iterate through the array once and we perform a binary search
- space complexity: `O(1)` - no additional space is used

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        for curr_num_index, num in enumerate(numbers):
            left, right = curr_num_index + 1, len(numbers) - 1
            while left <= right:
                mid = (left + right) // 2
                if (numbers[mid] + num) == target: return curr_num_index + 1, mid + 1
                if (numbers[mid] + num) > target: right = mid - 1
                else: left = mid + 1
```

#### Two-pointer approach

- initialize two pointers, `left` and `right`, pointing to the start and end of the array, respectively
- use a while loop to iterate until `left` is less than `right`
- calculate the sum of the numbers at their positions
- if the sum is greater than the `target`, decrement `right`
- if the sum is less than the `target`, increment `left`
- if the sum is equal to the `target`, return the indices `[left+1, right+1]`, as the indices are 1-based
- time complexity: `O(n)` - we iterate through the array once
- space complexity: `O(1)` - no additional space is used

```python
class Solution:
    def twoSum(self, nums, target):
        left, right = 0, len(nums) - 1
        while left < right:
            if nums[left] + nums[right] == target: return (left + 1,  right + 1)
            if nums[left] + nums[right] > target: right -= 1
            else: left += 1
```

