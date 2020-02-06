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
[451-根据字符出现顺序排序](https://leetcode-cn.com/problems/sort-characters-by-frequency)
```
class Solution {
public:
    string frequencySort(string s) {
        int len = s.length();
        if (len <= 0) {
            return s;
        }
        string ret;
        map<char,int> frequency;
        for (int i = 0; i < len; i++) {
            char c = s.at(i);
            if (frequency.find(c) == frequency.end()) {
                frequency[c] = 1;
            } else {
                frequency[c] += 1;
            }
        }
        vector<vector<char>> buckets(len+1);
        for(std::map<char, int> :: iterator it = frequency.begin(); it != frequency.end();) {
            char c = it->first;
            int cur_frequency = it->second;
            buckets[cur_frequency].push_back(c);
            it++;
        }
        for(int i = len; i > -1; i--) {
            if (!buckets[i].empty()) {
                for (auto c : buckets[i]) {
                    for (int j = 0; j < i; j++) {
                        ret.push_back(c);
                    }
                }
            }
        }
        return ret;
    }
};
```
[75-颜色排序，荷兰国旗问题](https://leetcode-cn.com/problems/sort-colors/submissions/)
```
class Solution {
public:
    void sortColors(vector<int>& nums) {
        vector<int> frequency(3);
        for (int i = 0; i < nums.size(); i++) {
            frequency[nums[i]] ++;
        }
        int idx = 0;
        for (int i = 0; i < frequency.size(); i++) {
            for (int j = 0; j < frequency[i]; j++) {
                nums[idx++] = i;
            }
        }
    }
};

// 第二种解法
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int zeros = -1;
        int one = 0;
        int two = nums.size();
        while (one < two) {
            if (nums[one] == 0) {
                swap(nums, ++zeros, one++);
            
            } else if (nums[one] == 2) {
                swap(nums, --two, one);
            
            } else {
                one++;
            }
        }
    }
    void swap(vector<int>& nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
};
```
[70-爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/submissions/)
```
class Solution {
public:
    int climbStairs(int n) {
        //
        if (n <= 2) {
            return n;
        }
        vector<int> dp(n+1);
        dp[0] = 0;
        dp[1] = 1;
        dp[2] = 2;
        for (int i = 3; i < dp.size(); i++) {
            dp[i] = dp[i-1] + dp[i-2];
        }
        return dp[n];
    }
};
```
[198-强盗抢劫](https://leetcode-cn.com/problems/house-robber/submissions/)
```
class Solution {
public:
    int rob(vector<int>& nums) {
        // dp[i] : 在第i号房屋可以偷到的最高金额； 状态转移：dp[i] = max(dp[i-2]+nums[i], dp[i-1])
        // 初始状态： dp[0] = nums[0]; dp[1] = max(dp[0], nums[1])
        if (nums.size() <= 0) {
            return 0;
        
        } else if (nums.size() == 1) {
            return nums[0];

        } else if (nums.size() == 2) {
            return max(nums[0], nums[1]);
        
        } else {
            vector<int> dp(nums.size());
            dp[0] = nums[0];
            dp[1] = max(nums[0], nums[1]);
            for (int i = 2; i < dp.size(); i++) {
                dp[i] = max(dp[i-2]+nums[i], dp[i-1]);
            }
            int n = dp.size();
            return max(dp[n-1], dp[n-2]);
        }
    }
    int max(int a, int b) {
        return (a > b) ? a : b;
    }
};



// 解法2：
class Solution {
public:
    int rob(vector<int>& nums) {
        if (nums.size() <= 0) {
            return 0;
        
        } else if (nums.size() == 1) {
            return nums[0];
        
        } else if (nums.size() == 2) {
            return max(nums[0], nums[1]);
        
        } else {
            int pre2 = nums[0];
            int pre1 = max(nums[0], nums[1]);
            for (int i = 2; i < nums.size(); i++) {
                int cur = max(pre2 + nums[i], pre1);
                pre2 = pre1;
                pre1 = cur;
            }
            return pre1;
        }
    }
    int max(int i, int j) {
        return (i > j) ? i : j;
    }
};
```
[213-打家劫舍](https://leetcode-cn.com/problems/house-robber-ii/submissions/)
```
class Solution {
public:
    int rob(vector<int>& nums) {
        if (nums.size() == 0) {
            return 0;
        
        } else if (nums.size() == 1) {
            return nums[0];
        
        } else if (nums.size() == 2) {
            return max(nums[0], nums[1]);
        
        } else {
            int n = nums.size();
            return max(rob(nums, 0, n - 1), rob(nums, 1, n));
        }
    }
    int rob(vector<int>& nums, int begin, int end) {
        int pre1 = 0;
        int pre2 = 0;
        for (int i = begin; i < end; i++)  {
            int cur = max(pre2 + nums[i], pre1);
            pre2 = pre1;
            pre1 = cur;
        }
        return pre1;
    }
    int max(int i, int j) {
        return (i > j) ? i : j;
    }
};
```
[1143-最长公共子序列](https://leetcode-cn.com/problems/longest-common-subsequence/submissions/)
```
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        //状态 ： dp[i][j], 表示 text1 第 i 位与 text2 第 j 位的公共子序列长度;
        // 状态转移 ：若 text1[i] == text2[j]， 则 dp[i][j] = dp[i-1][j-1] + 1 ; 否则， dp[i][j] = max(dp[i][j-1], dp[i-1][j])
        // 使用到 dp[i-1][j-1], dp[i-1][j], dp[i][j-1] 等左上，上，左三个过往值，用一个值存储 dp[i-1][j-1]，即可
        int n = text1.size();
        int m = text2.size();
        if (n == 0 || m == 0) {
            return 0;
        }
/*
        vector<vector <int>> dp(n + 1, vector<int>(m + 1, 0));
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                if (text1[i-1] == text2[j-1]) {
                    dp[i][j] = dp[i-1][j-1] + 1;
                }
                else{
                    dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
                }
            }
        }
        return dp[n][m];
*/
        vector<int> dp(m+1, 0);
        int last, temp; // last ： 存储 dp[i-1][j-1]; temp : 暂时存储 
        for (int i = 1; i <= n; i++, last=0) {
            for (int j = 1; j <= m; j++) {
                temp = dp[j]; // 存储当前 dp[i][j], 因为即将修改 dp[i][j]， 而下一次循环dp[i][j+1]时，要用到当前的 dp[i][j]
                if (text1[i-1] == text2[j-1]) {
                    dp[j] = last + 1;
                }
                else{
                    dp[j] = max(dp[j], dp[j-1]);
                }
                last = temp;
            }
        }
        return dp[m];
    }
    int max(int a, int b){
        return a > b ? a : b;
    }
};
```
[416-分割等和子集](https://leetcode-cn.com/problems/partition-equal-subset-sum/submissions/)
```
class Solution {
public:
    bool canPartition(vector<int>& nums) {
        // 状态：dp[i][j]， 表示前i个数中， 是否有和恰好为j的子集；
        /*
        状态转移： 
        1. 不取第 i 个数： dp[i][j] = dp[i-1][j]; 当前 i - 1个数已有和为 j 的子集时，
        2. 取第 i 个数： dp[i][j] = dp[i-1][j-nums[i]]; 当前 i-1 个数已有和为 j - nums[i] 的子集时，加上nums[i]即可得到和为 j 的子集；
        3. 特殊情况，可置于初始化状态中，  j == nums[i]； 若 j == nums[i] ， 表示nums[i]自身构成一个和为 j 的子集；若置于初始化状态中，则表示 dp[i][0] = true; 因为 j-nums[i] = 0;        
        */
        // 看作体积为 sum/2 的 0-1背包问题，这里每个体积的背包要恰好装满，所以每个背包的初始状态应设为无穷，保证每个背包的状态都是由其初始状态转换而来，详见《背包九讲》第6页。先行判断，总和是否为2的倍数，否则不能分割。 
        int sum = computeSum(nums);
        if (sum % 2 != 0) {
            return false;
        }
        sum /= 2;
        int n = nums.size() + 1;
        int m = sum + 1;


        /*  二维数组解法
        vector<vector<bool>> dp(n, vector<bool>(m, false));
        for (int i = 1; i < n; i++) {
            for (int j = 1; j < m; j++) {
                dp[i][j] = dp[i-1][j];
                if (j == nums[i-1]) {
                    dp[i][j] = true;
                    //continue;
                } else if (j > nums[i-1]) {// j 小于 nums[i-1]，肯定不取nums[i-1]。 这里的nums[i-1]就是第 i 个数，因为循环中的 i 从1开始到nums.size(); 而 nums数组下标从0开始；
                dp[i][j] = dp[i-1][j] || dp[i-1][j - nums[i-1]]; // j 大于 nums[i-1], 则可取可不取 nums[i-1]  
                } 
            }
        }
        return dp[n-1][m-1];
        */
        
        
        /*
        一维数组解法：从二维数组中可看到，第 i 行只与第 i-1 行的值相关，可用m列一维数组存储并更新,但是要注意的是，状态转移变为：
        1. 不取第i个数： dp[j] = dp[j]
        2. j == nums[i] : dp[0] = true
        3. 取第 i 个数： dp[j] = dp[j-nums[i]]
         状态转移中， dp[i][j] = dp[i-1][j-nums[i]] || dp[i-1][j]; 而 j-nums[i] 比 j 小，若从前往后更新，则会先更新 dp[i][j-nums[i]]，此时已经丢失了 dp[i-1][j-nums[i]] 的信息 
        */
        vector<bool> dp(m, false);
        dp[0] = true; // dp[i][0] 表示了两种含义， 一种是 j == num; 一种是 容积为 0; 
        for (int i = 0; i < n-1; i++) {
            for (int j = m; j >= nums[i]; j--) {
                dp[j] = dp[j] || dp[j-nums[i]];
            }
        }
        return dp[m-1];
    }
    int computeSum(vector<int>& nums){
        int sum = 0;
        for (auto num : nums){
            sum += num;
        }
        return sum;
    }
};
```
[494-目标和](https://leetcode-cn.com/problems/target-sum/submissions/)
```
class Solution {
public:
    int findTargetSumWays(vector<int>& nums, int S) {
        /* 
        设所有元素和为 M , 正元素和为 P, 负元素和为 N;
        则有： P + N = S; P - N = M; ==> 2P = S + M ==> P = (S+M)/2
        则问题等价为求 nums 中和为 P 的子集数，一共有多少个子集的和为 P 
        */
        int sum = computeSum(nums);
        if (sum < S) {
            return 0;
        }
        sum = sum + S;
        if (sum % 2 != 0) {
            return 0;
        }
        sum /= 2;

        /* 枚举，对每个 num， 计算 +num, -num 的个数
        return dfs(nums, 0, 0, 0, S);
        */

        /*
        状态 ： dp[i][j] : 前 i 个数中， 和为 j 的子集个数
        状态转移： 
        1. nums[i] 不取： dp[i][j] = dp[i-1][j]
        2. nums[i] 取：   dp[i][j] = dp[i-1][j] + dp[i-1][j-nums[i]]
        
        vector<int> dp(sum+1, 0);
        dp[0] = 1; // 初始状态，容积为0时，子集为0，是为一种取法
        for (auto num : nums){
            for (int j = sum; j >= num; j--) {
                dp[j] = dp[j] + dp[j - num];
            }
        }
        return dp[sum];
        */
    }
    int computeSum(vector<int>& nums){
        int sum = 0;
        for (auto num : nums){
            sum += num;
        }
        return sum;
    }
    int dfs(vector<int>& nums, int i, int sum, int count, int target) {
        if (i == nums.size()) {
            if (sum == target) {
                return ++count;
            }
            return count;
        }
        else {
            return dfs(nums, i+1, sum + nums[i], count, target) + dfs(nums, i+1, sum - nums[i], count, target);
        }
    }
};
```
[474-一和零](https://leetcode-cn.com/problems/ones-and-zeroes/submissions/)
```
class Solution {
public:
    int findMaxForm(vector<string>& strs, int m, int n) {
        // 2维的 0-1背包问题，有两个限制： m, n; 每个物品的价值均为 1 
        // 状态 ： dp[i][j] : 最多使用 i 个 0 和 j 个 1 的情况下，
        //        可以拼出的最大最多字符串个数
        // 状态转移： dp[i][j] = max(dp[i-1][j-1], dp[i-zero(str)][j-one(str)] + 1)
        //           不取当前字符串 str  ： dp[i-1][j-1]
        //           取当前字符串 str    :  dp[i - zero(str)][j - one(str)] + 1
        if (strs.size() == 0) {
            return 0;
        }   
        vector<vector<int>> dp(m+1, vector<int>(n+1, 0));
        // 困扰多年的初始化问题， 这里并不需要保证 m 跟 n 恰好用完，所以dp[0-m][0-n]都初始化为 dp[0][0] 的状态，即 0
        for (auto str : strs) {
            int zeros = 0;
            int ones = 0;
            for (int k = 0; k < str.length(); k++) {
                if (str[k] == '0') {
                    zeros++;
                }
                else if (str[k] == '1') {
                    ones++;
                }
            }

            for (int i = m; i >= zeros; i--) {
                for (int j = n; j >= ones; j--) {
                    dp[i][j] = max(dp[i][j], dp[i - zeros][j - ones] + 1);
                }
            }
        }
        return dp[m][n];
    }
    int max(int a, int b) {
        return a > b ? a : b;
    }
};
```
[322-零钱兑换](https://leetcode-cn.com/problems/coin-change/)
```
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        //背包问题，这里是完全背包，每个硬币可选无数次，注意的是要取的最小次数
        // 初始化有所不同，dp[0][0]=0 表示需要 0 枚硬币， 但 j == nums[i] 时，需要1枚硬币；所以要将 j == nums[i] 与 dp[0][0] 分别计算
        // amount 是体积， coins 是物品， 物品代价是 硬币面额， 价值是 1 （个数）， 
        // 这里要注意的是取价值最小而非价值最大
        if (coins.size() == 0) {
            return -1;
        }
        if (amount == 0) { // amount 为0时，输出为0，我也不懂
            return 0;
        }
        vector<int> dp(amount + 1, -1);
        dp[0] = 1;
        for (auto coin : coins) {
            for (int j = coin; j <= amount; j++) {
                if (j == coin) {
                    dp[j] = 1;
                }
                else if (dp[j-coin] != -1) {// dp[j-coin] 已更新，表明有硬币组合能够拼成 j-coin的总金额，那么加上当前的coin，一定可以拼成 j 的总金额
                    if (dp[j] == -1) {
                        dp[j] = dp[j-coin] + 1; //当前dp[j] 尚未从初始值 -1 开始更新
                    }
                    else {// d[j] != -1, 表示 dp[j] 已经包含了某种组合，这时才能取最小的组合
                        dp[j] = min(dp[j], dp[j-coin] + 1)                        ;
                    }
                    
                }
            }
        }
        return dp[amount];
    }
    int min(int a, int b) {
        return a < b ? a : b;
    }
};
```
[518-零钱兑换II](https://leetcode-cn.com/problems/coin-change-2/submissions/)
```
class Solution {
public:
    int change(int amount, vector<int>& coins) {
        if (amount == 0) {
            return 1;
        }
        if (coins.size() == 0) {
            return 0;
        }
        vector<int> dp(amount+1, 0);
        dp[0] = 1;
        for (auto coin : coins){
            for (int j = coin; j <= amount; j++) {
                dp[j] = dp[j] + dp[j-coin]; // 取或不取的总组合数
            }
        }
        return dp[amount];
    }
    int max(int a, int b) {
        return a > b ? a : b;
    }
};
```


