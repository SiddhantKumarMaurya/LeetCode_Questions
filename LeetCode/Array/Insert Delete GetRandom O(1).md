# [Insert Delete GetRandom O(1)](https://leetcode.com/problems/insert-delete-getrandom-o1/description/?envType=study-plan-v2&envId=top-interview-150)
## Topics: `Array`, `HashTable`, `Math`, `Design`, `Randomized`
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/9c912b4a-5247-4afd-b908-4862fd8cb954)
## Solution
```java
// Time taken: 128 ms.
import java.util.HashSet;
import java.util.ArrayList;
import java.util.Random;

class RandomizedSet {
    HashSet<Integer> set;
    Random random;
    public RandomizedSet() {
        this.set = new HashSet<>();
        random = new Random();
    }
    
    public boolean insert(int val) {
        if(this.set.contains(val)) return false;
        else {
            this.set.add(val);
            return true;
        }
    }
    
    public boolean remove(int val) {
        if(!this.set.contains(val)) return false;
        else {
            this.set.remove(val);
            return true;
        }
    }
    
    public int getRandom() {
        ArrayList<Integer> arrayList = new ArrayList<>(this.set);
        int randomIndex = this.random.nextInt(arrayList.size());
        return arrayList.get(randomIndex);
    }
}

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet obj = new RandomizedSet();
 * boolean param_1 = obj.insert(val);
 * boolean param_2 = obj.remove(val);
 * int param_3 = obj.getRandom();
 */
```
---
## Solution
```java
import java.util.HashMap;
import java.util.ArrayList;
import java.util.Random;

class RandomizedSet {
    HashMap<Integer, Integer> map;
    ArrayList<Integer> list;
    Random random;
    
    public RandomizedSet() {
        this.map = new HashMap<>();
        this.list = new ArrayList<>();
        this.random = new Random();
    }
    
    public boolean insert(int val) {
        if (map.containsKey(val)) return false;
        
        map.put(val, list.size());
        list.add(val);
        return true;
    }
    
    public boolean remove(int val) {
        if (!map.containsKey(val)) return false;
        
        int index = map.get(val);
        int lastElement = list.get(list.size() - 1);
        
        // Swap the element to be removed with the last element
        list.set(index, lastElement);
        map.put(lastElement, index);
        
        // Remove the last element from the list and map
        list.remove(list.size() - 1);
        map.remove(val);
        
        return true;
    }
    
    public int getRandom() {
        int randomIndex = random.nextInt(list.size());
        return list.get(randomIndex);
    }
}

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet obj = new RandomizedSet();
 * boolean param_1 = obj.insert(val);
 * boolean param_2 = obj.remove(val);
 * int param_3 = obj.getRandom();
 */
```
