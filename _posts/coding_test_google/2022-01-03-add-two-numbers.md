---
title: "Add Two Numbers"
excerpt: "You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list. You may assume the two numbers do not contain any leading zero, except the number 0 itself."
categories: 
  - algorithm
tags: 
  - leetcode
  - google
  - java
  - linked-list
  - math
  - recursion
header:
    overlay_image: /assets/images/algo_int/3.jpg
toc: true
toc_sticky: true
---

## Problem Description
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list. You may assume the two numbers do not contain any leading zero, except the number 0 itself.

> What if the the digits in the linked list are stored in non-reversed order? 

## Examples
##### Example 1
```
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
```
##### Example 2
```
Input: l1 = [0], l2 = [0]
Output: [0]
```
##### Example 3
```
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
```

## Constraints
* The number of nodes in each linked list is in the range `[1, 100]`.
* $0 <= Node.val <= 9$
* It is guaranteed that the list represents a number that does not have leading zeros.

## Approaches
### Approach 1: Elementary Math
#### Intuition
Keep track of the carry using a variable and simulate digits-by-digits sum starting from the head of list, which contains the least-significant digit.

#### Implementation
```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    ListNode dummyHead = new ListNode(0);
    ListNode p = l1, q = l2, curr = dummyHead;
    int carry = 0;
    while (p != null || q != null) {
        int x = (p != null) ? p.val : 0;
        int y = (q != null) ? q.val : 0;
        int sum = carry + x + y;
        carry = sum / 10;
        curr.next = new ListNode(sum % 10);
        curr = curr.next;
        if (p != null) p = p.next;
        if (q != null) q = q.next;
    }
    if (carry > 0) {
        curr.next = new ListNode(carry);
    }
    return dummyHead.next;
}
```

#### Complexity Analysis
* Time complexity : $O(\max(m, n))$. Assume that $m$ and $n$ represents the length of $l1$ and $l2$ respectively, the algorithm above iterates at most $\max(m, n)$ times.

* Space complexity : $O(\max(m,n))$. The length of the new list is at most $\max(m,n) + 1$.