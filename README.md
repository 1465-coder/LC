# 从头更新吧，之前单纯的复制题目感觉没有作用，对题目还是应该多思考一些
二分法
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        }
        else if (l2 == null) {
            return l1;
        }
        else if (l1.val < l2.val) {
            l1.next = mergeTwoLists(l1.next, l2);
            return l1;
        }
        else {
            l2.next = mergeTwoLists(l1, l2.next);
            return l2;
        }

    }
# 
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
# 
