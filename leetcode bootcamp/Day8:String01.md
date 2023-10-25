# [344. Reverse String](https://leetcode.com/problems/reverse-string/)
# [541. Reverse String II](https://leetcode.com/problems/reverse-string-ii/)
# [151. Reverse Words in a String（Medium）](https://leetcode.com/problems/reverse-words-in-a-string/)

**解题想法：**

这三道题的难度是逐渐上升，第一道题就是简单使用了双指针对字符串做了反转，第二题在双指针基础上，for循环累加方式变成了i += 2 * k

第三题比较难一点，用到了两次双指针，第一次是去除多余空格的时候，快指针循环，慢指针记录不带多余空格的，然后返回新的数组。第二次使用是用右指针处理，取出 每一个单词，然后进行反装。

**Solution Ideas:**

The difficulty of these three problems gradually increases. The first problem is simply using a two-pointer approach to reverse a string. In the second problem, on top of the two-pointer approach, the for loop cumulative method changes to i += 2 * k.

The third problem is a bit more challenging. It involves using two sets of two pointers. The first set is used to remove excess spaces, with the fast pointer looping and the slow pointer recording the string without the extra spaces, then returning the new array. The second set is used with the right pointer to extract each word and then reverse them.

# [ 剑指Offer 05.替换空格 ](https://leetcode.cn/problems/ti-huan-kong-ge-lcof/)
# [  剑指Offer58-II.左旋转字符](https://leetcode.cn/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

**解题想法：**

第一题对字符串循环，把“.”替换成空格，保存在新的数组里面。
第二题最字符串两次循环，第一次是target到字符串末尾，然后保存在新的字符数组，第二次是0到target，最后保存在上一步新的字符数组

**Solution Ideas:**

In the first question, loop through the string, replace "." with a space, and save it in a new array.

In the second question, there are two loops through the string. The first loop goes from "target" to the end of the string, and the result is saved in a new character array. The second loop goes from 0 to "target," and the result is saved in the character array created in the previous step.
