

## 146. LRU Cache

```cpp
class LRUCache {
public:
    LRUCache(int capacity) {
        cap = capacity;
    }
    
    int get(int key) {
        if (index.find(key) == index.end()) {
            return -1;
        }
        touch(index[key]);
        return nums.front().second;
    }
    
    void put(int key, int value) {
        if (index.find(key) != index.end()) {
            touch(index[key]);
            nums.front().second = value;
            return;
        }
        if (nums.size() == cap) {
            int delkey = nums.back().first;
            index.erase(delkey);
            nums.pop_back();
        }
        nums.push_front({key, value});
        index[key] = nums.begin();
    }
    
private:
    int cap;
    using pList = list<pair<int, int>>;
    unordered_map<int, pList::iterator> index;
    pList nums;
    
    void touch(pList::iterator num)
    {
        int key = num->first;
        int value = num->second;
        nums.erase(num);
        nums.push_front({key, value});
        index[key] = nums.begin();
    }
    
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```

## 155. Min Stack

```cpp
class MinStack {
public:
    /** initialize your data structure here. */
    MinStack() {
        
    }
    
    void push(int x) {
        s1.push(x);
        if (s2.empty() || x <= s2.top()) {
            s2.push(x);
        }
    }
    
    void pop() {
        if (s1.top() == s2.top()) {
            s2.pop();
        }
        s1.pop();
        
    }
    
    int top() {
        return s1.top();
    }
    
    int getMin() {
        return s2.top();
    }
private:
    stack<int> s1;
    stack<int> s2;
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(x);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */
```

