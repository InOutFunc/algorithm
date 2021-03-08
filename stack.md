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

## jz5 用两个栈来实现一个队列

```cpp
class Solution
{
public:
    void push(int node) {
        stack1.push(node);
    }

    int pop() {
        if (stack2.empty()) {
            while (!stack1.empty()) {
                stack2.push(stack1.top());
                stack1.pop();
            }
        }
        int tmp = stack2.top();
        stack2.pop();
        return tmp;
    }

private:
    stack<int> stack1;
    stack<int> stack2;
};
```

## jz21 请判断第二个序列是否可能为该栈的弹出顺序

```cpp
class Solution {
public:
    bool IsPopOrder(vector<int> pushV,vector<int> popV) {
        stack<int> st;
        int index = 0;
        for (int i = 0; i < pushV.size(); i++) {
            st.push(pushV[i]);
            while (!st.empty() && st.top() == popV[index]) {
                st.pop();
                index++;
            }
        }
        
        return st.empty();
    }
};
```

## jz20 能够得到栈中所含最小元素的min函数

```cpp
class Solution {
public:
    void push(int value) {
        st1.push(value);
        if (st2.empty() || value <= st2.top()) {
            st2.push(value);
        }
    }
    void pop() {

        if (st2.top() == st1.top()) {
            st2.pop();
        }
        st1.pop();
    }
    int top() {
        return st1.top();
    }
    int min() {
        return st2.top();
    }

private:
    stack<int> st1;
    stack<int> st2;
};
```

