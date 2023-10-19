# [24. Swap Nodes in Pairs(Medium)](https://leetcode.com/problems/swap-nodes-in-pairs/description/)

 **代码随想录(programmercarl.com)explanation:**
#### [Video explanation](https://www.bilibili.com/video/BV1YT411g7br/?spm_id_from=333.788&vd_source=892b6c3c3853e62a1c440b3a6c6946c2)

#### [Article explanation](https://programmercarl.com/0024.%E4%B8%A4%E4%B8%A4%E4%BA%A4%E6%8D%A2%E9%93%BE%E8%A1%A8%E4%B8%AD%E7%9A%84%E8%8A%82%E7%82%B9.html)

**Solution**:

The problem is solved by using **the dummy head node**.

Firstly, the dummy node points to the head node, and the current node is the dummy node.

Secondly, the current node **points to **the next of the head node****, then **points to the head node**, and then **points to the third node**, this can swap the first and second nodes,

Thirdly, the current node changes to **the head node(it points to the third node)**, repeating the second step.

At last, when the current node. next is null and the current node.next.next is null,  end of the process, return this swapped linked list.

```JAVA
class Solution {
    public ListNode swapPairs(ListNode head) {

        // Define the virtual head node
        ListNode dummyNode = new ListNode(-1);

        // The next of the virtual head nodes points to head
        dummyNode.next = head;

        // Define the current node, value is the virtual head node
        ListNode cur = dummyNode;

        // Define three temporary nodes
        ListNode firstNode;
        ListNode secondNode;
        ListNode temp;

        // While loop on linked list
        // The order of while conditons should not be reversed to prevent null pointer exceptions
        while(cur.next != null && cur.next.next != null){

            // Save old node positions with temporary nodes
            firstNode = cur.next;
            secondNode = cur.next.next;
            temp = cur.next.next.next;

            // Reverse the current nodes
            cur.next = secondNode;
            secondNode.next = firstNode;
            firstNode.next = temp;

            // Current Node moves in prepared for the next round of exchanges
            cur = firstNode;

        }
        return dummyNode.next;
    }
}
```

# [19. Remove Nth Node From End of List(Medium)](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/)

 **代码随想录(programmercarl.com)explanation:**
#### [Video explanation](https://www.bilibili.com/video/BV1vW4y1U7Gf/?spm_id_from=333.788&vd_source=892b6c3c3853e62a1c440b3a6c6946c2)

#### [Article explanation](https://programmercarl.com/0019.%E5%88%A0%E9%99%A4%E9%93%BE%E8%A1%A8%E7%9A%84%E5%80%92%E6%95%B0%E7%AC%ACN%E4%B8%AA%E8%8A%82%E7%82%B9.html#%E6%80%9D%E8%B7%AF)

**Solution**:

The problem is solved by using **two points and the dummy head node**.

Firstly, define a dummy head node, and point to the head node.

Secondly, define fast and slow nodes (two points), and their values are the dummy head node.

Thirdly, the fast node moves to **n + 1** times, ensuring that when fast and slow nodes move together and the fast node is null, the slow node is **the one before the deleted node**.

At last, the slow node points to **the next of the deleted node**.

```JAVA
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {

        // Define the dummy node, and it points to the head
        ListNode dummyNode = new ListNode(-1);
        dummyNode.next = head;

        // The problem was solved with double points,
        // so define the fast and slow node， and their values are dummy node
        ListNode fastNode = dummyNode;
        ListNode slowNode = dummyNode;

        // The fast node moves to n + 1 times,
        // ensuring that when the fast and slow move together,
        // the slow one can move to the one before the deleted node.
        for(int i = 0; i <= n; i ++){
            fastNode = fastNode.next;
        }

        // The fast and slow nodes move together,
        // when the fast node is null,
        // the slow node is the one before the deleted node
        while(fastNode != null){
            fastNode = fastNode.next;
            slowNode = slowNode.next;
        }

        // The slow node points to the next of the deleted node
        slowNode.next = slowNode.next.next;

        return dummyNode.next;
    }
}
```

# [面试题 02.07. 链表相交(easy)](https://leetcode.cn/problems/intersection-of-two-linked-lists-lcci/description/)

 **代码随想录(programmercarl.com)explanation:**

#### [Article explanation](https://programmercarl.com/%E9%9D%A2%E8%AF%95%E9%A2%9802.07.%E9%93%BE%E8%A1%A8%E7%9B%B8%E4%BA%A4.html#%E6%80%9D%E8%B7%AF/)

**Solution**:

Firstly, calculate **the length** of the linked list A and B, get **the gap** from the length of A and B.

Secondly, the **longer** linked list move to **gap times**(ensuring that A and B can move together to get the intersection node)

At last, when the nodes of A and B are **equal**, it can get the **intersection** node, return this one. 

```JAVA
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {

        // Define the current node A and B, and they are the respective head node
        ListNode curA = headA;
        ListNode curB = headB;

        // Define the length of the linked list A and B
        int lenA = 0, lenB = 0;

        // Calculate the length of the linked listA
        while(curA != null){
            lenA ++;
            curA = curA.next;
        }

        // Calculate the length of the linked listB
        while(curB != null){
            lenB ++;
            curB = curB.next;
        }

        // The current nodes A and B redirect to the individual head node
        curA = headA;
        curB = headB;

        // Ensure that the length of the linked list A is the longest
        if(lenA < lenB){

            // Exchange the length of linked list A and B
            int lenTemp = lenA;
            lenA = lenB;
            lenB = lenTemp;

            // Swap the linked list A and B
            ListNode tempNode = curA;
            curA = curB;
            curB = tempNode;
        }

        // Calculate the gap of the length of the linked list A and B
        int gap = lenA - lenB;

        // The current node A moves to the gap times, 
        // ensuring that when the current node A and B move together, they can point to the same node.
        while(gap-- > 0){
            curA = curA.next;
        }

        // The current node A and b move together,
        // when they point to the same node, return the current node A
        // when they point to null and they don't point to the same node, return null
        while(curA != null){

            if(curA == curB){
                return curA;
            }

            curA = curA.next;
            curB = curB.next;
        }
        
        return null;   
    }
}
```
# [142. Linked List Cycle II(Medium)](https://leetcode.com/problems/linked-list-cycle-ii/description/)

 **代码随想录(programmercarl.com)explanation:**
#### [Video explanation](https://www.bilibili.com/video/BV1if4y1d7ob/?spm_id_from=333.788&vd_source=892b6c3c3853e62a1c440b3a6c6946c2)

#### [Article explanation](https://programmercarl.com/0142.%E7%8E%AF%E5%BD%A2%E9%93%BE%E8%A1%A8II.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE/)

**Solution**:

The problem is solved by using **two points**.

Firstly, define the fast and slow nodes(two points), and their value are the head node

Secondly, each time, the fast node moves twice and the slow node moves once, when the fast and slow nodes are equal, it can proves there is a circle in the linked list.

Thirdly, the current node changes to the head node(it points to the third node), repeating the second step.

At last, when the current node. next is null and the current node.next.next is null,  end of the process, return this swapped linked list.

```JAVA
public class Solution {
    public ListNode detectCycle(ListNode head) {

        // The problem is solved with doubule points,
        // so it need to define fast and slow node, and the value are the head node.
        ListNode fastNode = head;
        ListNode slowNode = head;

        // Each time, the fast node moves twice, but the slow node move once,
        // when the fast and slow node point to the name node,
        // this can prove that there is a cycle in the linked list.
        // when not, there is no cycle.
        while(fastNode != null && fastNode.next != null){
            fastNode = fastNode.next.next;
            slowNode = slowNode.next;

            // When there is a cycle,
            // define two nodes, node1 points to the fast node, node2 point2 the head node.
            // Then they each move once per loop.
            // When they point to the same node, it is the entrance of the cycle
            if(fastNode == slowNode){

                ListNode node1 = fastNode;
                ListNode node2 = head;
                while (node1 != node2){
                    node1 = node1.next;
                    node2 = node2.next;
                }
                return node1;
            }

        }
        return null;
        
    }
}
```





