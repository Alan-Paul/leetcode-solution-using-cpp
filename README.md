##leetcode solutions in cpp
借鉴了[cs-notes](https://github.com/CyC2018/CS-Notes/blob/master/notes/Leetcode%20%E9%A2%98%E8%A7%A3%20-%20%E7%9B%AE%E5%BD%95.md)中的顺序

[167-两数之和](https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/submissions/)
                
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
    
    
[633-平方数之和](https://leetcode-cn.com/problems/sum-of-square-numbers/submissions/)

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


[345-反转字符串中的元音字母](https://leetcode-cn.com/problems/reverse-vowels-of-a-string/submissions/)

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
    
[680-验证回文串](https://leetcode-cn.com/problems/valid-palindrome-ii/submissions/)

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
