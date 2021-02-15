## 11. Container With Most Water

```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int l = 0;
        int r = height.size() - 1;
        int ret = 0;
        
        while (l < r) {
            ret = std::max(ret, (r - l) * std::min(height[r], height[l]));
            
            if (height[l] < height[r]) {
                l++;
            } else {
                r--;
            }
        }
        
        return ret;
    }
};
```

## 15. 3Sum

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        if (nums.size() < 3) {
            return {};
        }
        sort(nums.begin(), nums.end());
        vector<vector<int>> res;
        for (int i = 0; i < nums.size() - 2; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            int l = i + 1;
            int r = nums.size() - 1;
            while (l < r) {
                if (nums[i] + nums[l] + nums[r] == 0) {
                    res.push_back({nums[i], nums[l], nums[r]});
                    while (l < r && nums[l] == nums[l + 1]) {
                        l++;
                    }
                    while (l < r && nums[r] == nums[r - 1]) {
                        r--;
                    }
                    l++;
                    r--;
                } else if (nums[i] + nums[l] + nums[r] > 0) {
                    r--;
                } else {
                    l++;
                }
            }
        }
        
        return res;
    }
};
```

## 19. Remove Nth Node From End of List

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* dummy = new ListNode(-1);
        dummy->next = head;
        ListNode* fast = dummy;
        while (n > 0) {
            fast = fast->next;
            n--;
        }
        ListNode* slow = dummy;
        while (fast != nullptr && fast->next != nullptr) {
            fast = fast->next;
            slow = slow->next;
        }
        
        slow->next = slow->next->next;
        return dummy->next;
    }
};
```

## 42. Trapping Rain Water

```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int l = 0;
        int r = height.size() - 1;
        int minL = 0;
        int minR = 0;
        int res = 0;
        while (l <= r) {
            if (height[l] < height[r]) {
                if (minL > height[l]) {
                    res += (minL - height[l]);
                }
                minL = max(minL, height[l]);
                l++;
            } else {
                if (minR > height[r]) {
                    res += (minR - height[r]);
                }
                minR = max(minR, height[r]);
                r--;
            }
        }
        return res;
    }
};
```

