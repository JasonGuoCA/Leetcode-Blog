# [239. Sliding Window Maximum(Hard)](https://leetcode.com/problems/sliding-window-maximum/)
# [347. Top K Frequent Elements(Midium)](https://leetcode.com/problems/top-k-frequent-elements/)

**解题想法：**

两道题都不容易，花了我很长时间才解决。

**第一题**

滑动窗口取最大值，用DequeQueue这个数据结构，Queue里面是**递减**的，这样子最后取头数据就是最大值，

实现方面实例化了add(),poll()和peek()三个方法，

具体操作：add()方法里面会传入的值和queue的尾部进行比较，比尾部数据大的时候尾部数据会删掉，

这是一个**循环**的操作，直到遇到小的时候才会加进来。

poll()方法不是所有的都poll，而是头数据比较，数组**i-k**的值和头数据相等，才会poll，

peek（）就是返回头数据

再主方法处理的时候先循环**0-k**,add()到queue，去一次最大值（头数据）存在新数组。

然后再循环**k-数据长度**，先调用poll（）方法处理数组**i-k**的值，然后add（）数组i的值，再取最大值存在新数组，最后返回新数组。


**第二题**

感觉比第一题更加难一些，用了优先队列小顶推，底层是二叉树的结构，头结点是最小的。

实现方面，定义一个map，key是数组的值，value是相同值出现的次数。

然后定义优先队列，这里lamb表达式里面[1]的意思是去数组里面第二个值，也就是次数。

然后循环map，优先队列size和k比较，小于k全部放入，反之比较优先map.value和优先队列的头数据（最小值）比较（pq.peek()[1]），

**大于**的时候，才需要poll头数据把新的值加进来，反之说明已经是排名再k以外的数据了就不需要加入了。
```JAVA
//在优先队列中存储二元组(num,cnt),cnt表示元素值num在数组中的出现次数
        //出现次数按从队头到队尾的顺序是从小到大排,出现次数最低的在队头(相当于小顶堆)
        PriorityQueue<int[]> pq = new PriorityQueue<>((pair1,pair2)->pair1[1]-pair2[1]);
        for(Map.Entry<Integer,Integer> entry:map.entrySet()){//小顶堆只需要维持k个元素有序
            if(pq.size()<k){//小顶堆元素个数小于k个时直接加
                pq.add(new int[]{entry.getKey(),entry.getValue()});
            }else{
                if(entry.getValue()>pq.peek()[1]){//当前元素出现次数大于小顶堆的根结点(这k个元素中出现次数最少的那个)
                    pq.poll();//弹出队头(小顶堆的根结点),即把堆里出现次数最少的那个删除,留下的就是出现次数多的了
                    pq.add(new int[]{entry.getKey(),entry.getValue()});
                }
            }
        }
```
循环完，取优先队列里面的值，这里面循环的i值要注意，它对应的是新数组的小标，所以需要**k-1**
```JAVA
int[] ans = new int[k];
for(int i=k-1;i>=0;i--){//依次弹出小顶堆,先弹出的是堆的根,出现次数少,后面弹出的出现次数多
            ans[i] = pq.poll()[0];
}
```
最后返回新数组

**Solution Thoughts:**

Both of these two questions were not easy, and it took me a long time to solve them.

For **the first question**: 

It's about sliding window maximum values using the Deque data structure. 

The queue is designed in a way that it maintains a decreasing order inside. 

This way, the maximum value can be obtained by looking at the front of the queue. 

In terms of implementation, I instantiated three methods: add(), poll(), and peek().

Specifically,

in the add() method, the value passed is compared with the tail of the queue, and if it's greater, the tail data is removed. This is a looping operation, and it continues until a smaller value is encountered.

The poll() method doesn't poll all elements but only those that have the same value as the element at index i-k. 

Finally, peek() returns the head data.

In the main method, I iterate from 0 to k, add elements to the queue, and store the maximum value (head data) in a new array. Then, I iterate from k to the length of the data, call the poll() method to handle elements at index i-k, add elements at index i, and then store the maximum value in the new array. Finally, I return the new array.


For the **second question**: 

This one seemed even more challenging than the first question. 

I used a min-heap (priority queue) with a binary tree structure as the underlying data structure, where the head node contains the smallest value.

In terms of implementation, I defined a map where the keys represent the values in the array, and the values represent how many times those values appear. Then, I defined a priority queue where the lambda expression inside sorts the elements based on the second value in the array (the frequency).

I loop through the map, comparing the size of the priority queue with k. 

If it's smaller than k, I add all the elements. If it's larger, I compare the value of the map with the value at the head of the priority queue (pq.peek()[1]). 

If the map value is greater, I remove the head and add the new value. If it's smaller, I consider it as a value outside the top k elements, so it's not added.

After the loop, I extract the values from the priority queue. It's important to note that the loop variable i corresponds to the index in the new array, so it should be k-1.

Finally, I return the new array.
