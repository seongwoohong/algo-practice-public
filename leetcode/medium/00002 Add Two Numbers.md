# 2. Add Two Numbers

| Categories  | Runtime     | Memory      |
| :-----------: | :-----------: | :-----------: |
| Linked List, Math         | 12ms         | 4.7MB       |

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example**
```
**Input**: (2 -> 4 -> 3) + (5 -> 6 -> 4)
**Output**: 7 -> 0 -> 8
**Explanation**: 342 + 465 = 807.
```

**My Answer**
```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func addTwoNumbers(l1 *ListNode, l2 *ListNode) *ListNode {
    carry, result := 0, l1

    for {
        l1.Val += l2.Val + carry
        carry = int(l1.Val / 10)
        l1.Val = l1.Val % 10 
        
        if l2.Next == nil {
            break
        } else if l1.Next == nil {
            l1.Next = l2.Next
            break
        }  

        l1 = l1.Next
        l2 = l2.Next
    }
    
    for carry > 0 {
        if l1.Next == nil {
	    l1.Next = &ListNode{0,nil}
	}
        
        l1.Next.Val += carry
        carry = l1.Next.Val / 10
        l1.Next.Val = l1.Next.Val % 10

        l1 = l1.Next
    }

    return result
}
```

**Test Cases**
```go
func TestAddTwoNumbers(t *testing.T) { //Q2
	f := []*ListNode{
		&ListNode{2, &ListNode{4, &ListNode{3, nil}}},
		&ListNode{7, &ListNode{2, &ListNode{5, nil}}},
	}
	g := []*ListNode{
		&ListNode{5, &ListNode{6, &ListNode{4, nil}}},
		&ListNode{5, &ListNode{7, &ListNode{8, nil}}},
	}
	r := []*ListNode{
		&ListNode{7, &ListNode{0, &ListNode{8, nil}}},
		&ListNode{2, &ListNode{0, &ListNode{4, &ListNode{1, nil}}}},
	}

	for i := 0; i < len(f); i++ {
		assert.DeepEqual(t, addTwoNumbers(f[i], g[i]), r[i])
	}
}
```