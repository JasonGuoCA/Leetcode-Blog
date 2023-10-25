# [242. Valid Anagram(Easy)](https://leetcode.com/problems/valid-anagram/)

 **代码随想录(programmercarl.com)explanation:**
#### [Video explanation](https://www.bilibili.com/video/BV1YG411p7BA/)

#### [Article explanation](https://programmercarl.com/0242.%E6%9C%89%E6%95%88%E7%9A%84%E5%AD%97%E6%AF%8D%E5%BC%82%E4%BD%8D%E8%AF%8D.html)

**Solution**:

The problem is solved by using **hash array**.

Firstly, define a hash array, The input strings are all lowercase English letters, so the length of the array is 26.

Secondly, in Loop string s, the array corresponding to that letter is **+1** at each loop.

Thirdly, Loop string t, the array corresponding to that letter is **-1** at each loop.

At last, Confirm the values of the array are **totally 0**, if all 0, return string s and t are anagrams.

**Time Complexity:O(n)**

**Space Complexity:O(1)**

```JAVA
class Solution {
    public boolean isAnagram(String s, String t) {

        /// Define a hash array, input strings are all lowercase English letters, so the length of array is 26.
        // a belongs to int[0], and so on, z corresponds int[25], and all values are 0
        int[] hashArray = new int[26];

        // Loop string s, the array corresponding to that letter is +1 at each loop
        for(int i = 0; i < s.length(); i ++){
            hashArray[s.charAt(i) - 'a'] ++;
        }

        // Loop string t, the array correspoonding to that letter is -1 at each loop
        for(int i = 0; i < t.length(); i ++){
            hashArray[t.charAt(i) - 'a'] --;
        }

        // Conform the values of the array are totally 0, if all 0, return string s and t are anagram.
        for(int record : hashArray){
            if(record != 0){
                return false;
            }
        }
        return true;
        
    }
}
```

# [349. Intersection of Two Arrays(Easy)](https://leetcode.com/problems/intersection-of-two-arrays/)

 **代码随想录(programmercarl.com)explanation:**
#### [Video explanation](https://www.bilibili.com/video/BV1ba411S7wu/)

#### [Article explanation](https://programmercarl.com/0349.%E4%B8%A4%E4%B8%AA%E6%95%B0%E7%BB%84%E7%9A%84%E4%BA%A4%E9%9B%86.html)

**Solution**:

The problem is solved by using two methods (**hash set and hash array**).

1. Hash Set

Firstly, define two sets, set 1 can accept the value of the input array nums1, then **compare it with  the value of set 1 and the array nums2**, 
the same values are saved in set 2.

At last,  store/save the value of set 2 in the array, and return it

**Time Complexity:O(m + n)**

**Space Complexity:O(n)**

```JAVA
class Solution {

    public int[] intersection(int[] nums1, int[] nums2) {

        // when input array nums1 and nums2 are null, return new int[0]
        if(nums1 == null || nums1.length == 0 || nums2 == null || nums2.length == 0){
            return new int[0];
        }

        // Define two sets, set 1 can accept the value of the array nums1,
        // then compare with  the value fo the set 1 and the array nums2, the same values are saved in set 2
        Set<Integer> set1 = new HashSet<>();
        Set<Integer> resultSet = new HashSet<>();

        // Loop of nums 1, and the value are saved in set 1
        for(int i : nums1)
            set1.add(i);

        // Loop of nums2, and compare with the value of nums2 and set1, the same values are saved in resutlSet
        for(int i : nums2){
            if(set1.contains(i)){
                resultSet.add(i);
            }
        }
        
         // Return method 1
        // Define the  return array
        int[] resultArr = new int[resultSet.size()];

        // The values of resultSet are saved in the array resultArr
        int j = 0;
        for(int i : resultSet){
            resultArr[j ++] = i;
        }

        return resultArr;

        // Return method 2
        return resultSet.stream().mapToInt(x -> x).toArray();
    }
}
```

2. Hash Array

Solution:

Define two hash arrays, the values of the input array1 are saved in the index of the new hash array1,  and the values of the new hash array1 are plus 1.
then the values of the input array2 are saved in the index of the new hash array2, and the values are plus 1.
After that loop the new arrays 1 and 2, and **confirm the values of them are totally bigger than 0 in each loop**,
if yes, it's the intersection, save it, and at last return the result.

```JAVA
class Solution {

    public int[] intersection(int[] nums1, int[] nums2) {

        // Define two hash Array
        int[] hashArr1 = new int[1001];
        int[] hashArr2 = new int[1001];

        // the value of nums1 and nums2 are saved in the index of hashArr1 and hashArr2
        for(int i : nums1)
            hashArr1[i] ++;

        for(int i : nums2)
            hashArr2[i] ++;

        // Loop the array hashArr1 and hashArr2, when the value are greater than 0, the indexs are saved in the new list
        List<Integer> resultList = new ArrayList<>();
        for(int i = 0; i < 1001; i ++){
            if(hashArr1[i] > 0 && hashArr2[i] > 0){
                resultList.add(i);
            }
        }

        // Define a array to get the result value
        int[] resultArr = new int[resultList.size()];
        int j = 0;
        for(int i : resultList)
            resultArr[j ++] = i;

        return resultArr;
    }
}
```

# [202. Happy Number(easy)](https://leetcode.com/problems/happy-number/)

 **代码随想录(programmercarl.com)explanation:**

#### [Article explanation](https://programmercarl.com/0202.%E5%BF%AB%E4%B9%90%E6%95%B0.html/)

**Solution**:

This problem can use recursion

Firstly, define a hash set to save the processing data.

Secondly, while condition: n == 1 means it's a happy number.  **set. contains(n): means enter an infinite loop.**
Input: n = 19
Explanation:
1^2 + 9^2 = 82
method： **n%10 means can get single digit 9**
                 **n /10 then n %10 can get tens digit 1**
             
**Time Complexity:O(logn)**

**Space Complexity:O(logn)**

```JAVA
class Solution {
    public boolean isHappy(int n) {

        // Define a set
        Set<Integer> record = new HashSet<>();

        // when n and 1 are not equal or n is not repeated/recurrence in a loop, the loop is continue
        while(n != 1 && !record.contains(n)){
             record.add(n);
             n = getNumber(n);
        }

    return n == 1;
        
        
    }

    private int getNumber(int n){

        int res = 0;

        // when a is bigger than 0,  calculate the number by the sum of the squares of its digits
        while(n > 0){

            int temp = n % 10;
            res += temp * temp;
            n = n / 10;
        }

        return res;
    }
}
```
# [1. Two Sum(Easy)](https://leetcode.com/problems/two-sum/)

 **代码随想录(programmercarl.com)explanation:**
#### [Video explanation](https://www.bilibili.com/video/BV1aT41177mK/)

#### [Article explanation](https://programmercarl.com/0001.%E4%B8%A4%E6%95%B0%E4%B9%8B%E5%92%8C.html)

**Solution**:

The problem is solved by using **hash map**.

Firstly, loop the input array nums, and calculate the difference between the target and the input array.

Secondly, confirm the difference exists in the input array, it can use the hash map too.  If has， it‘s the right answer, saved in the array, and at last, return it.

**Time Complexity:O(n)**

**Space Complexity:O(n)**

```JAVA
class Solution {
    public int[] twoSum(int[] nums, int target) {

        // Define a int array to save the result
        int[] resArr = new int[2];

        // if input nums is null or its length is 0, return a empty array
        if(nums == null || nums.length == 0){
            return resArr;
        }

         // Define a hash map to save the value of the array nums
        Map<Integer,Integer> numsMap = new HashMap<>();

        // Loop of the array nums
        for(int i = 0; i < nums.length; i ++){
            
            // Calcuate the difference of the target and the value per loop
            int cou = target - nums[i];
            
            // If the difference is exist in the map, it can get the result array
            if(numsMap.containsKey(cou)){
                resArr[1] = i;
                resArr[0] = numsMap.get(cou);
                break;
            }
            numsMap.put(nums[i] , i);

        }
        return resArr;
        
    }
}
```
