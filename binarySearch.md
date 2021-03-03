## 4. Median of Two Sorted Arrays

```cpp
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        if (nums1.size() > nums2.size()) {
            return findMedianSortedArrays(nums2, nums1);
        }
        std::sort(nums1.begin(), nums1.end());
        std::sort(nums2.begin(), nums2.end());
        int n1 = nums1.size();
        int n2 = nums2.size();
        int l = 0;
        int r = n1;
        while (l <= r) {
            int i = l + (r - l) / 2;
            int j = (n1 + n2 + 1) / 2 - i;
            
            int maxLx = (i == 0) ? -pow(2, 31) : nums1[i - 1];
            int minRx = (i == n1) ? pow(2, 31) - 1 : nums1[i];
            
            int maxLy = (j == 0) ? -pow(2, 31) : nums2[j - 1];
            int minRy = (j == n2) ? pow(2, 31) - 1 : nums2[j];
            
            // cout << i << j << maxLx << maxLy << minRx << minRy << endl;
            if (maxLx <= minRy && maxLy <= minRx) {
                if ((n1 + n2) % 2 == 0) {
                    return (std::max(maxLx, maxLy) + std::min(minRx, minRy)) / 2.0;
                } else {
                    return std::max(maxLx, maxLy);
                }
            } else if (maxLx > minRy) {
                r = i - 1;
            } else {
                l = i + 1; // to be understood
            }
        }
        return 0;
    }
};
```

## 33. Search in Rotated Sorted Array

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int l = 0;
        int r = nums.size() - 1;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] == target) {
                return mid;
            }
            if (nums[mid] > nums[r]) {
                if (target >= nums[l] && target <= nums[mid]) {
                    r = mid - 1;
                } else {
                    l = mid + 1;
                }
            } else {
                if (target >= nums[mid] && target <= nums[r]) {
                    l = mid + 1;
                } else {
                    r = mid - 1;
                }
            }
        }
        
        return -1;
    }
};
```

## 34. Find First and Last Position of Element in Sorted Array

```cpp
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        int l = lowerBound(nums, target);
        int r = lowerBound(nums, target + 1);
        if (l == r) {
            return {-1, -1};
        }
        return {l, r - 1};
    }

private:
    int lowerBound(vector<int>& nums, int target)
    {
        int l = 0;
        int r = nums.size();
        while (l < r) {
            int mid = l + (r - l) / 2;
            if (nums[mid] < target) {
                l = mid + 1;
            } else {
                r = mid;
            }
        }
        return l;
    }
};
```

## 300. Longest Increasing Subsequence

```cpp
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        vector<int> res;
        for (int i = 0; i < nums.size(); i++) {
            vector<int>::iterator iter = lower_bound(res.begin(), res.end(), nums[i]);
            if (iter == res.end()) {
                res.push_back(nums[i]);
                continue;
            }
            *iter = nums[i];
        }
        return res.size();
    }
};
```

## jz6 输出旋转数组的最小元素

```cpp
class Solution {
public:
    int minNumberInRotateArray(vector<int> rotateArray) {
        int l = 0;
        int r = rotateArray.size() - 1;
        while (l < r) {
            int mid = l + (r - l) / 2;
            if (rotateArray[mid] < rotateArray[r]) {
                r = mid;
            } else if (rotateArray[mid] > rotateArray[r]) {
                l = l + 1;
            } else {
                r--;
            }
        }
        return rotateArray[l];
    }
};
```

