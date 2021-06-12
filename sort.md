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

## 215. Kth Largest Element in an Array

```cpp
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        k = nums.size() - k;
        int l = 0;
        int r = nums.size() - 1;
        while (l < r) {
            int pivot = partition(nums, l, r);
            if (pivot == k) {
                return nums[k];
            } else if (pivot > k) {
                r = pivot - 1;
            } else {
                l = pivot + 1;
            }
        }
        return nums[l];
    }
private:
    int partition(vector<int>& nums, int l, int r)
    {
        int i = l;
        for (int j = l; j < r; j++) {
            if (nums[j] < nums[r]) {
                swap(nums[i], nums[j]);
                i++;
            }
        }
        swap(nums[i], nums[r]);
        return i;
    }
};
```

## jz13 使得所有的奇数位于数组的前半部分

```cpp
class Solution {
public:
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 
     * @param array int整型vector 
     * @return int整型vector
     */
    vector<int> reOrderArray(vector<int>& array) {
        // write code here
        for (int i = 1; i < array.size(); i++) {
            for (int j = i; j > 0 && array[j] % 2 != 0 && array[j - 1] % 2 == 0; j--) {
                swap(array[j], array[j - 1]);
            }
            
        }
        return array;
    }
};
```

## jz29 找出其中最小的K个数

```cpp
class Solution {
public:
    vector<int> GetLeastNumbers_Solution(vector<int> input, int k) {
        if (k > input.size() || k <= 0) {
            return {};
        }
        int l = 0;
        int r = input.size() - 1;
        int pivot = 0;
        while (l < r) {
            pivot = partition(input, l, r);
            cout << pivot;
            if (pivot == k - 1) {
                break;
            } else if (pivot > k - 1) {
                r = pivot - 1;
            } else {
                l = pivot + 1;
            }
        }
        vector<int> res;
        for (int i = 0; i < k; i++) {
            res.push_back(input[i]);
        }
        return res;
    }
private:
    int partition(vector<int>& input, int l, int r)
    {
        int i = l;
        for (int j = l; j < r; j++) {
            if (input[j] < input[r]) {
                swap(input[i], input[j]);
                i++;
            }
        }
        swap(input[i], input[r]);
        return i;
    }
};
void QuickSort(int A[], int low, int high)
{
    if (low >= high) {
        return;
    }
    int pivotPos = Partition(A, low, high);
    QuickSort(A, low, pivotPos - 1);
    QuickSort(A, pivotPos + 1, high);
}
```

## jz32 打印能拼接出的所有数字中最小的一个

```cpp
class Solution {
public:
    string PrintMinNumber(vector<int> numbers) {
        std::sort(numbers.begin(), numbers.end(), [](const int a, const int b){
            return to_string(a) + to_string(b) < to_string(b) + to_string(a);
        });
        string res;
        for (const auto item : numbers) {
            res += to_string(item);
        }
        
        return res;
    }
};
```

## jz35 求出这个数组中的逆序对的总数P

```cpp
class Solution {
public:
    int InversePairs(vector<int> data) {
        vector<int> copy = data;
        long long res = 0;
        mergeSort(data, copy, 0, data.size() - 1, res);
        return res % 1000000007;
    }
private:
    void mergeSort(vector<int>& data, vector<int>& copy, int l, int r, long long& res)
    {
        if (l == r) {
            return;
        }
        int mid = l + (r - l) / 2;
        mergeSort(copy, data, l, mid, res);
        mergeSort(copy, data, mid + 1, r, res);
        merge(data, copy, l, mid, r, res);
    }
    void merge(vector<int>& data, vector<int>& copy, int l, int mid, int r, long long& res)
    {
        if (l == r) {
            return;
        }
        int i = mid;
        int j = r;
        int p = r;
        while (i >= l && j >= mid + 1) {
            if (copy[i] > copy[j]) {
                res += (j - mid);
                data[p--] = copy[i--];
            } else {
                data[p--] = copy[j--];
            }
        }
        while (i >= l) {
            data[p--] = copy[i--];
        }
        while (j >= mid + 1) {
            data[p--] = copy[j--];
        }
    }
};
```

## 表示数值的字符串

```cpp
class Solution {
public:
    bool isNumber(string s) {
        static vector<unordered_map<string, int>> states = {
            {},                                                    // state 0
            {{"blank", 1}, {"sign", 2}, {"digit", 3}, {"dot", 4}}, // state 1
            {{"digit", 3}, {"dot", 4}},                            // state 2
            {{"digit", 3}, {"dot", 5}, {"e", 6}, {"blank", 9}},    // state 3, final
            {{"digit", 5}},                                        // state 4
            {{"digit", 5}, {"e", 6}, {"blank", 9}},                // state 5, final
            {{"sign", 7}, {"digit",8}},                            // state 6
            {{"digit", 8}},                                        // state 7
            {{"digit", 8}, {"blank", 9}},                          // state 8, final
            {{"blank", 9}}                                         // state 9, final
        };
        int currState = 1;
        string transition;

        for(auto c : s) {
            if(c>='0' && c<='9') transition = "digit";
            else if(c=='-' || c=='+') transition = "sign";
            else if(c == ' ') transition = "blank";
            else if(c == '.') transition = "dot";
            else if(c == 'e') transition = "e";
            else return false;

            auto it = states[currState].find(transition);
            if  (it == states[currState].end()) 
                return false;
            else
                currState = it->second;
        }
        if  (currState == 3 || currState == 5 || currState == 8 || currState == 9)
            return true;
        else
            return false;
    }
};
```



