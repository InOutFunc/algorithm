## 20. Valid Parentheses

```cpp
class Solution {
public:
    bool isValid(string s) {
        stack<char> st;
        for (const auto& item : s) {
            if (item == '(') {
                st.push(')');
            } else if (item == '[') {
                st.push(']');
            } else if (item == '{') {
                st.push('}');
            } else {
                if (st.empty() || st.top() != item) {
                    return false;
                } else {
                    st.pop();
                }
            }
        }
        
        return st.empty();
    }
};
```

##  32. Longest Valid Parentheses

```cpp
class Solution {
public:
    int longestValidParentheses(string s) {
        stack<int> invalid;
        for (int i = 0; i < s.size(); i++) {
            if (s[i] == '(') {
                invalid.push(i);
                continue;
            }
            if (!invalid.empty() && s[invalid.top()] == '(') {
                invalid.pop();
                continue;
            }
            invalid.push(i);
        }
        
        if (invalid.empty()) {
            return s.size();
        }
        int res = 0;
        int r = s.size();
        int l = 0;
        while (!invalid.empty()) {
            l = invalid.top();
            invalid.pop();
            res = max(res, r - l - 1);
            r = l;
        }
        res = max(res, r);
        
        return res;
    }
};
```

