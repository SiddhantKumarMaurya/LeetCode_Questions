# [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/description/)
## Problem Statement
![image](https://github.com/SiddhantKumarMaurya/LeetCode_Questions/assets/107787014/9f782f9c-fb49-490d-bec3-b2fefbc6ff54)
## Solutions:
### Java
``` java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> leftSymbols = new Stack<>();
        for (char c: s.toCharArray()) {
            if (c == '(' || c == '{' || c == '[') {
                leftSymbols.push(c);
            } else if (c == ')' && !leftSymbols.isEmpty() && leftSymbols.peek() == '(') {
                leftSymbols.pop();
            } else if (c == '}' && !leftSymbols.isEmpty() && leftSymbols.peek() == '{') {
                leftSymbols.pop();
            } else if (c == ']' && !leftSymbols.isEmpty() && leftSymbols.peek() == '[') {
                leftSymbols.pop();
            } else {
                return false;
            }
        }
        return leftSymbols.isEmpty();
    }
}
```
### Python
``` python
class Solution:
    def isValid(self, s: str) -> bool:
        left_symbols = []
        mapping = {')': '(', '}': '{', ']': '['}

        for char in s:
            if char in '({[':
                left_symbols.append(char)
            elif char in ')}]':
                if not left_symbols or left_symbols.pop() != mapping[char]:
                    return False

        return not left_symbols
```
### JavaScript
``` javascript
var isValid = function(s) {
    const leftSymbols = [];
    const mapping = {')': '(', '}': '{', ']': '['};

    for (const char of s) {
        if (char === '(' || char === '{' || char === '[') {
            leftSymbols.push(char);
        } else if (char === ')' || char === '}' || char === ']') {
            if (!leftSymbols.length || leftSymbols.pop() !== mapping[char]) {
                return false;
            }
        }
    }

    return leftSymbols.length === 0;
};
```
### Lua
``` lua
function isValid(s)
    local leftSymbols = {}
    local mapping = { [")"] = "(", ["}"] = "{", ["]"] = "[" }

    for char in s:gmatch(".") do
        if char == "(" or char == "{" or char == "[" then
            table.insert(leftSymbols, char)
        elseif char == ")" or char == "}" or char == "]" then
            if #leftSymbols == 0 or leftSymbols[#leftSymbols] ~= mapping[char] then
                return false
            end
            table.remove(leftSymbols)
        end
    end

    return #leftSymbols == 0
end
```
### C++
``` c++
#include <stack>
#include <string>

class Solution {
public:
    bool isValid(std::string s) {
        std::stack<char> leftSymbols;
        std::unordered_map<char, char> mapping = {{')', '('}, {']', '['}, {'}', '{'}};

        for (char c : s) {
            if (c == '(' || c == '{' || c == '[') {
                leftSymbols.push(c);
            } else if (c == ')' || c == '}' || c == ']') {
                if (leftSymbols.empty() || leftSymbols.top() != mapping[c]) {
                    return false;
                }
                leftSymbols.pop();
            }
        }

        return leftSymbols.empty();
    }
};
```
### C
``` c
#include <stdbool.h>
#include <stdlib.h>
#include <string.h>

struct Stack {
    char data;
    struct Stack* next;
};

typedef struct Stack Stack;

Stack* createStack() {
    return NULL;
}

void push(Stack** top, char data) {
    Stack* newStack = (Stack*)malloc(sizeof(Stack));
    newStack->data = data;
    newStack->next = *top;
    *top = newStack;
}

char pop(Stack** top) {
    if (*top == NULL) {
        return '\0';
    }
    char data = (*top)->data;
    Stack* temp = *top;
    *top = (*top)->next;
    free(temp);
    return data;
}

bool isValid(char* s) {
    Stack* leftSymbols = createStack();
    char mapping[256] = {0};
    mapping[')'] = '(';
    mapping['}'] = '{';
    mapping[']'] = '[';

    int length = strlen(s);

    for (int i = 0; i < length; i++) {
        char c = s[i];
        if (c == '(' || c == '{' || c == '[') {
            push(&leftSymbols, c);
        } else if (c == ')' || c == '}' || c == ']') {
            char topChar = pop(&leftSymbols);
            if (topChar != mapping[c]) {
                return false;
            }
        }
    }

    return leftSymbols == NULL;
}
```
