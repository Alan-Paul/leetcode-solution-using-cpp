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
[524-匹配字典最长单词](https://leetcode-cn.com/problems/longest-word-in-dictionary-through-deleting/)
```
class Solution {
public:
    string findLongestWord(string s, vector<string>& d) {
        string ret = "";
        for (int index = 0; index < d.size(); index++) {
            int i, j;
            if (d[index].length() < ret.length() ||(d[index].length() == ret.length() && d[index] > ret)) {
                continue;
            }
            for (i = 0, j = 0; i < s.length() && j < d[index].length(); i++) {
                if (s[i] == d[index][j]) {
                    j++;
                }
            }
            if (j == d[index].length()) {
                if (j > ret.length() || (j == ret.length() && d[index] < ret)) {
                    ret = d[index];
                }
            }
        }
        return ret;
    }
};
```

[215-第K个最大的元素](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)
```
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        priority_queue<int> max_heap;
        if (nums.empty() || nums.size() < k) {
            return -1;
        }
        k = nums.size() - k + 1;
        for (int i = 0; i < k; i++) {
            max_heap.push(nums[i]);
        }
        for (int i = k; i < nums.size(); i++) {
            if (max_heap.top() > nums[i]) {
                max_heap.pop();
                max_heap.push(nums[i]);
            }
        }
        return max_heap.top();
    }
};
```
[347-出现频率最高的K个元素](https://leetcode-cn.com/problems/top-k-frequent-elements/)
```
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        vector<int> ret;
        if (nums.empty() || nums.size() < k) {
            return ret;
        }
        int n = nums.size();
        map<int,int> frequency;
        for (int i=0; i < n; i++) {
            if (frequency.find(nums[i]) == frequency.end()) {
                frequency[nums[i]] = 1;
            
            } else{
                frequency[nums[i]] = frequency[nums[i]] + 1;
            }
        }
        vector<vector<int>> buckets(n+1);
        
        for (map<int, int>::iterator i=frequency.begin(); i!=frequency.end();) {
            int key = i->first;
            int frequency = i->second;
            buckets[frequency].push_back(key);
            i++;
        } 
        int i = 0;
        int j = buckets.size();
        while(i < k) {
            while(buckets[--j].size()==0);
            for (int h = 0; h < buckets[j].size(); h++) {
                if (i == k) {
                    break;
                }
                ret.push_back(buckets[j][h]);
                i++;
            }
        }
        return ret;
    }
};
```



