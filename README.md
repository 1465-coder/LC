```
#2020.5.9
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
```
#2020.5.10
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
```
#2020.5.11
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
