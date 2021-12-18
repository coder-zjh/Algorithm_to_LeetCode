# 链表

## Easy

#### [21. 合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)

设置一个存放结果的链表，链表头为dummy，还有一个为dummy赋值服务的指针p。

为两个有序链表设置指针p1、p2，用于遍历list1和list2。

当p1和p2指向的值都不为空时，进行大小比较，把小的放入dummy，

也就是p指针指向的位置，



```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        // 设置一个哑节点作为结果链表的起始->p。
        ListNode dummy = new ListNode(-1),p = dummy;
        // 为两条链表分别设置两个指针->p1/p2
        ListNode p1 = list1,p2 = list2;

        // 当两个指针指向的位置都有值时，比较两指针对应的值
        while(p1!=null&&p2!=null){
            // p1值大于p2值
            if(p1.val>p2.val){
                // 则p2要加入结果链表
                p.next = p2;
                // 然后p2的指针指向它所在链表的下一个位置
                p2 = p2.next;
            }else{
                //p1值小于p2值，则p1要加入结果链表
                p.next = p1;
                // 然后p1的指针指向它所在链表的下一个位置
                p1 = p1.next;
            }
            // 赋值后结果列表指针进1
            p = p.next;
        }

        // 当两条链表有一条为null时，跳出while循环，
        // 这时观察是哪一条链表不为null，则接上结果链表
        if(p1!=null){
            p.next = p1;
        }
        if(p2!=null){
            p.next = p2;
        }
    // 理解为什么这里是dummy.next，
    // dummy结果是[-1,1,1,2,3,4,4]
    // dummy.next结果是[1,1,2,3,4,4]
    // p结果是[4,4]
    return dummy.next;

    }
}
```

#### [83. 删除排序链表中的重复元素](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/)

```java
```

#### [141. 环形链表](https://leetcode-cn.com/problems/linked-list-cycle/)

```java
```

#### [160. 相交链表](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/)

```java
```

#### [203. 移除链表元素](https://leetcode-cn.com/problems/remove-linked-list-elements/)

```java

```

#### [206. 反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)

```java

```

#### [234. 回文链表](https://leetcode-cn.com/problems/palindrome-linked-list/)

```java
```

#### [237. 删除链表中的节点](https://leetcode-cn.com/problems/delete-node-in-a-linked-list/)

```java

```

#### [705. 设计哈希集合](https://leetcode-cn.com/problems/design-hashset/)

```java
```

#### [706. 设计哈希映射](https://leetcode-cn.com/problems/design-hashmap/)

```java

```

#### [716. 最大栈](https://leetcode-cn.com/problems/max-stack/)

```java

```

#### [876. 链表的中间结点](https://leetcode-cn.com/problems/middle-of-the-linked-list/)

```java

```

#### [1290. 二进制链表转整数](https://leetcode-cn.com/problems/convert-binary-number-in-a-linked-list-to-integer/)

```java
```

#### [1474. 删除链表 M 个节点之后的 N 个节点](https://leetcode-cn.com/problems/delete-n-nodes-after-m-nodes-of-a-linked-list/)

```java

```

## Medium

#### [2. 两数相加](https://leetcode-cn.com/problems/add-two-numbers/)

```java

```







## Hard

