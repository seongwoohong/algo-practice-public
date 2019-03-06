# 1. Two Sum

| Categories  | Runtime     | Memory      |
| ----------- | ----------- | ----------- |
| Array, HashTable         | 4ms         | 3.4MB       |

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.
You may assume that each input would have **exactly** one solution, and you may not use the same element twice.

**Example**
```
Given nums = [2, 7, 11, 15], target = 9,
Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

**My Answer**
```go
func twoSum(nums []int, target int) []int {
	maps := make(map[int]int, len(nums))

	for i := 0 ; i < len(nums); i++ {
		complement := target - nums[i]
		if _, ck := maps[complement]; ck {
			return []int{ maps[complement], i }
		}
		maps[nums[i]] = i
	}

	return nil
}
```

**Test Cases**
```go
func TestTwoSum(t *testing.T) { // Q1
	nums := [][]int{
		{2, 7, 11, 15},
		{6, 9, 41, 21},
		{3, 7, 14, 52},
	}
	target := []int{
		9,
		50,
		45,
	}
	result := [][]int{
		{0, 1},
		{1, 2},
		nil,
	}
	for i := 0; i < len(nums); i++ {
		assert.DeepEqual(t, twoSum(nums[i], target[i]), result[i])
	}
}
```