# 3. Longest Substring Without Repeating Characters

| Categories  | Runtime     | Memory      |
| :-----------: | :-----------: | :-----------: |
| Hash Table, Two Pointers, String, Sliding Window        | 4ms         | 2.5MB       |

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Given a string, find the length of the **longest substring** without repeating characters.


**Example**

| Input  | Output     | Explanation      |
| :-----------: | :-----------: | :----------- |
| "abcabcbb" | 3 | The answer is "abc", with the length of 3. |
| "bbbbb" | 1 | The answer is "b", with the length of 1. |
| "pwwkew" | 3 | The answer is "wke", with the length of 3.  Note that the answer must be a **substring**, "pwke" is a subsequence and not a substring. |
 

**Efficient Solution**
```go
func lengthOfLongestSubstring(s string) int {
    var start, ans int

    m := [256]int{}

    for i := range m {
        m[i] = -1
    }

    for i:=0; i<len(s); i++ {
        if m[s[i]] < start {
            if i-start+1 > ans {
                ans = i-start+1
            }
        } else {
            start = m[s[i]] + 1
        }
        m[s[i]] = i
    }

    return ans
}
```

**Test Cases**
```go
func TestLengthOfLongestSubstring(t *testing.T) {
    f := []string{"abcabcbb", "bbbbb", "pwwkew"}
    r := []int{3, 1, 3}

    for i := 0; i < len(f); i++ {
        assert.DeepEqual(t, lengthOfLongestSubstring(f[i]), r[i])
    }
}
```