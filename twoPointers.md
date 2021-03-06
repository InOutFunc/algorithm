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

## 141. Linked List Cycle

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    bool hasCycle(ListNode *head) {
        if (head == nullptr || head->next == nullptr) {
            return false;
        }
        ListNode* fast = head;
        ListNode* slow = head;
        while (fast != nullptr && fast->next != nullptr) {
            fast = fast->next->next;
            slow = slow->next;
            if (fast == slow) {
                return true;
            }
        }
        
        return false;
    }
};
```

## 142. Linked List Cycle II

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode* slow = head;
        ListNode* fast = head;
        while (fast != nullptr && fast->next != nullptr) {
            slow = slow->next;
            fast = fast->next->next;
            if (fast == slow) {
                break;
            }
        }
        if (fast == nullptr || fast->next == nullptr) {
            return nullptr;
        }
        fast = head;
        while (fast != slow) {
            fast = fast->next;
            slow = slow->next;
        }
        return slow;
    }
};
```

## 287. Find the Duplicate Number

```cpp
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int slow = nums[0];
        int fast = nums[0];
        while (fast < nums.size() && nums[fast] < nums.size()) {
            slow = nums[slow];
            fast = nums[nums[fast]];
            if (slow == fast) {
                break;
            }
        }
        if (fast == nums.size() || nums[fast] == nums.size()) {
            return -1;
        }
        fast = nums[0];
        while (fast != slow) {
            fast = nums[fast];
            slow = nums[slow];
        }
        return slow;
    }
};
```

## jz14 输出该链表中倒数第k个结点

```cpp
/**
 * struct ListNode {
 *	int val;
 *	struct ListNode *next;
 *	ListNode(int x) : val(x), next(nullptr) {}
 * };
 */
class Solution {
public:
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 
     * @param pHead ListNode类 
     * @param k int整型 
     * @return ListNode类
     */
    ListNode* FindKthToTail(ListNode* pHead, int k) {
        // write code here
        ListNode* slow = pHead;
        ListNode* fast = pHead;
        while (k > 0) {
            if (fast == nullptr) {
                return nullptr;
            }
            fast = fast->next;
            k--;
        }
        while (fast != nullptr) {
            slow = slow->next;
            fast = fast->next;
        }
        return slow;
    }
};
```

