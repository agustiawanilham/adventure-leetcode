# Questions

Source : (Two sum)[https://leetcode.com/problems/two-sum]

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

Example 1:

Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
Example 2:

Input: nums = [3,2,4], target = 6
Output: [1,2]
Example 3:

Input: nums = [3,3], target = 6
Output: [0,1]

Follow-up: Can you come up with an algorithm that is less than O(n2) time complexity?

# My Answer

## Solutions

1. Naive solutions

```go
func twoSum(nums []int, target int) []int {
    target1 := 0
    target2 := 1
    for i := 0; i < len(nums); i++ {
        for j := i + 1; j < len(nums); j++ {
            if nums[i] + nums[j] == target {
                target1 = i
                target2 = j
                break
            }
        }
    }

    return []int{target1, target2}
}
```

2. Better solutions

```go
func twoSum(nums []int, target int) []int {
    var hash = make(map[int]int)
    for i, num := range nums {
        if index, ok := hash[target-num]; ok {
            return []int{i, index}
        }

        hash[nums[i]] = i
    }

    return nil
}
```

hash = value, index

- check di hash
- jika target minus current value sudah ada di hash, return current loop index dan index target - value
- set hash dengan key=current value dan value = current index

Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
Example 2:

The second function is more efficient than the first one due to its time complexity.

The first function uses a nested loop to find the two numbers that add up to the target.
This results in a time complexity of O(n^2), where n is the length of the input array. This is because for each element in the array, the function checks all other elements to see if they add up to the target.

The second function, on the other hand, uses a hash map to store the numbers it has seen so far and their indices. It then checks for each number if the difference between the target and the current number is in the hash map. If it is, it means that the two numbers that add up to the target have been found. This results in a time complexity of O(n), which is more efficient than O(n^2), especially for large input arrays.

In terms of space complexity, the first function has a space complexity of O(1) as it does not use any additional data structures, while the second function has a space complexity of O(n) due to the hash map. However, the improved time efficiency of the second function often outweighs the increased space usage, especially for large inputs.
