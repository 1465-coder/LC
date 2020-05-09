#2020.5.9
二分法：由于 xx 平方根的整数部分 \textit{ans}ans 是满足 k^2≤x 的最大 k值，因此我们可以对 k进行二分查找，从而得到答案。
二分查找的下界可设为1，上界可以粗略地设定为x。在二分查找的每一步中，我们只需要比较中间元素mid 的平方与 x 的大小关系，并通过比较的结果调整上下界的范围。由于我们所有的运算都是整数运算，不会存在误差，因此在得到最终的答ans 后，也就不需要再去尝试ans+1了。
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

