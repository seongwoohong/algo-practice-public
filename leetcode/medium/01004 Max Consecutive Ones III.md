# 1004. Max Consecutive Ones III

| Categories  | Runtime     | Memory      |
| :-----------: | :-----------: | :-----------: |
| Two Pointers, Sliding Window         | 60ms         | 7.4MB       |

Given an array **A** of 0s and 1s, we may change up to **K** values from 0 to 1.

Return the length of the longest (contiguous) subarray that contains only 1s. 

**Example**

| Input  | Output     | Explanation      |
| :-----------: | :-----------: | :----------- |
| A = [1,1,1,0,0,0,1,1,1,1,0]<br>K = 2  | 6 | [1,1,1,0,0,<u>**1**</u>,<u>1</u>,<u>1</u>,<u>1</u>,<u>1</u>,<u>**1**</u>]<br>Bolded numbers were flipped from 0 to 1.  The longest subarray is underlined. |
| A = [0,0,1,1,0,0,1,1,1,0,1,1,0,0,0,1,1,1,1]<br>K = 3 | 10 | [0,0,<u>1</u>,<u>1</u>,<u>**1**</u>,<u>**1**</u>,<u>1</u>,<u>1</u>,<u>1</u>,<u>**1**</u>,<u>1</u>,<u>1</u>,0,0,0,1,1,1,1]<br>Bolded numbers were flipped from 0 to 1. The longest subarray is underlined. |

**Note:**
1. 1 <= A.length <= 20000
2. 0 <= K <= A.length
3. A[i] is 0 or 1 

**My Subsmission**
```go
func longestOnes(A []int, K int) int {
    i, j := 0, 0
    for j = 0; j < len(A); j++ {
        if A[j] == 0 {
            K--
        }
        if K < 0 {
            if A[i] == 0 {
                K++
            }
            i++
        }
    }
    return j-i
}
```

**Test Cases**
```go
func TestLongestOnes(t *testing.T) {
    f := [][]int{
        {1,1,1,0,0,0,1,1,1,1,0},
        {0,0,1,1,0,0,1,1,1,0,1,1,0,0,0,1,1,1,1},
    }
    g := []int{2,3}
    r := []int{6,10}

    for i := 0; i < len(f); i++ {
        assert.DeepEqual(t, longestOnes(f[i], g[i]), r[i])
    }
}
```