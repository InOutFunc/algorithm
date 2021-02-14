##  2. Add Two Numbers

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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* dummy = new ListNode(-1);
        ListNode* cur = dummy;
        int carry = 0;
        while (l1 != nullptr || l2 != nullptr) {
            int val1 = (l1 == nullptr ? 0 : l1->val);
            int val2 = (l2 == nullptr ? 0 : l2->val);
            int sum = val1 + val2 + carry;
            cur->next = new ListNode(sum % 10);
            
            carry = sum / 10;
            cur = cur->next;
            l1 = (l1 == nullptr ? nullptr : l1->next);
            l2 = (l2 == nullptr ? nullptr : l2->next);
        }
        if (carry == 1) {
            cur->next = new ListNode(1);
        }
        return dummy->next;
    }
};
```

