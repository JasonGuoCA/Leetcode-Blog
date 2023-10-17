# [203. Remove Linked List Elements(easy)](https://leetcode.com/problems/remove-linked-list-elements/)

 **代码随想录(programmercarl.com)explanation:**
#### [Video explanation](https://www.bilibili.com/video/BV18B4y1s7R9/?vd_source=892b6c3c3853e62a1c440b3a6c6946c2)

#### [Article explanation](https://programmercarl.com/0203.%E7%A7%BB%E9%99%A4%E9%93%BE%E8%A1%A8%E5%85%83%E7%B4%A0.html#%E6%80%9D%E8%B7%AF)

**Solution**:
This question involves the following two ways of Linked list operation:

**1. Use the original Linked list directly to perform the delete operation.**
```JAVA
class Solution {
    public ListNode removeElements(ListNode head, int val) {

        while(head != null && head.val == val){
            head = head.next;
        }
        if(head == null){
            return head;
        }
        
        ListNode pre = head;
        ListNode cur = head.next;
        while(cur!=null){
            if(cur.val == val){
                pre.next = cur.next;
            }else {
                pre = cur;
            }
            cur = cur.next;
        }
        return head;    
    }
}
```
**If you define only a present node and do not use a past node, the code will be more compact.**
```JAVA
        ListNode cur = head;
        while(cur.next != null){
            if(cur.next.val == val){
                cur.next = cur.next.next;
            } else {
                cur = cur.next;
            }
        }
        return head;
```
**2. Set a virtual head node in the delete operation.**
```JAVA
class Solution {
    public ListNode removeElements(ListNode head, int val) {

        if(head == null){
            return head;
        }

        ListNode dummy = new ListNode(-1,head);
        ListNode pre = dummy;
        ListNode cur = head;

        while(cur != null) {

            if(cur.val == val){
                pre.next = cur.next;
            } else {
                pre = cur;
            }
            cur = cur.next;
        }
        return dummy.next;        
    }
}
```

# [707. Design Linked List(Medium)](https://leetcode.com/problems/design-linked-list/)

 **代码随想录(programmercarl.com)explanation:**
#### [Video explanation](https://www.bilibili.com/video/BV1FU4y1X7WD/)

#### [Article explanation](https://programmercarl.com/0707.%E8%AE%BE%E8%AE%A1%E9%93%BE%E8%A1%A8.html)

**Solution**:
This problem can be solved in two ways: single Linked list and double Linked list. Also set up a virtual head node in the operation

**1. single Linked list**
```JAVA
class ListNode{
    int val;
    ListNode next;
    ListNode(){}
    ListNode(int val){
        this.val = val;
    }
}
class MyLinkedList {

    int size;

    ListNode head;

    public MyLinkedList() {
        
        size = 0;
        head = new ListNode(0);       
    }
    
    public int get(int index) {

        if(index < 0 || index >= size){
            return -1;
        }

        // dummyNode
        ListNode currentNode = head;

        for(int i = 0; i <= index; i++){
            currentNode = currentNode.next;
        }
        return currentNode.val;
    }
    
    public void addAtHead(int val) {
        addAtIndex(0,val);
        
    }
    
    public void addAtTail(int val) {
        addAtIndex(size,val);
        
    }
    
    public void addAtIndex(int index, int val) {

        if(index > size){
            return ;
        }

        if(index < 0){
            index = 0;
        }

        // because add one node, siza + 1
        size ++;

        ListNode pre = head;

        for(int i = 0; i < index; i ++){
            pre = pre.next;
        } 

        // add node
        ListNode toAdd = new ListNode(val);

        toAdd.next = pre.next;
        pre.next = toAdd;    
    }
    
    public void deleteAtIndex(int index) {

        if(index < 0 || index >= size){
            return ;
        }
        
        // because delete one node, size - 1
        size --;

        ListNode pre = head;

        for(int i = 0; i < index; i ++){
            pre = pre.next;
        }

        pre.next = pre.next.next;     
    }
}
```

**2. double Linked list**
```JAVA
class ListNode{
    int val;
    ListNode next, prev;
    ListNode(){}
    ListNode(int val){
        this.val = val;
    }
}
class MyLinkedList {

    int size;
    ListNode head,tail;

    public MyLinkedList() {
        
        size = 0;
        head = new ListNode(0);
        tail = new ListNode(0);
        head.next = tail;
        tail.prev = head;
        
    }
    
    public int get(int index) {

        if(index < 0 || index >= size){
            return -1;
        }

        // dummyNode
        ListNode currentNode = head;
        
        if(index >= size / 2){
            currentNode = tail;
            for(int i = 0 ; i < size - index; i ++){
                
                currentNode = currentNode.prev;
            }
        } else {
            for(int i = 0; i <= size; i ++){

                currentNode = currentNode.next;
            }
        }

        return currentNode.val;

    }
    
    public void addAtHead(int val) {
        addAtIndex(0,val);
        
    }
    
    public void addAtTail(int val) {
        addAtIndex(size,val);
        
    }
    
    public void addAtIndex(int index, int val) {

        if(index > size){
            return ;
        }

        if(index < 0){
            index = 0;
        }

        // because add one node, siza + 1
        size ++;

        ListNode pre = head;

        for(int i = 0; i < index; i ++){
            pre = pre.next;
        } 

        // add node
        ListNode toAdd = new ListNode(val);

        toAdd.next = pre.next;
        pre.next.prev = toAdd;
        toAdd.prev = pre;
        pre.next = toAdd;
        
    }
    
    public void deleteAtIndex(int index) {

        if(index < 0 || index >= size){
            return ;
        }
        size --;

        ListNode pre = head;

        for(int i = 0; i < index; i ++){
            pre = pre.next;
        }
   
        pre.next.next.prev = pre;
        pre.next = pre.next.next;    
    }
}
```
# [206. Reverse Linked List(easy)](https://leetcode.com/problems/reverse-linked-list/)

 **代码随想录(programmercarl.com)explanation:**
#### [Video explanation](https://www.bilibili.com/video/BV1nB4y1i7eL/)

#### [Article explanation](https://programmercarl.com/0206.%E7%BF%BB%E8%BD%AC%E9%93%BE%E8%A1%A8.html)

**Solution**:
Changing the next pointer of a Linked List directly inverts the Linked List without having to redefine a new Linked List.
**The two-pointer method**

First define a cur pointer, pointing to the head node, and a pre pointer, initialized to null.Then it's time to start the inversion process. 
After that, **we need to save the cur->next node with the tmp pointer**, that is, we need to save this node.
Why save this node, because the next change cur->next pointing to cur->next pointing to pre, at this time has reversed the first node.
The next step is to loop through the logic of the code as follows, continuing to move the pre and cur pointers.
Finally, the cur pointer has pointed to null, the cycle is over, Linked List has been reversed. At this point, we return the pre pointer, which points to the new head node.

```JAVA
class Solution {
    public ListNode reverseList(ListNode head) {

        ListNode cur = head;
        ListNode pre = null;
        ListNode temp = null;
        while(cur != null){
            temp = cur.next;
            cur.next = pre;
            pre = cur;
            cur = temp;
        }
        return pre;
    }
  }
```
**Recursion**

Recursive method is relatively abstract, but in fact and the double pointer method is the same logic, the same is when cur is empty when the loop ends, constantly pointing cur to the process of pre.
The key is the initialization of the place, you can see the double pointer method of initialization cur = head, pre = NULL, in the recursive method can be seen from the following code to initialize the logic is the same, only that the writing method has changed.
```JAVA
class Solution {
    public ListNode reverseList(ListNode head) {
        return reverse(head,null);
    }

    private ListNode reverse(ListNode cur, ListNode pre){

        if(cur == null){
            return pre;
        }
        ListNode temp = cur.next;
        cur.next = pre;
        return reverse(temp,cur);
    }
}
```
