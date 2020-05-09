从头更新吧，之前单纯的复制题目感觉没有作用，对题目还是应该多思考一些

2020/4/25
46. 全排列
给定一个 没有重复 数字的序列，返回其所有可能的全排列。 示例:

输入: [1,2,3]
输出:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
此题应用回溯 算法求解，对其进行深度优先遍历。对于回溯算法应该弄明白三点：

怎么前进（进入下一状态）

怎么回退（回到上一个状态）

什么时候停止

其中比较重要的是：采取何种方式处理好状态的前进和回退。在本题中，在前进时，需要查看当前数字是否已经在组合的路径中，也就是要回避非法状态；在回退时，要将当前数字从组合的路径中删除，以达到回溯、不影响进入到下一个状态的目的。

Java 里面都是值传递，对于列表对象来说，复制的是 path 这个变量的地址，所以是值传递。也就是说add的时候确实是满着的，不过递归结束就变空了，整个过程都用的一份path。

2020/4/26
23.合并K个排序链表
合并 k 个排序链表，返回合并后的排序链表。请分析和描述算法的复杂度。 示例:

输入:
[
  1->4->5,
  1->3->4,
  2->6
]
输出: 1->1->2->3->4->4->5->6
此题采用分治算法 类似于归并排序 将合并整个链表数组 变为合成两个链表数组 再一直划分知道变为合成两个链表

合成两个链表方法：

1. 每次改变的就是每个的next只需将每个时刻最小的作为头结点再依次串起来就可以。采用递归

list1[0]+merge(list1[1:],list2)  list1[0]<list2[0]

list2[0]+merge(list1,list2[1:])  otherwise
时间复杂度：O(n+m)。 因为每次调用递归都会去掉 l1 或者 l2 的头元素（直到至少有一个链表为空），函数 mergeTwoList 中只会遍历每个元素一次。所以，时间复杂度与合并后的链表长度为线性关系。

空间复杂度：O(n+m)。调用 mergeTwoLists 退出时 l1 和 l2 中每个元素都一定已经被遍历过了，所以 n+m个栈帧会消耗 O(n+m)的空间

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
