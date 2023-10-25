# [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)
# [1047. Remove All Adjacent Duplicates In String](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/)
# [150. Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)

**解题想法：**

**第一题**用栈来实现，对输入的字符串进行循环，然后要注意三种错误的情况

 1.在循环中，栈已经空了
 
 2.在循环到左符号时，会在栈里面push入对应的右符号，如果循环的右符号和栈的进行比较，出现了不一致
 
3.循环结束后发现栈不为空

**第二题**是删除字符串相邻重复字符，用栈来实现，准确的说是用Deque来实现。
出现第一个字符时，该字符入栈，然后后面进行比较，相同时让这个字符出栈，
循环结束后，下面这段代码要注意，基于栈的LIFO规则，出栈处理要在加号前面
```JAVA
while(!deq.isEmpty())
    st = deq.pop() + st;
```

**第三题**，对输入字符串数组进行循环，然后判断“+” ，“-”，“*”，“/”进行判断，把计算的结果

入栈，需要注意的是基于栈的LIFO特性，要注意减法和除法，
减法的时候参考下面代码
```java
 else if("-".equals(tokens[i])) deq.push(-deq.pop() + deq.pop());
```
在除法的时候，要用变量先记录再相除
```java
else if("/".equals(tokens[i])) {
   int temp1 = deq.pop();
   int temp2 = deq.pop();
   deq.push(temp2 / temp1); 
```
除此以外就是把相应的数字入栈,

**Solution Ideas:**

**For the first question**, a stack is used for implementation. The input string is looped through, and three error cases need to be considered:

1.Within the loop, if the stack is already empty.

2.When looping through left symbols, the corresponding right symbol is pushed onto the stack. If the right symbol encountered in the loop does not match the one in the stack, it's an inconsistency.

3.After the loop, if it's found that the stack is not empty.

**For the second question**, it involves removing adjacent duplicate characters in a string, and a stack, specifically a Deque, is used for implementation. Here's a breakdown:

When the first character is encountered, it's pushed onto the stack.
Subsequent characters are compared, and if they match the one on top of the stack, that character is popped.
After the loop, there's a piece of code to be aware of, which follows the Last-In-First-Out (LIFO) rule:
```JAVA

while(!deq.isEmpty())
    st = deq.pop() + st;
```
**For the third question**, a loop goes through an input string array, and operations "+," "-," "*," and "/" are evaluated, and the results are pushed onto the stack. Pay attention to subtraction and division. For subtraction, refer to the following code:

```java

else if("-".equals(tokens[i])) deq.push(-deq.pop() + deq.pop());
```
For division, a variable is used to first store values and then perform the division:

```java

else if("/".equals(tokens[i])) {
    int temp1 = deq.pop();
    int temp2 = deq.pop();
    deq.push(temp2 / temp1);
```
Besides these operations, other numbers are simply pushed onto the stack.
