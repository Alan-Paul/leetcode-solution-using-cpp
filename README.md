**leetcode solutions in cpp**

借鉴了[cs-notes](https://github.com/CyC2018/CS-Notes/blob/master/notes/Leetcode%20%E9%A2%98%E8%A7%A3%20-%20%E7%9B%AE%E5%BD%95.md)中的顺序

[167-两数之和](https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/submissions/)

```
    class Solution {
    public:
        vector<int> twoSum(vector<int>& numbers, int target) {
            int begin = 0;
            int last = numbers.size() - 1;
            while (begin < last) {
                int sum = numbers[begin] + numbers[last];
                if (sum == target) {
                    int res[] = {begin+1, last+1};
                    return vector<int>(res, res+2);
                    // return {begin+1, last+1};
                } else if (sum > target) {
                    last--;    
                } else {
                    begin++;
                }            
            }
            return vector<int>(2, -1);
        }
    };
```
    
    
[633-平方数之和](https://leetcode-cn.com/problems/sum-of-square-numbers/submissions/)
```
    class Solution {
    public:
        bool judgeSquareSum(int c) {
            int low = 0;
            int high = (int)sqrt((double)c);
            while(low <= high) {
                long sum = (long)pow(low, 2) + (long)pow(high, 2);
                if (sum == c) {
                    return true;
                } else if (sum > c) {
                    high--;
                } else {
                    low++;
                }
            }
            return false;
        }
    };
```

[345-反转字符串中的元音字母](https://leetcode-cn.com/problems/reverse-vowels-of-a-string/submissions/)
```
    class Solution {
    public:
        string reverseVowels(string s) {
            string letter = "AEIOUaeiou";
            int low = 0;
            int high = s.length() - 1;
            while (low < high) {
                if (letter.find(s[low]) == letter.npos){
                    low++;
                } else if (letter.find(s[high]) == letter.npos) {
                    high--;
                } else {
                    swap(s[low], s[high]);
                    low++;
                    high--;
                }
            }
            return s;
        }
    };
```    
[680-验证回文串](https://leetcode-cn.com/problems/valid-palindrome-ii/submissions/)
```
    class Solution {
    public:
        bool validPalindrome(string s) {
            int low = 0;
            int high = s.length() - 1;
            while (low < high) {
                if (s[low] != s[high]) {
                    return isPalindrome(s, low+1, high) || isPalindrome(s, low, high - 1);
                } else {
                    low++;
                    high--;
                }            
            }
            return true;
        };

        bool isPalindrome(string s, int low, int high) {
            while (low < high) {
                if (s[low++] != s[high--]) {
                    return false;
                }
            }
            return true;
        }
    };
```
[88-合并两个有序数组](https://leetcode-cn.com/problems/merge-sorted-array/submissions/)
```
    class Solution {
    public:
        void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
            int index1 = m - 1;
            int index2 = n - 1;
            int indexMerge = m + n - 1;
            while (index1 >=0 || index2 >=0) {
                if (index2 < 0) {
                    return;
                } else if (index1 < 0) {
                    nums1[indexMerge--] = nums2[index2--];
                } else {
                    nums1[indexMerge--] = nums1[index1] > nums2[index2] ? nums1[index1--] : nums2[index2--];
                }
            }        
        }
    };
```

[141-环形链表](https://leetcode-cn.com/problems/linked-list-cycle/submissions/)
```
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
        if (head == nullptr)  {
            return false;
        }
        ListNode* pre = head;
        ListNode* cur = head->next;
        while (pre != nullptr && cur != nullptr && cur->next != nullptr) {
            if (pre == cur) {
                return true;
            }
            pre = pre->next;
            cur = cur->next->next;
        }
        return false;
    }
};
```
