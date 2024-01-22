# Leetcode solutions

I am following [neetcode](https://neetcode.io/practice).

- [Arrays and hashing](#arrays-and-hashing)
    - [217. Contains duplicate](#217-contains-duplicate) - easy

## Arrays and hashing

### 217. Contains duplicate

#### The problem

Given an integer aray nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

#### Brute force

- time complexity: `O(n**2)`

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
- time complexity for sorting: `O(n*logn)`
- time complexity for searching adjacent elements:`O(n)`
- overall time complexity: `O(n*logn)`

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
- time complexity: `O(n)`

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
- time complexity: `O(n)`

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

