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

## 394. Decode String

```cpp
class Solution {
public:
    string decodeString(string s) {
        string cur;
        stack<string> tmpStr;
        int count;
        stack<int> tmpCnt;
        for (char ch : s) {
            if (isdigit(ch)) {
                count = count * 10 + (ch - '0');
            } else if (ch == '[') {
                tmpStr.push(cur);
                cur.clear();
                tmpCnt.push(count);
                count = 0;
            } else if (ch == ']') {
                string pre = tmpStr.top();
                tmpStr.pop();
                int tmp = tmpCnt.top();
                tmpCnt.pop();
                while (tmp > 0) {
                    pre += cur;
                    tmp--;
                }
                cur = pre;
            } else {
                cur += string(1, ch);
            }
        }
        
        return cur;
    }
};
```

