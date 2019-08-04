### 题目描述

输入一个链表，输出该链表中倒数第k个结点。

### 解析

先找到链表中顺数第k个节点,然后两个指针,第一个指针指向链表头,第二个指针指向顺数第k个节点,遍历链表,两个指针一起动,直到第二个指针指向链表尾,此时第一个指针指向的节点就是答案

### 代码示例

```java
/*
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}*/
public class Solution {
    public ListNode FindKthToTail(ListNode head,int k) {
        if (head == null || k == 0) return null;
        ListNode temp = head;
        ListNode pHead = head;
        for (int i = 1; i < k; i++) {
            if (temp.next != null) temp = temp.next;
            else return null;
        }
        while (temp.next != null) {
            temp = temp.next;
            pHead = pHead.next;
        }
        return pHead;
    }
}
```