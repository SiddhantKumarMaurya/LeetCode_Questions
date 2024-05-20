# [Kth Largest Element in a Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream/description/)
## Topics: `Tree`, `Design`, `Binary Search Tree`, `Heap (Priority Queue)`, `Binary Tree`, `Data Stream`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/1794e5de-d297-46c5-b2cd-6b27f36bddff)
## Solution
```java
import java.util.PriorityQueue;

class KthLargest {
    private PriorityQueue<Integer> minHeap;
    private int k;

    public KthLargest(int k, int[] nums) {
        this.k = k;
        minHeap = new PriorityQueue<>();
        
        for (int num : nums) {
            add(num);
        }
    }

    public int add(int val) {
        if (minHeap.size() < k) {
            minHeap.offer(val);
        } else if (val > minHeap.peek()) {
            minHeap.poll();
            minHeap.offer(val);
        }
        return minHeap.peek();
    }
}

/**
 * Your KthLargest object will be instantiated and called as such:
 * KthLargest obj = new KthLargest(k, nums);
 * int param_1 = obj.add(val);
 */
```
---
## Solution
```java
class KthLargest {
    int[] minHeap;
    int k;

    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }

    private void heapify(int[] nums, int i) {
        int minChild = 2*i + 1;
        if(minChild + 1 < nums.length && nums[minChild+1] < nums[minChild]) minChild += 1;
        //System.out.println(minChild + " " + i);
        if(minChild < nums.length && nums[minChild] < nums[i]) {
            swap(nums, i, minChild);
            heapify(nums, minChild);
        }
    }

    private void addInHeap(int[] minHeap, int val) {
        //System.out.println(val);
        if(val > minHeap[0]) {
            minHeap[0] = val;
            heapify(minHeap, 0);
        }
    }

    private void printHeap(int[] minHeap) {
        for(int i = 0; i< minHeap.length; i++) {
            System.out.print(minHeap[i] + " ");
        }
        System.out.println("");
    }

    public KthLargest(int k, int[] nums) {
        minHeap = new int[k];
        for(int i = 0; i<k; i++) {
            minHeap[i] = Integer.MIN_VALUE;
        }
        for(int i = 0; i<k&&i<nums.length; i++) {
            minHeap[i] = nums[i];
        }
        for(int i = minHeap.length/2; i>=0; i--) {
            heapify(minHeap, i);
        }
        for(int i = k; i<nums.length; i++) {
            addInHeap(minHeap, nums[i]);
        }
    }
    
    public int add(int val) {
        addInHeap(minHeap, val);
        //printHeap(minHeap);
        return minHeap[0];
    }
}


/**
 * Your KthLargest object will be instantiated and called as such:
 * KthLargest obj = new KthLargest(k, nums);
 * int param_1 = obj.add(val);
 */
```
