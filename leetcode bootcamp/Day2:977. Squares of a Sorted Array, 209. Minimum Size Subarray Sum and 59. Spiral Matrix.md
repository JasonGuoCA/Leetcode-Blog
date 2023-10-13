# [977. Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/description/)

 **代码随想录(programmercarl.com)explanation:**

#### [Video explanation](https://www.bilibili.com/video/BV1QB4y1D7ep )

#### [Article explanation](https://programmercarl.com/0977.%E6%9C%89%E5%BA%8F%E6%95%B0%E7%BB%84%E7%9A%84%E5%B9%B3%E6%96%B9.html)

**Solution**:
```JAVA
class Solution {
    public int[] sortedSquares(int[] nums) {

        int k = nums.length;
        int[] result = new int[k--];

        for(int i = 0, j = k ; i <= j; ){
            
            // The squares of the left number are bigger
            if(nums[i] * nums[i] > nums[j] * nums[j] ){
                result[k--] = nums[i] * nums[i];
                i++;
            } else {
                // The squares of the right number are bigger or equal
                result[k--] = nums[j] * nums[j];
                j--;
            }
        }
        return result;
    }
}
```
# [209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/description/)

**代码随想录(programmercarl.com)explanation:**

#### [Video explanation](https://www.bilibili.com/video/BV1tZ4y1q7XE)

#### [Article explanation](https://programmercarl.com/0209.%E9%95%BF%E5%BA%A6%E6%9C%80%E5%B0%8F%E7%9A%84%E5%AD%90%E6%95%B0%E7%BB%84.html)

**Solution**:
```JAVA
class Solution {
    public int minSubArrayLen(int target, int[] nums) {

      int result = Integer.MAX_VALUE;
      int i = 0;
      int sum = 0;

      for(int j = 0; j < nums.length; j++){
          sum += nums[j];
          while(sum >= target){
              result = Math.min(result, j - i + 1);
              sum -= nums[i++];
          }
      }
      return result = result == Integer.MAX_VALUE ? 0 : result;

    }
}
```

# [59. Spiral Matrix II](https://leetcode.com/problems/spiral-matrix-ii/description/)

**代码随想录(programmercarl.com)explanation:**

#### [Video explanation](https://www.bilibili.com/video/BV1SL4y1N7mV/)

#### [Article explanation](https://programmercarl.com/0059.%E8%9E%BA%E6%97%8B%E7%9F%A9%E9%98%B5II.html)

**Solution**:
```JAVA
class Solution {
    public int[][] generateMatrix(int n) {

        int start = 0;
        int loop = 0;
        int count = 1;
        int[][] result = new int[n][n];
        int i , j;

        while(loop++ < n/2){
            for( j = start; j < n - loop; j++){
                result[start][j] = count ++;
            }
            for( i = start; i < n - loop; i ++){
                result[i][j] = count ++;
            }
            for(; j >= loop; j --){
                result[i][j] = count ++;
            }
            for(; i >= loop; i --){
                result[i][j] = count ++;
            }
            start ++;
        }

        if(n % 2 == 1){
            result[start][start] = count;
        }
        return result;
        
    }
}
```
