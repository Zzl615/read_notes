# 二分查找

Knuth 大佬（发明 KMP 算法的那位）都说二分查找：**思路很简单，细节是魔鬼**。

时间复杂度：logN

用途：简化连续的空间线性搜索

### 一、 基本的二分搜索

当初始化 right = nums.length - 1时，搜索区间是 [left, right]，循环终止条件是 left <= right (left == right + 1)，区间的形式就是 `[right + 1, right]`，区间更新方式：left = mid+1 和 right = mid-1，因为只需要找到一个 target 的索引，所以当 nums[mid] == target 时立即返回。

### 二、左侧边界的二分搜索

当初始化 right = nums.length时，搜索区间是 [left, right)，循环终止条件是 left < right (left == right),区间的形式就是 `[right, right)`，区间更新方式：left = mid+1 和 right = mid，因为需要找到 target 的最左侧索引，所以当 nums[mid] == target 时不要立即返回，而要收紧右侧边界以锁定左侧边界

### 三、右侧边界的二分搜索

当初始化 right = nums.length，搜索区间是 [left, right)
循环终止条件是 left < right (left == right),区间的形式就是 `[right, right)`，区间更新方式：left = mid+1 和 right = mid ，因为需要找到 target 的最右侧索引，所以当 nums[mid] == target 时不要立即返回，而要收紧左侧边界以锁定右侧边界，又因为收紧左侧边界时必须 left = mid + 1，所以最后无论返回 left 还是 right，必须减一。

终止条件：while 的退出条件是 `left == right + 1`

搜索区间：两端都闭，左闭右开

总结：

1、分析二分查找代码时，不要出现 else，全部展开成 else if 方便理解。

2、注意「搜索区间」和 while 的终止条件，如果存在漏掉的元素，记得在最后检查。

3、如需定义左闭右开的「搜索区间」搜索左右边界，只要在 `nums[mid] == target` 时做修改即可，搜索右侧时需要减一。

4、如果将「搜索区间」全都统一成两端都闭，好记，只要稍改 `nums[mid] == target` 条件处的代码和返回的逻辑即可，**推荐拿小本本记下，作为二分搜索模板**。

例子：



[3. 二分查找详解](https://github.com/labuladong/fucking-algorithm/blob/master/%E7%AE%97%E6%B3%95%E6%80%9D%E7%BB%B4%E7%B3%BB%E5%88%97/%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE%E8%AF%A6%E8%A7%A3.md)
