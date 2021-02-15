## 23. Merge k Sorted Lists

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
struct cmp {
    bool operator()(ListNode* p1, ListNode* p2)
    {
        return p1->val > p2->val;
    }
};

class Solution {
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        priority_queue<ListNode*, vector<ListNode*>, cmp> pq;
        for (auto item : lists) {
            if (item != nullptr) {
                pq.push(item);  
            }

        }
        
        ListNode* dummy = new ListNode(-1);
        ListNode* cur = dummy;
        while (!pq.empty()) {
            cur->next = pq.top();
            ListNode* tmp = pq.top();
            pq.pop();
            if (tmp->next != nullptr) {
                pq.push(tmp->next);
            }
            cur = cur->next;
        }
        
        return dummy->next;
    }
};
```

