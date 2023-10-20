# [454. 4Sum II(Medium)](https://leetcode.com/problems/4sum-ii/)

 **代码随想录(programmercarl.com)explanation:**
#### [Video explanation](https://www.bilibili.com/video/BV1Md4y1Q7Yh/)

#### [Article explanation](https://programmercarl.com/0454.%E5%9B%9B%E6%95%B0%E7%9B%B8%E5%8A%A0II.html)

**Solution**:

The problem is solved by using **hash map**.

Firstly, loop the input arrays 1 and 2， and save them in a hash map.
           map **key**: sum the array 1 and 2 per loop
                   **value**: number of times the same key appears

Secondly, loop the input arrays 3 and 4, Calculate the **difference** between 0 and the sum of arrays 3 and 4 per loop, and then **confirm the difference exists in the map**. If yes, record the map value(times), at last return the record.

**Time Complexity:O(n^2)**

**Space Complexity:O(n^2)**

```JAVA
class Solution {
    public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {

        // Define a hash map to save the sum of the array nums1 and nums2
        Map<Integer,Integer> sumMap = new HashMap<>();

        // loop the array nums1 and nums2, and the sum of the value per loop are saved in the hash map
        for(int num1 : nums1){
            for(int num2 : nums2){
                
                int sumVal = num1 + num2;
                sumMap.put(sumVal, sumMap.getOrDefault(sumVal , 0)+1 );
            }
        }

        // loop the array nums3 and nums4, and calculate the difference between 1 and the sum of nums3 and nums4 per loop
        // then conform that the difference is exist in the map
        int count = 0;
        for(int num3 : nums3){
            for(int num4 : nums4){

                count += sumMap.getOrDefault(0- (num3 + num4), 0);
                 
            }
        }

        return count;
        
        
    }
}
```

# [383. Ransom Note(Easy)](https://leetcode.com/problems/ransom-note/)

 **代码随想录(programmercarl.com)explanation:**

#### [Article explanation](https://programmercarl.com/0383.%E8%B5%8E%E9%87%91%E4%BF%A1.html)

**Solution**:

The problem is solved by using two methods (**hash array**).

Firstly, define a hash array, 

Loop the string magazine， saved in the array, array **index**: every loop value-'a'  **value**: **plus** 1
Loop the string ransomNote， saved in the array, array index: every loop value-'a'  value: **diminish** 1

// Notice String → char
for(**char c : magazine.toCharArray()**){

At last,  confirm the array, the values are all bigger than 0, and return true.

**Time Complexity:O(n)**

**Space Complexity:O(1)**

```JAVA
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {

        // Define a int array, its length is 26
        int[] recordArr = new int[26];

        // if the length of string rensomNote is bigger than the one of the magazine,
        // it proves that ransomNote can not be constructed by using the letters from magazine,
        // so return false
        if(ransomNote.length() > magazine.length())
            return false;

        // Recuring magazine
        for(char c : magazine.toCharArray())
            recordArr[c - 'a'] ++;
        
        // Recurring ransomNote
        for(char c : ransomNote.toCharArray())
            recordArr[c - 'a'] --;
        
        
        // Recurring the array result
        for(int i : recordArr)
            if(i < 0) return false;

        return true;     
    }


}
```


# [15. 3Sum(Medium)](https://leetcode.com/problems/3sum/)

 **代码随想录(programmercarl.com)explanation:**

#### [Video explanation](https://www.bilibili.com/video/BV1GW4y127qo/)

#### [Article explanation](https://programmercarl.com/0015.%E4%B8%89%E6%95%B0%E4%B9%8B%E5%92%8C.html/)

**Solution**:

This problem can be used by **two-pointers**
Loop the input array, define the **left** and **right** pointers, and sum the loop index, left pointer, and right pointer.
Pay attention to the **de-duplication** process inside

// Sort the input array
  **Arrays**.**sort**(nums);
// Array → List
result.add(**Arrays.asList**(nums[i] , nums[left] , nums[right]));

**Time Complexity: O(n^2)**

**Space Complexity:O(1)**

```JAVA
lass Solution {
    public List<List<Integer>> threeSum(int[] nums) {

        // Define a list to save the result
        List<List<Integer>> result = new ArrayList<>();

        // Sort the input array
        Arrays.sort(nums);

        // Consurring the input array
        for(int i = 0; i < nums.length; i ++){

            // The first value of nums is bigger than 0 ,return the empty list
            if(nums[i] > 0) return result;

            // If there is the same value in the nums, jump to the next loop.
            if(i > 0 && nums[i] == nums[i - 1]) continue;
            
            // using double pointers, define left and right pointers
            int left = i + 1;
            int right = nums.length - 1;

            while(right > left) {
                
                // Calculate the 3sum
                int sum = nums[i] + nums[left] + nums[right];
                
                // If 3sum is bigger than 0, get the smaller value of the left of the right pointer
                if(sum > 0) right --;
                
                // If 3sum is smaller than 0, get the bigger value of the right of the left pointer
                else if (sum < 0) left ++;
                else{
                    // saving arrays equal to 0 in the result
                    result.add(Arrays.asList(nums[i] , nums[left] , nums[right]));
                    
                    // De-duplication of the right pointer
                    while(right > left && nums[right] == nums[right -1]) right --;
                    
                    // De-duplication of the left pointer
                    while(right > left && nums[left] == nums[left +1]) left ++;
                    
                    right --;
                    left ++;
                }
            }
            

        }
        return result;
        
        
    }
}
```
# [18. 4Sum(Medium)](https://leetcode.com/problems/4sum/)

 **代码随想录(programmercarl.com)explanation:**
#### [Video explanation](https://www.bilibili.com/video/BV1DS4y147US/)

#### [Article explanation](https://programmercarl.com/0018.%E5%9B%9B%E6%95%B0%E4%B9%8B%E5%92%8C.html)

**Solution**:

The problem is solved by using **Two-pointers**.
Adding to the 3sum **the first number of loops to be processed**,
pay attention to the **de-duplication** inside


**Time Complexity:O(n^3)**

**Space Complexity:O(1)**

```JAVA
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {

        // Defint the result list
        List<List<Integer>> result = new ArrayList<>();

        // Sort the input array
        Arrays.sort(nums);

        for(int i = 0; i < nums.length; i ++){

            // The first value is bigger than target and target is bigger than 0, the loop ends
            if(nums[i] > target && target > 0) break;

            // De-duplicate process
            if(i > 0 && nums[i] == nums[i - 1]) continue;

            for(int j = i + 1; j < nums.length; j ++){

                // The first value is bigger than target and target is bigger than 0, the loop ends
                if(nums[i] + nums[j] > target && target > 0) 
                    break;

                // De-duplicate process
                if(j > i + 1 && nums[j] == nums[j - 1]) 
                    continue;

                // using two pointer, defint left and right pointer
                int left = j + 1;
                int right = nums.length - 1;

                while(left < right){

                    // Calculate the 4sum
                    long sum = (long)nums[i] + nums[j] + nums[left] + nums[right];

                    // If sum is bigger than targer, the right pointer moves to one step of the left
                    if(sum > target)
                        right --;
                    
                    // If sum is smaller than targer, the left pointer moves to the right
                    else if(sum < target)
                        left ++;

                    else{
                        result.add(Arrays.asList(nums[i], nums[j], nums[left], nums[right]));

                        // De-Duplicate process
                        while(left < right && nums[left] == nums[left + 1])
                            left ++;
                        while(left < right && nums[right] == nums[right - 1])
                            right --;

                        left ++;
                        right --;

                    }
                }



            }

        }
        return result;   
    }
}
```
