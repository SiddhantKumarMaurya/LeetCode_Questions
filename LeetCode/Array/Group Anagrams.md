# [Group Anagrams](https://leetcode.com/problems/group-anagrams/description/)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/ce377f24-b2b0-41d4-bb40-99a1b91d176c)
## Solutions
### Java (Incorrect)
``` java
Group anagrams:
import java.util.Arrays;

class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        int length = strs.length;
        List<List<String>> result = new ArrayList<>();
        List<String> row;

        // List<String> row = new List<String>();
        // List<row> result = new List<row>();
        String uniqueStrs[] = new String[length];
        // Arrays.fill(uniqueStrs, null); // Initialize the array with null values

        for (int i = 0; i < length; i++) {
            char charArr[] = strs[i].toCharArray();
            Arrays.sort(charArr);
            String arrangedStr = Arrays.toString(charArr);
            if (i == 0) {
                Arrays.fill(uniqueStrs, arrangedStr);
            } else {
                Arrays.sort(uniqueStrs);
                int res = Arrays.binarySearch(uniqueStrs, arrangedStr);
                boolean test = res >= 0 ? true : false;
                if (!test) {
                    uniqueStrs[i] = arrangedStr;// Everytime the element is being replaced,
                    // this is not good because we might need the replaced string for later use
                } else {
                    continue;
                
                }
            }
            row = new ArrayList<String>();
            for (int j = i; j < length; j++) {
                charArr = strs[j].toCharArray();
                Arrays.sort(charArr);
                String nextArrangedStr = Arrays.toString(charArr);
                if(nextArrangedStr.equals(arrangedStr)) {
                    row.add(strs[j]);
                }
            }
            result.add(row);
        }
        return result;
    }
}
```
### Java (Correct but time complexity is very high)
``` java
// 111 / 119 test cases passed. Correct solution but time complexity is O(N * K * log(K))

import java.util.Arrays;
import java.util.Collections;

class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        int length = strs.length;
        List<List<String>> result = new ArrayList<>();
        List<String> row;
        ArrayList<String> uniqueStrs = new ArrayList<>();

        // List<String> row = new List<String>();
        // List<row> result = new List<row>();
        // Arrays.fill(uniqueStrs, null); // Initialize the array with null values

        for (int i = 0; i < length; i++) {
            char charArr[] = strs[i].toCharArray();
            Arrays.sort(charArr);
            String arrangedStr = Arrays.toString(charArr);
            Collections.sort(uniqueStrs);
            boolean res = uniqueStrs.contains(arrangedStr);
            if (!res) {
                uniqueStrs.add(arrangedStr);
            } else {
                continue;
            
            }
            row = new ArrayList<String>();
            for (int j = i; j < length; j++) {
                charArr = strs[j].toCharArray();
                Arrays.sort(charArr);
                String nextArrangedStr = Arrays.toString(charArr);
                if(nextArrangedStr.equals(arrangedStr)) {
                    row.add(strs[j]);
                }
            }
            result.add(row);
        }
        return result;
    }
}
```
### Java
``` java
import java.util.*;

class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        // Initialize a map to store groups of anagrams.
        Map<String, List<String>> anagramGroups = new HashMap<>();

        // Iterate through each string in the input array 'strs'.
        for (String str : strs) {
            // Convert the string 'str' to a character array.
            char[] charArr = str.toCharArray();

            // Sort the character array 'charArr' to obtain a sorted representation of the string.
            Arrays.sort(charArr);

            // Create a new string 'sortedStr' from the sorted character array.
            String sortedStr = new String(charArr);

            // Check if 'anagramGroups' already contains 'sortedStr' as a key.
            if (!anagramGroups.containsKey(sortedStr)) {
                // If not, create a new entry in 'anagramGroups' with 'sortedStr' as the key
                // and initialize an empty list as its corresponding value.
                anagramGroups.put(sortedStr, new ArrayList<>());
            }

            // Add the original string 'str' to the list associated with 'sortedStr' in 'anagramGroups'.
            anagramGroups.get(sortedStr).add(str);
        }

        // Convert the values (lists of anagrams) from 'anagramGroups' to a list of lists
        // and return it as the final result.
        return new ArrayList<>(anagramGroups.values());
    }

    public static void main(String[] args) {
        Solution solution = new Solution();

        // Example input
        String[] strs = {"eat", "tea", "tan", "ate", "nat", "bat"};

        // Group anagrams
        List<List<String>> groupedAnagrams = solution.groupAnagrams(strs);

        // Print the grouped anagrams
        for (List<String> group : groupedAnagrams) {
            System.out.println(group);
        }
    }
}

```
### Python
``` python
from collections import defaultdict

class Solution:
    def groupAnagrams(self, strs):
        anagram_groups = defaultdict(list)

        for str in strs:
            sorted_str = ''.join(sorted(str))
            anagram_groups[sorted_str].append(str)

        return list(anagram_groups.values())

# Example input
strs = ["eat", "tea", "tan", "ate", "nat", "bat"]

solution = Solution()
grouped_anagrams = solution.groupAnagrams(strs)
for group in grouped_anagrams:
    print(group)
```
### JavaScript
``` javascript
class Solution {
    groupAnagrams(strs) {
        const anagramGroups = new Map();

        for (const str of strs) {
            const sortedStr = str.split('').sort().join('');
            if (!anagramGroups.has(sortedStr)) {
                anagramGroups.set(sortedStr, []);
            }
            anagramGroups.get(sortedStr).push(str);
        }

        return Array.from(anagramGroups.values());
    }
}

// Example input
const strs = ["eat", "tea", "tan", "ate", "nat", "bat"];

const solution = new Solution();
const groupedAnagrams = solution.groupAnagrams(strs);
groupedAnagrams.forEach(group => console.log(group));
```
### Lua
``` lua
function groupAnagrams(strs)
    local anagramGroups = {}

    for _, str in ipairs(strs) do
        local sortedStr = table.concat({string.byte(str, 1, -1)}):gsub(".", function(c) return string.char(c) end)
        anagramGroups[sortedStr] = anagramGroups[sortedStr] or {}
        table.insert(anagramGroups[sortedStr], str)
    end

    local result = {}
    for _, group in pairs(anagramGroups) do
        table.insert(result, group)
    end

    return result
end

-- Example input
local strs = {"eat", "tea", "tan", "ate", "nat", "bat"}

local groupedAnagrams = groupAnagrams(strs)
for _, group in ipairs(groupedAnagrams) do
    print(table.concat(group, ", "))
end
```
### C++
``` c++
#include <iostream>
#include <vector>
#include <unordered_map>
#include <algorithm>

class Solution {
public:
    std::vector<std::vector<std::string>> groupAnagrams(std::vector<std::string>& strs) {
        std::unordered_map<std::string, std::vector<std::string>> anagramGroups;

        for (const std::string& str : strs) {
            std::string sortedStr = str;
            std::sort(sortedStr.begin(), sortedStr.end());
            anagramGroups[sortedStr].push_back(str);
        }

        std::vector<std::vector<std::string>> result;
        for (const auto& entry : anagramGroups) {
            result.push_back(entry.second);
        }

        return result;
    }
};

int main() {
    Solution solution;

    // Example input
    std::vector<std::string> strs = {"eat", "tea", "tan", "ate", "nat", "bat"};

    std::vector<std::vector<std::string>> groupedAnagrams = solution.groupAnagrams(strs);
    for (const std::vector<std::string>& group : groupedAnagrams) {
        for (const std::string& str : group) {
            std::cout << str << " ";
        }
        std::cout << std::endl;
    }

    return 0;
}
```
### C
``` c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct AnagramGroup {
    char** words;
    int size;
};

struct AnagramGroupList {
    struct AnagramGroup* groups;
    int size;
};

void initGroup(struct AnagramGroup* group) {
    group->words = NULL;
    group->size = 0;
}

void initGroupList(struct AnagramGroupList* groupList) {
    groupList->groups = NULL;
    groupList->size = 0;
}

void addWordToGroup(struct AnagramGroup* group, const char* word) {
    group->size++;
    group->words = (char**)realloc(group->words, group->size * sizeof(char*));
    group->words[group->size - 1] = strdup(word);
}

void addGroupToGroupList(struct AnagramGroupList* groupList, struct AnagramGroup* group) {
    groupList->size++;
    groupList->groups = (struct AnagramGroup*)realloc(groupList->groups, groupList->size * sizeof(struct AnagramGroup));
    groupList->groups[groupList->size - 1] = *group;
    initGroup(group);
}

void freeGroup(struct AnagramGroup* group) {
    for (int i = 0; i < group->size; i++) {
        free(group->words[i]);
    }
    free(group->words);
    group->words = NULL;
    group->size = 0;
}

void freeGroupList(struct AnagramGroupList* groupList) {
    for (int i = 0; i < groupList->size; i++) {
        freeGroup(&groupList->groups[i]);
    }
    free(groupList->groups);
    groupList->groups = NULL;
    groupList->size = 0;
}

int compareChars(const void* a, const void* b) {
    return (*(char*)a - *(char*)b);
}

char* sortString(const char* str) {
    char* sortedStr = strdup(str);
    qsort(sortedStr, strlen(sortedStr), sizeof(char), compareChars);
    return sortedStr;
}

struct AnagramGroupList groupAnagrams(char** strs, int strsSize, int* returnSize) {
    struct AnagramGroupList groupList;
    initGroupList(&groupList);

    struct AnagramGroup currentGroup;
    initGroup(&currentGroup);

    char** sortedStrs = (char**)malloc(strsSize * sizeof(char*));

    for (int i = 0; i < strsSize; i++) {
        sortedStrs[i] = sortString(strs[i]);
    }

    int* visited = (int*)calloc(strsSize, sizeof(int));

    for (int i = 0; i < strsSize; i++) {
        if (!visited[i]) {
            addWordToGroup(&currentGroup, strs[i]);
            for (int j = i + 1; j < strsSize; j++) {
                if (!visited[j] && strcmp(sortedStrs[i], sortedStrs[j]) == 0) {
                    addWordToGroup(&currentGroup, strs[j]);
                    visited[j] = 1;
                }
            }
            addGroupToGroupList(&groupList, &currentGroup);
        }
    }

    *returnSize = groupList.size;
    free(sortedStrs);
    free(visited);

    return groupList;
}

int main() {
    char* strs[] = {"eat", "tea", "tan", "ate", "nat", "bat"};
    int strsSize = sizeof(strs) / sizeof(strs[0]);
    int returnSize;
    
    struct AnagramGroupList group
```
