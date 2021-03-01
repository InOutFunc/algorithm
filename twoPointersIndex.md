

## 75. Sort Colors

```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int zeros = 0;
        int twos = nums.size() - 1;
        for (int i = 0; i <= twos;) {
            if (nums[i] == 0) {
                swap(nums[i], nums[zeros++]);
                i++;
                continue;
            }
            if (nums[i] == 2) {
                swap(nums[i], nums[twos--]);
                continue;
            }
            i++;
        }
    }
};
```

## 283. Move Zeroes

```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int i = 0;
        for (int j = 0; j < nums.size(); j++) {
            if (nums[j] != 0) {
                nums[i++] = nums[j];
            }
        }
        while (i < nums.size()) {
            nums[i] = 0;
            i++;
        }
    }
};
```

