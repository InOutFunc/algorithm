## 148. Sort List

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
    ListNode* sortList(ListNode* head) {
        if (head == nullptr || head->next == nullptr) {
            return head;
        }
        ListNode* slow = head;
        ListNode* fast = head;
        while (fast != nullptr && fast->next != nullptr && fast->next->next != nullptr) {
            slow = slow->next;
            fast = fast->next->next;
        }
        ListNode* p2 = slow->next;
        slow->next= nullptr;
        ListNode* l = sortList(head);
        ListNode* r = sortList(p2);
        return merge(l, r);
    }
    
private:
    ListNode* merge(ListNode* p1, ListNode* p2)
    {
        if (p1 == nullptr) {
            return p2;
        }
        if (p2 == nullptr) {
            return p1;
        }
        if (p1->val < p2->val) {
            p1->next = merge(p1->next, p2);
            return p1;
        }
        p2->next = merge(p1, p2->next);
        return p2;
    }
};
```

