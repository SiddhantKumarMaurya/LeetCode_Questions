# [Top K Frequent Element](https://leetcode.com/problems/top-k-frequent-elements/)
## Topics: `Array`, `Hash Table`, `Divide and Conquer`, `Sorting`, `Heap (Priority Queue)`, `Bucket Sort`, `Counting`, `Quickselect`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/505cd54b-fd16-4d8f-ba62-f0cac5fdf359)
## Solution (Incorrect)
```java
import java.util.HashMap;
import java.util.HashSet;
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        int length = nums.length;
        int maxFrequency = 0;

        HashMap<Integer, Integer> map = new HashMap<>();
        HashSet<Integer> set = new HashSet<>();

        for (int i = 0; i < length; i++) {
            int currentFrequency = map.getOrDefault(nums[i], 0) + 1;
            if (currentFrequency > maxFrequency) maxFrequency = currentFrequency;
            else if (currentFrequency == maxFrequency) {
                // now, another problem arises how to get the key for the value
                // and even if we add it to the set iterating through the set is going to be difficult becuase then we cannot decrement the value of maxFrequency on line 31 untill all the the keys have been added in the topKFreqeuntElements array.
                set.add()
            }
            map.put(nums[i], currentFrequency);
        }

        int[] topKFreqeuntElements = new int[k];

        int i = 0;
        while (maxFrequency != 0 && i < k) {
            // this will return the key if it exits but what if there are more than one keys
            // to solve this problem we should use set
            if (map.containsValue(maxFrequency)) {
                topKFrequentElements[i] = map.getKey(maxFrequency);
                i++;
            }
            maxFrequency--;
        } 
        return topKFreqeuntElements;
        
    }
}
```
---
## Solution
```java
import java.util.*;

class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        // Step 1: Create a HashMap to count the frequency of each element
        Map<Integer, Integer> frequencyMap = new HashMap<>();
        for (int num : nums) {
            frequencyMap.put(num, frequencyMap.getOrDefault(num, 0) + 1);
        }
        
        // Step 2: Create a PriorityQueue (min heap) to store elements based on their frequency
        PriorityQueue<Integer> minHeap = new PriorityQueue<>(Comparator.comparingInt(frequencyMap::get));
        
        // Step 3: Iterate through the HashMap and add elements to the PriorityQueue
        for (int num : frequencyMap.keySet()) {
            minHeap.offer(num);
            // Step 4: If the size of the PriorityQueue exceeds k, remove the element with the lowest frequency
            if (minHeap.size() > k) {
                minHeap.poll();
            }
        }
        
        // Step 5: Create an array to store the top k frequent elements
        int[] result = new int[k];
        int index = 0;
        // Step 6: Pop elements from the PriorityQueue and store them in the result array
        while (!minHeap.isEmpty()) {
            result[index++] = minHeap.poll();
        }
        return result;
    }
}
```
---
## Solution
```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer,Integer> map = new HashMap<>();
        for(int num : nums){
            map.put(num,map.getOrDefault(num,0)+1);
        }
        PriorityQueue<Integer> heap = new PriorityQueue<>((n1,n2) -> map.get(n1)-map.get(n2));
        for(int num : map.keySet()){
            heap.add(num);
            if(heap.size() > k){
                heap.remove();
            }
        }
        int[] ans = new int[k];
        for(int i = 0 ; i < k ; i++){
            ans[i] = heap.remove();
        }
        return ans;
    }
}
```
---
## Solution
```java
class Solution {
//     input: nums arr, output: int arr, constraints: count all items in arr best time O(nlogn), space: O(n), edge cases: all 1 item and ask for top 2, empty arr, top 2 and there's a tie between 2nd and 3rd
//     testing: all 1 item and ask for top 2 -> [num], empty arr -> [], top 2 and there's a tie between 2nd and 3rd -> [num1, num2] either
//     strategy
//     hashmap to track the count so far
//     heap to store item and count
//     pop items from heap till set is of a particular size
//     return set as array
    public int[] topKFrequent(int[] nums, int k) {
        // int: count
        Map<Integer, Integer> map = new HashMap();
//         {[num: count]}
        PriorityQueue<int[]> queue = new PriorityQueue<int[]>((a, b) -> b[1] - a[1]);
        for(int num: nums) 
            map.put(num, map.getOrDefault(num, 0) + 1);
        
        for(Map.Entry<Integer, Integer> entry: map.entrySet())
            queue.add(new int[]{entry.getKey(), entry.getValue()});
        
        int[] result = new int[k];
        int i = 0;
        while(k > 0 && !queue.isEmpty()){
            result[i++] = queue.poll()[0];
            k--;
        }
        
        return result;
    }
}
```

