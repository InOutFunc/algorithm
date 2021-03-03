## jz7 斐波那契数列

```cpp
class Solution {
public:
    int Fibonacci(int n) {
        vector<int> dp(n + 1);
        dp[0] = 0;
        dp[1] = 1;
        for (int i = 2; i < n + 1; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }
};
```

## jz8 一只青蛙一次可以跳上1级台阶，也可以跳上2级

```cpp
class Solution {
public:
    int jumpFloor(int number) {
        vector<int> dp(number + 1);
        dp[1] = 1;
        dp[2] = 2;
        for (int i = 3; i < number + 1; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[number];
    }
};
```

## jz9 它也可以跳上n级

```cpp
class Solution {
public:
    int jumpFloorII(int number) {
        vector<int> dp(number + 1);
        dp[1] = 1;
        for (int i = 2; i < number + 1; i++) {
            dp[i] = dp[i - 1] * 2;
        }
        return dp[number];
    }
};
```

## jz10 矩形横着或者竖着去覆盖更大的矩形

```cpp
class Solution {
public:
    int rectCover(int number) {
        if (number <= 2) {
            return number;
        }
        return rectCover(number - 1) + rectCover(number - 2);
    }
};
```

