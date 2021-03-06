# 1、复杂度分析

复杂度总览：https://www.bigocheatsheet.com/

## 1.1、时间复杂度
（参考：https://www.jianshu.com/p/d48c0af8c04f）
**注意：只看最高复杂度的运算**
1. O(1)：Constant Complexity 常数时间复杂度
2. O(log n)：Logarithmic Complexity 对数时间复杂度
3. O(n)：Linear Complexity 线性时间复杂度
4. O(n^2)：N square Complexity 平方
5. O(n^3)：N cubic Complexity 立方
6. O(2^n)：Exponential Growth 指数
7. O(n!)：Factorial 阶乘

### 1.1.1、主定理
有4种方式可以判断递归函数的时间复杂度
1. Binary search（二分搜索算法）：O(logn)
2. Binary tree Traversal（二叉树遍历算法）：O(n)
3. Optimal sorted matrix search（最优有序矩阵查找）：O(n)
4. Merge sort（归并排序算法）：(nlogn) （参考：https://blog.csdn.net/qq_20011607/article/details/82351225）

### 1.1.2、常见算法时间复杂度
1. 二叉树遍历-前序、中序、后序：时间复杂度为O(n)，因为每个节点都被访问一次，且仅访问一次
2. 图的遍历：时间复杂度为O(n)，因为图里的每个节点访问一次，且仅访问一次
3. 图的搜索算法：DFS（深度优先）、BFS（广度优先）的时间复杂度都为O(n)，因为图里的每个节点访问一次，且仅访问一次
4. 二分查找：时间复杂度为O(logn)，主定理得出

## 1.2、空间复杂度
一般有2个原则来判读
1. 数组的长度：数组长度决定空间复杂度，如果开的一维数组那么数组长度为n，则空间复杂度为O(n)，开的二维数组那么数组长度为n^2，则空间复杂度为O(n^2)
2. 递归的深度：递归的深度决定空间复杂度，如果深度为n，则空间复杂度为O(n)

# 2、数据结构
## 2.1、一维
### 2.1.1、基础
数组array(string)，链表Linked List
### 2.1.2、高级
栈stack，队列queue，双端队列deque，集合set，映射map（hash or map），etc
## 2.2、二维
### 2.2.1、基础
树tree，图graph
### 2.2.2、高级
二叉搜索树binary search tree（red-black tree，AVL），堆heap，并查集disjoint set，字典树Trie，etc
## 2.3、特殊
1. 位运算Bitwise，布隆过滤器BloomFilter
2. LRU Cache

# 3、算法
1. if-else,switch --> branch
2. for,while loop --> Iteration
3. 递归Recursion（Divide & Conquer 分治，Backtrace 回溯）
4. 搜索Search：深度优先搜索Depth first search，广度优先搜索Breadth first search，启发式搜索A*，etc
5. 动态规划Dynamic Programming
6. 二分查找Binary Search
7. 贪心Greedy
8. 数学Math，几何Geometry

## 3.1、代码模板
* 分治、回溯、搜索：https://github.com/duwanjiang/AlgorithmQIUZHAO/blob/master/Week_03/README.md
* 递归：
``` java
public void recur(int level, int param){
    //terminator
    if(level > MAX_LEVEL){
        //process result
        return;
    }
    //process current logic
    process(level, param);
    //drill down
    recur(level + 1, newParam);
    //restore current status
}
```
# 4、化繁为简的思想
1. 人肉递归低效、很累
2. 找到最近最简方法，将其拆解成可重复解决的问题
3. 数学归纳法思想

* 本质：寻找重复性 --> 计算机指令集

# 5、学习要点
1. 基本功是区别业余和职业选手的根本。深厚功底来自于 -- 过遍数
2. 最大的误区： 只做一遍
3. 五毒神掌
4. 刻意练习 - 练习缺陷弱点地方、不舒服、枯燥
5. 反馈 - 看题解、看国际版的高票回答

# 6、经典习题
1. 爬楼梯、硬币兑换（可以使用DFS、BFS、数组、动态规划等方法）
2. 括号匹配、括号生成、直方图最大面积、滑动窗口
3. 二叉树遍历、分成输出树、判断二叉搜索树
4. 股票买卖、偷房子、字符串编辑距离、最长上升子序列、最长公共子序列
5. 异位词（判断和归类）、回文串（最大回文串）、regex和通配符匹配
6. 高级数据结构（Trie、BloomFilter、LRU Cache、etc）

# 7、五毒神掌
1. 第一遍：
    1. 5-15分钟：读题+思考
    2. 直接看题解：注意！多解法，比较解法优劣（LeetCode题解、国际站的Top Discuss）
    3. 背诵、默写好的解法
2. 第二遍：
    1. 马上自己写-->LeetCode提交
    2. 多种解法比较、体会-->优化
3. 第三遍：
    1. 一天后再进行练习
    2. 不同解法的熟练程度-->专项练习
4. 第四遍：一周后再进行练习，对不熟悉题目进行专项练习
5. 第五遍：面试前一到两周进行恢复性练习

# 8、面试技巧
1. Clarification：明确题目意思、边界、数据规模
2. Possible solutions：穷尽所有可能的解法
    1. 比较时间复杂度/空间复杂度
    2. optimal solution找出最优解
3. Coding：代码简洁、高性能、美感
4. Test cases 测试示例
