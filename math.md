## jz31 从1 到 n 中1出现的次数

```cpp
class Solution {
public:
    int NumberOf1Between1AndN_Solution(int n)
    {
        int base = 1;
        int res = 0;
        while (n / base > 0) {
            int high = n / base / 10;
            int cur = n / base % 10;
            int low = n % base;
            if (cur == 0) {
                res += high * base;
            } else if (cur == 1) {
                res += (high * base + low + 1);
            } else if (cur > 1) {
                res += (high + 1) * base;
            }
            base *= 10;
        }
        
        return res;
    }
};
```

