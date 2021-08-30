### LeetCode题目2-add-two-number

---
### 来源
https://leetcode-cn.com/problems/add-two-numbers/

---
### 题目：
给你两个 非空 的链表，表示两个非负的整数。它们每位数字都是按照 逆序 的方式存储的，并且每个节点只能存储 一位 数字。
请你将两个数相加，并以相同形式返回一个表示和的链表。
你可以假设除了数字 0 之外，这两个数都不会以 0 开头。
示例 1：
![twonumber](../pic/2/addtwonumber1.jpg)

输入：l1 = [2,4,3], l2 = [5,6,4]
输出：[7,0,8]
解释：342 + 465 = 807.
示例 2：

输入：l1 = [0], l2 = [0]
输出：[0]
示例 3：

输入：l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
输出：[8,9,9,9,0,0,0,1]
 

提示：

每个链表中的节点数在范围 [1, 100] 内
0 <= Node.val <= 9
题目数据保证列表表示的数字不含前导零

---
#### 分析
基本上是遍历链表的过程, 实现过程如下
1. 同时遍历两个链表，直到达到一个链表结束。把每个节点的值相加，判断是否大于10，设置标志，如果对于10，下个节点计算加1。值取个位数。
1. 遍历没有遍历完的链表。为了方便和优雅，两个表统一处理。
1. 判断大于10的标志位，如果已经设置，增加节点，值为1。

---
代码实现：
c++
```
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
		bool gt10 = false;
		ListNode* head = nullptr;
		ListNode* tmp = nullptr;
		while (!(l1 == nullptr && l2 == nullptr)) {
			int v;
			if (l1 != nullptr && l2 != nullptr) {
				v = l1->val + l2->val;
				l1 = l1->next;
				l2 = l2->next;
			}
			else if (l1 == nullptr && l2 != nullptr){
				v = l2->val;
				l2 = l2->next;
			}
			else {
				v = l1->val;
				l1 = l1->next;
			}
			if (gt10) {
				++v;
			}

			ListNode* n;
			if (v >= 10) {
				gt10 = true;
				n = new ListNode(v - 10);
			}
			else {
				gt10 = false;
				n = new ListNode(v);
			}
			if (head == nullptr) {
				head = n;
			}
			else {
				tmp->next = n;
			}
			tmp = n;
		}
		if (gt10) {
			tmp->next = new ListNode(1);
		}
		return head;
    }
};
```

---
Go代码
```
func addTwoNumbers(l1 *ListNode, l2 *ListNode) *ListNode {
	var h *ListNode
	var p *ListNode
	var g10 bool

	// 两个点相加, 并生成链表
	for l1 != nil && l2 != nil {
		v := l1.Val + l2.Val
		if g10 {
			v += 1
		}
		var tp *ListNode
		if v >= 10 {
			g10 = true
			tp = &ListNode{v % 10, nil}
		} else {
			tp = &ListNode{v, nil}
			g10 = false
		}
		if h == nil {
			h = tp
		} else {
			p.Next = tp
		}
		p = tp

		l1 = l1.Next
		l2 = l2.Next
	}

	// 遍历没有遍历好的链表
	lf := func(l *ListNode) {
		for ; l != nil; l = l.Next {
			v := l.Val
			if g10 {
				v += 1
			}
			var tp *ListNode
			if v >= 10 {
				g10 = true
				tp = &ListNode{v % 10, nil}
			} else {
				tp = &ListNode{v, nil}
				g10 = false
			}
			if h == nil {
				h = tp
			} else {
				p.Next = tp
			}
			p = tp
		}
	}
	lf(l1)
	lf(l2)

	//处理最后一个点是有进位
	if g10 {
		p.Next = &ListNode{1, nil}
	}

	return h
}
```