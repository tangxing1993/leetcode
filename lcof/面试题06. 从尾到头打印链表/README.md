# [面试题 06. 从尾到头打印链表](https://leetcode.cn/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

## 题目描述

<p>输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>head = [1,3,2]
<strong>输出：</strong>[2,3,1]</pre>

<p>&nbsp;</p>

<p><strong>限制：</strong></p>

<p><code>0 &lt;= 链表长度 &lt;= 10000</code></p>

## 解法

该题需要将链表转换为数组，且需要反向。由于目标是链表，无法第一时间得知长度，声明等长数组。

解题方案：

-   遍历
    -   从头到尾遍链表，获取链表长度，声明等长数组；
    -   再次遍历并放入数组当中，在数组中的放置顺序是从尾到头。
-   递归
    -   记录深度，递归到链表尾部；
    -   将深度化为数组长度，将回溯结果正序放入数组当中。
-   动态数组
    -   遍历链表，将元素放入数组当中；
    -   遍历结束，将数组倒置后返回（`reverse()`）。

<!-- tabs:start -->

### **Python3**

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None


class Solution:
    def reversePrint(self, head: ListNode) -> List[int]:
        ans = []
        while head:
            ans.append(head.val)
            head = head.next
        return ans[::-1]
```

### **Java**

栈实现：

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public int[] reversePrint(ListNode head) {
        Deque<Integer> stk = new ArrayDeque<>();
        for (; head != null; head = head.next) {
            stk.push(head.val);
        }
        int[] ans = new int[stk.size()];
        int i = 0;
        while (!stk.isEmpty()) {
            ans[i++] = stk.pop();
        }
        return ans;
    }
}
```

先计算链表长度 n，然后创建一个长度为 n 的结果数组。最后遍历链表，依次将节点值存放在数组上（从后往前）：

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public int[] reversePrint(ListNode head) {
        if (head == null) {
            return new int[] {};
        }
        int n = 0;
        for (ListNode cur = head; cur != null; cur = cur.next, ++n)
            ;
        int[] ans = new int[n];
        for (ListNode cur = head; cur != null; cur = cur.next) {
            ans[--n] = cur.val;
        }
        return ans;
    }
}
```

### **JavaScript**

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} head
 * @return {number[]}
 */
var reversePrint = function (head) {
    let ans = [];
    for (; !!head; head = head.next) {
        ans.unshift(head.val);
    }
    return ans;
};
```

### **Go**

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func reversePrint(head *ListNode) []int {
	ans := []int{}
	for head != nil {
		ans = append([]int{head.Val}, ans...)
		head = head.Next
	}
	return ans
}
```

### **C++**

递归实现：

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {
        if (!head) return {};
        vector<int> ans = reversePrint(head->next);
        ans.push_back(head->val);
        return ans;
    }
};
```

栈实现：

```cpp
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {
        stack<int> stk;
        vector<int> ans;
        ListNode *p = head;
        while (p) {
            stk.push(p->val);
            p = p->next;
        }
        while (!stk.empty()) {
            ans.push_back(stk.top());
            stk.pop();
        }
        return ans;
    }
};
```

### **TypeScript**

```ts
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function reversePrint(head: ListNode | null): number[] {
    let ans: number[] = [];
    for (; !!head; head = head.next) {
        ans.unshift(head.val);
    }
    return ans;
}
```

### **Rust**

动态数组：

```rust
// Definition for singly-linked list.
// #[derive(PartialEq, Eq, Clone, Debug)]
// pub struct ListNode {
//   pub val: i32,
//   pub next: Option<Box<ListNode>>
// }
//
// impl ListNode {
//   #[inline]
//   fn new(val: i32) -> Self {
//     ListNode {
//       next: None,
//       val
//     }
//   }
// }
impl Solution {
    pub fn reverse_print(head: Option<Box<ListNode>>) -> Vec<i32> {
        let mut arr: Vec<i32> = vec![];
        let mut cur = head;
        while let Some(node) = cur {
            arr.push(node.val);
            cur = node.next;
        }
        arr.reverse();
        arr
    }
}
```

遍历：

```rust
// Definition for singly-linked list.
// #[derive(PartialEq, Eq, Clone, Debug)]
// pub struct ListNode {
//   pub val: i32,
//   pub next: Option<Box<ListNode>>
// }
//
// impl ListNode {
//   #[inline]
//   fn new(val: i32) -> Self {
//     ListNode {
//       next: None,
//       val
//     }
//   }
// }
impl Solution {
    pub fn reverse_print(head: Option<Box<ListNode>>) -> Vec<i32> {
        let mut cur = &head;
        let mut n = 0;
        while let Some(node) = cur {
            cur = &node.next;
            n += 1;
        }

        let mut arr = vec![0; n];
        let mut cur = head;
        while let Some(node) = cur {
            n -= 1;
            arr[n] = node.val;
            cur = node.next;
        }
        arr
    }
}
```

### **C#**

```cs
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int x) { val = x; }
 * }
 */
 public class Solution {
     public int[] ReversePrint(ListNode head) {
         List<int> ans = new List<int>();
         while (head != null) {
             ans.Add(head.val);
             head = head.next;
         }
         ans.Reverse();
         return ans.ToArray();
     }
 }
```

### **...**

```

```

<!-- tabs:end -->
