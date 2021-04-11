## 动态规划（Dynamic Program）

#### 1. 定义：

动态规划（英语：Dynamic programming，简称DP）是一种在数学、管理科学、计算机科学、经济学和生物信息学中使用的，通过把原问题分解为相对简单的子问题的方式求解复杂问题的方法。 动态规划常常适用于有重叠子问题[1]和最优子结构性质的问题，动态规划方法所耗时间往往远少于朴素解法。 动态规划背后的基本思想非常简单。大致上，若要解一个给定问题，我们需要解其不同部分（即子问题），再根据子问题的解以得出原问题的解。 通常许多子问题非常相似，为此动态规划法试图仅仅解决每个子问题一次，从而减少计算量：一旦某个给定子问题的解已经算出，则将其记忆化存储，以便下次需要同一个子问题解之时直接查表。这种做法在重复子问题的数目关于输入的规模呈指数增长时特别有用。

#### 2. 要点：

1. 递归树时间复杂度 = 子问题个数 * 子问题时间。
  
2. 斐波那契数列：重叠子问题（备忘录）、最优子结构、状态转移方程。（自顶向下）
  
3. 动态规划：（自底向上）：base case => 转移状态 => 选择状态 => dp数组
  
4. 最优子结构（求最值）：问题的答案，可以通过求解子问题得到 => 如何改造重叠子问题，成最优子结构。
  

### 一、最长递增子序列

#### 解法一：动态规划

思路：**`dp[i]` 表示以 `nums[i]` 这个数结尾的最长递增子序列的长度**）

动态规划: [力扣](https://leetcode-cn.com/problems/number-of-longest-increasing-subsequence/solution/zui-chang-di-zeng-zi-xu-lie-de-ge-shu-by-leetcode/)

#### 解法二：二分查找

思路：**patience game 的纸牌游戏**，只能把点数小的牌压到点数比它大的牌上；如果当前牌点数较大没有可以放置的堆，则新建一个堆，把这张牌放进去；如果当前牌有多个堆可供选择，则选择最左边的那一堆放置。（数学规则执行，就能得到最长递增子序列）

二分查找：

### 二·、高楼扔鸡蛋

题目：你面前有一栋从 1 到 `N` 共 `N` 层的楼，然后给你 `K` 个鸡蛋（`K` 至少为 1）。现在确定这栋楼存在楼层 `0 <= F <= N`，在这层楼将鸡蛋扔下去，鸡蛋**恰好没摔碎**（高于 `F` 的楼层都会碎，低于 `F` 的楼层都不会碎）。现在问你，**最坏**情况下，你**至少**要扔几次鸡蛋，才能**确定**这个楼层 `F` 呢？

#### 问题分析：

- **变化的状态：** 当前拥有的鸡蛋数 `K` 和需要测试的楼层数 `N`。随着测试的进行，鸡蛋个数可能减少，楼层的搜索范围会减小，这就是状态的变化。
  
- **选择：** 选择哪层楼扔鸡蛋
  

#### 选择策略：

1. 线性扫描：我先在 1 楼扔一下，没碎，我再去 2 楼扔一下，没碎，我再去 3 楼…… 
  
2. 二分查找（最佳），我先去第 `(1 + 7) / 2 = 4` 层扔一下。如果不限制鸡蛋个数的话，二分思路显然可以得到最少尝试的次数，但问题是，**现在给你了鸡蛋个数的限制 `K`，直接使用二分思路就不行了**。
  
3. 二者的区别：二分查找每次选择到楼层区间的中间去扔鸡蛋，而线性扫描选择一层层向上测试。不同的选择会造成状态的转移。
  

#### 二分思路：

1. **base case 理解**：当楼层数 `N` 等于 0 时，显然不需要扔鸡蛋；当鸡蛋数 `K` 为 1 时，显然只能线性扫描所有楼层。
  
2. **复杂度分析**：动态规划算法的时间复杂度就是子问题个数 × 函数本身的复杂度。函数本身的复杂度就是忽略递归部分的复杂度，这里 `dp` 函数中有一个 for 循环，所以函数本身的复杂度是 O(N)。子问题个数也就是不同状态组合的总数，显然是两个状态的乘积，也就是 O(KN)。所以算法的总时间复杂度是 O(K*N^2), 空间复杂度 O(KN)。
  
3. **优化方向：**
  
  - 修改代码中的 for 循环为二分搜索，可以将时间复杂度降为 O(K*N*logN)；
    
  - 再改进动态规划解法可以进一步降为 O(KN)；
    
  - 使用数学方法解决，时间复杂度达到最优 O(K*logN)，空间复杂度达到 O(1)。
    
4. **二分搜索**，相当于求 Valley（山谷）值，可以用二分查找来快速寻找这个点。