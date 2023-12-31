# [704.BinarySearch](https://leetcode.com/problems/binary-search/)

 **代码随想录(programmercarl.com)explanation:**

#### [Video explanation](https://www.bilibili.com/video/BV1fA4y1o715)

#### [Article explanation](https://programmercarl.com/0704.%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE.html)


**Solution**:

To solve the problem, you need to know how to use binary search.

**(1)left inclusion right inclusion**

```JAVA
class Solution {
    public int search(int[] nums, int target) {   
        int left = 0;
        int right = nums.length - 1;
        while(left <= right){
            int middle = left +((right - left)/2);
            
            if(nums[middle] > target){ // target is right of center
                right = middle - 1;
            } else if(nums[middle] < target){ // target is left of center
                left = middle + 1;
            } else {      // target is in the center
                return middle;
            }
        }
        return -1;
    }
}
```
Time complexity： O(logN)

Space complexity: O(1)

**(2)left inclusion right exclusion**
```JAVA
class Solution {
    public int search(int[] nums, int target) {   
        int left = 0;
        int right = nums.length;
        while(left < right){
            int middle = left +((right - left)/2);
            
            if(nums[middle] > target){ // target is right of center
                right = middle;
            } else if(nums[middle] < target){ // target is left of center
                left = middle + 1;
            } else {      // target is in the center
                return middle;
            }
        }
        return -1;
    }
}
```
Time complexity： O(logN)

Space complexity: O(1)

# [27. Remove Element](https://leetcode.com/problems/remove-element/description/)

 **代码随想录(programmercarl.com)explanation:**

#### [Video explanation](https://www.bilibili.com/video/BV12A4y1Z7LP )

#### [Article explanation](https://programmercarl.com/0027.%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0.html)

**Solution**:

Defined two points: fast point and slow point, fast point finds an element different from val,
slow point records the new array which is different from val.
```JAVA
class Solution {
    public int removeElement(int[] nums, int val) {
        int lowPoint = 0;
        for(int fastPoint = 0; fastPoint < nums.length; fastPoint++){
            if(nums[fastPoint] != val){
                nums[lowPoint ++] = nums[fastPoint];
            }
        }
        return lowPoint;
    }
}
```
Time complexity： O(N)

Space complexity: O(1)

