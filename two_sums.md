# two sums

## 思路1：可以使用O(n^2)时间复杂度，空间复杂度O(1)的loop,但是这样时间复杂度太高
```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i, v in enumerate(nums[:-1]):
            for j, v1 in enumerate(nums[i+1:]):
                if v+v1 == target:
                    return [i,j]
```

## 思路2： 利用空间换时间，O(n)时间复杂度，O(n)空间复杂度 

```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hash_map = {}
        # using hash map record the value of nums
        for i, v in enumerate(nums):
            if v in hash_map:
                return [hash_map[v], i]
            else:
                hash_map[target-v] = i
```