## 295. Find Median from Data Stream

```cpp
class MedianFinder {
public:
    /** initialize your data structure here. */
    MedianFinder() {
        
    }
    
    void addNum(int num) {
        smallData.push(num);
        largeData.push(smallData.top());
        smallData.pop();
        if (smallData.size() < largeData.size()) {
            smallData.push(largeData.top());
            largeData.pop();
        }
    }
    
    double findMedian() {
        if (smallData.size() > largeData.size()) {
            return smallData.top();
        }
        return (smallData.top() + largeData.top()) / 2.0;
    }
private:
    priority_queue<int> smallData;
    priority_queue<int, vector<int>, greater<>> largeData;
};

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder* obj = new MedianFinder();
 * obj->addNum(num);
 * double param_2 = obj->findMedian();
 */
```

