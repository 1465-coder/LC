# 2020.5.8
```
两数之和的暴力法
给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。
你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。
示例:
给定 nums = [2, 7, 11, 15], target = 9
因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
暴力法具体代码如下：
```
```
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) { 
        int i=0,j=0,a,b;
        for(i=0;i<nums.size()-1;i++)
        for(j=i+1;j<nums.size();j++)
        if(target-nums[j]==nums[i])
            {a=i;
             b=j;}
    return {a,b};
        
    }
};
```
# 2020.5.9
```
#二分法：由于 xx 平方根的整数部分 \textit{ans}ans 是满足 k^2≤x 的最大 k值，因此我们可以对 k进行二分查找，从而得到答案。
二分查找的下界可设为1，上界可以粗略地设定为x。在二分查找的每一步中，我们只需要比较中间元素mid 的平方与 x 的大小关系，并通过比较的结果调整上下界的范围。由于我们所有的运算都是整数运算，不会存在误差，因此在得到最终的答ans 后，也就不需要再去尝试ans+1了。
具体代码如下：
```
```
class Solution {
public:
    int mySqrt(int x) {
        long l = 1;
        long r = x;
        if (x == 0) return 0;
        if (x == 1) return 1;
        while(l<r) {
            int mid = (l+r)/2;
            if (x/mid == mid) {
                return mid;
            } else if (x/mid > mid) {
                l = mid+1;
            } else {
                r = mid;
            }
        }
        return l-1;
    }
};
```
# 2020.5.10
```
#给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。
百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”
例如，给定如下二叉树:  root = [3,5,1,6,2,0,8,null,null,7,4]
示例 1:
输入: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
输出: 3
解释: 节点 5 和节点 1 的最近公共祖先是节点 3。
示例 2:
输入: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
输出: 5
解释: 节点 5 和节点 4 的最近公共祖先是节点 5。因为根据定义最近公共祖先节点可以为节点本身。
说明:
所有节点的值都是唯一的。
p、q 为不同节点且均存在于给定的二叉树中。具体代码如下：
```
```
class Solution {
public:
    unordered_map<int, TreeNode*> fa;
    unordered_map<int, bool> vis;
    void dfs(TreeNode* root){
        if (root->left != nullptr) {
            fa[root->left->val] = root;
            dfs(root->left);
        }
        if (root->right != nullptr) {
            fa[root->right->val] = root;
            dfs(root->right);
        }
    }
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        fa[root->val] = nullptr;
        dfs(root);
        while (p != nullptr) {
            vis[p->val] = true;
            p = fa[p->val];
        }
        while (q != nullptr) {
            if (vis[q->val]) return q;
            q = fa[q->val];
        }
        return nullptr;
    }
};
```
# 2020.5.11
```
#实现 pow(x, n) ，即计算 x 的 n 次幂函数。
#迭代法#
我们可以分三种情况来讨论
(1)当n等于零，返回1
(2)当n大于零，且为奇数时，表达为a^(n-1)*n；为偶数时，表示为a^n/2*a^n/2
(3)当n小于零时，表达为1/(a^(-n))
以此方式迭代即可，具体代码如下：
```
```
class Solution {
public:
    double quickMul(double x, long long N)
    {
         if (N < 0) return quickMul(1/x, -N);
        if (N==0) return 1.0;
        else if (N%2==1) return quickMul(x, N- 1) * x;
        else 
        {
            double tmp = quickMul(x, N/2);
            return tmp * tmp; 
        }
    }
    double myPow(double x, int n) 
    {
          return quickMul(x, n);
    }
};
```
# 2020.5.14
## 数组中出现一次的数
异或运算有以下三个性质:
(1) 任何数和 0 做异或运算，结果仍然是原来的数；
(2) 任何数和其自身做异或运算，结果是 0；
(3) 异或运算满足交换律和结合律。
假设数组中有 2m+1 个数，其中有 m个数各出现两次，一个数出现一次。根据异或性质可得，数组中的全部元素的异或运算结果总是为那个出现一次的数目。故可通过异或进行求解。
（1）
```
class Solution {
public:
    int singleNumber(vector<int>& nums) {
      int ret=0,i;
        for(i=0;i<size(nums);i++)
       { 
           ret^=nums[i];
       }
       return ret;
    }
};
```
（2）
```
class Solution {
public:
    int singleNumber(vector<int>& nums) {
      int ret=0;
        for(auto e:nums)
        ret^=e;
       return ret;
    }
};
```
# 2020.5.15
#### 和为K的子数组
给定一个整数数组和一个整数 k，你需要找到该数组中和为 k 的连续的子数组的个数。
示例 1 :
```
输入:nums = [1,1,1], k = 2
输出: 2 , [1,1] 与 [1,1] 为两种不同的情况。
```
考虑以 i 结尾和为 k的连续子数组个数，我们需要统计符合条件的下标 j的个数，其中 0≤j≤i 且 [j..i]这个子数组的和恰好为 k
我们可以枚举 [0..i]里所有的下标 jj 来判断是否符合条件，具体代码如下：
```
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int step=0,i,j;
        for(i=0;i<size(nums);i++)
        {
        int sum=0;
        for(j=i;j>=0;j--)
        {
            sum+=nums[j];
            if(sum==k)
            step++;
        }
        }
   return step;
    }
};
```
# 2020.5.19
#### 验证回文字符串
给定一个非空字符串 s，最多删除一个字符。判断是否能成为回文字符串。
```
示例 1:

输入: "aba"
输出: True
示例 2:

输入: "abca"
输出: True
解释: 你可以删除c字符。
```
首先考虑如果不允许删除字符，如何判断一个字符串是否是回文串。常见的做法是使用双指针。定义左右指针，初始时分别指向字符串的第一个字符和最后一个字符，每次判断左右指针指向的字符是否相同，如果不相同，则不是回文串；如果相同，则将左右指针都往中间移动一位，直到左右指针相遇，则字符串是回文串。在允许最多删除一个字符的情况下，同样可以使用双指针，通过贪心算法实现。
具体代码如下：
```
class Solution {
public:
枚举法
    bool checkPalindrome(const string& s, int low, int high) {
        for (int i = low, j = high; i < j; ++i, --j) {
            if (s[i] != s[j]) {
                return false;
            }
        }
        return true;
    }
  贪心算法
    bool validPalindrome(string s) {
        int low = 0, high = s.size() - 1;
        while (low < high) {
            char c1 = s[low], c2 = s[high];
            if (c1 == c2) {
                ++low;
                --high;
            }
            else {
                return checkPalindrome(s, low, high - 1) || checkPalindrome(s, low + 1, high);
            }
        }
        return true;
    }
};
```
