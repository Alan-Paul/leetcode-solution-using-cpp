##leetcode solutions in cpp
借鉴了[cs-notes](https://github.com/CyC2018/CS-Notes/blob/master/notes/Leetcode%20%E9%A2%98%E8%A7%A3%20-%20%E7%9B%AE%E5%BD%95.md)中的顺序
[两数之和](https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/submissions/)
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
