---
title: 递归 (Recursion) 与 动态规划 (Dynamic Programming)
date: 2025/1/01 12:49:25
index_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201338383.jpg
banner_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201338383.jpg
categories:
  - [计算机科学基础,数据结构,初学者入门,4.常用算法]
tag:
  - 数据结构
  - 递归
  - 动态规划
published: true
---

## 递归 (Recursion)

**概念：函数调用自身**

**递归 (Recursion)** 是一种非常重要的编程技巧，它描述的是 **函数在自身定义中调用自身** 的过程。  你可以把递归想象成一面镜子对着另一面镜子，镜子中又反映镜子，无限循环下去。 在编程中，递归函数就是这样，它会不断地调用自身，直到满足某个 **终止条件**  才停止。

**核心思想：**  将一个 **复杂的问题**  分解成 **规模更小、结构相同**  的 **子问题** 。  然后通过 **解决子问题**  来最终 **解决原问题** 。  递归的关键在于每次函数调用时，问题的规模都必须有所 **缩小**，并且最终要达到一个可以直接解决的 **基本情况 (base case)** ，也就是 **终止条件**。

**应用：树的遍历、分治算法等**

递归在很多算法和数据结构中都有广泛的应用，尤其是在处理 **树形结构** 和实现 **分治算法**  时，递归往往是最自然、最简洁的解决方案。

1. **树的遍历 (Tree Traversal)：**  例如，二叉树的前序遍历、中序遍历、后序遍历等，都可以使用递归非常优雅地实现。  递归的结构天然地与树的层次结构相吻合。

   **示例 - 二叉树前序遍历 (Preorder Traversal):**

   ```
   前序遍历 (根 -> 左子树 -> 右子树):
   
   procedure preorder(root)
      if root is null then
         return
      end if
   
      访问 root 节点 (例如，打印节点值)
      preorder(root.left)  // 递归遍历左子树
      preorder(root.right) // 递归遍历右子树
   end procedure
   ```

2.  **分治算法 (Divide and Conquer Algorithms)：**  许多经典的分治算法都使用递归来实现，例如：

    *   **归并排序 (Merge Sort):**  递归地将数组分成两半，分别排序，然后合并排序好的两半。
    *   **快速排序 (Quick Sort):**  递归地选择一个基准值，将数组划分为左右两部分，分别排序。
    *   **二分查找 (Binary Search):**  递归地在有序数组的左右两半查找目标值。


*   **注意：理解递归的终止条件和栈溢出问题**

    在使用递归时，务必注意两个关键点，否则可能会导致程序出错甚至崩溃：

    1. **终止条件 (Base Case)：**  **递归必须要有明确的终止条件。**  终止条件定义了递归何时停止调用自身，开始返回结果。  **如果没有终止条件，递归函数会无限地调用自身，形成无限循环，最终导致程序栈溢出。**  在设计递归函数时，首先要考虑清楚基本情况，即问题规模缩小到什么程度时，可以直接给出答案，而不需要继续递归。

    2. **栈溢出 (Stack Overflow)：**  **递归的每一次函数调用都会在计算机的调用栈 (Call Stack) 中分配一块内存空间，用于存储函数的局部变量、参数、返回地址等信息。**  如果递归调用的 **深度过大**  （即递归层数太多），调用栈可能会被耗尽，导致 **栈溢出 (Stack Overflow) 错误**，程序崩溃。
    
      **如何避免栈溢出：**
   
      *   **优化递归算法：**  尽量减少不必要的递归调用，优化递归逻辑，降低递归深度。
      *   **使用迭代 (循环) 替代递归：**  很多递归算法都可以用迭代方式改写，迭代方式通常不会有栈溢出的问题，因为迭代只使用固定的栈空间。
      *   **限制递归深度：**  某些编程语言或环境提供了设置最大递归深度的机制，可以限制递归调用的层数，防止无限递归导致程序崩溃，但这只是最后的保护手段，并不能根本解决问题。

## 动态规划 (Dynamic Programming)

**概念：将复杂问题分解成子问题，存储子问题的解，避免重复计算，提高效率**

**动态规划 (Dynamic Programming, DP)**  是一种非常强大的算法设计技巧，主要用于解决 **优化问题**  （例如，求最大值、最小值、最长、最短、计数等）。 

动态规划的核心思想是： **将一个复杂的、规模较大的问题分解成若干个相互重叠的、规模较小的子问题**，然后 **自底向上 (bottom-up)**  或 **自顶向下 (top-down with memoization)**  地 **求解子问题**，并将 **子问题的解存储起来**，以便在求解更大规模的问题时 **直接查表复用**，**避免重复计算**，从而 **提高效率**。

### 动态规划的关键特点

*   **重叠子问题 (Overlapping Subproblems)：**  在分解问题的过程中，**不同的分支会遇到相同的子问题。**  动态规划通过 **存储子问题的解**  来避免对这些重叠子问题进行重复计算，这是动态规划提高效率的关键。
*   **最优子结构 (Optimal Substructure)：**  **原问题的最优解可以通过子问题的最优解组合而成。**  这意味着，我们可以通过求解子问题的最优解来构建原问题的最优解。  最优子结构是动态规划能够解决优化问题的基础。

* **适用场景：求解最优解问题，例如：背包问题、最长公共子序列等**

  动态规划非常适合解决具有 **重叠子问题**  和 **最优子结构**  性质的 **优化问题**。  常见的动态规划应用场景包括：

  1. **背包问题 (Knapsack Problem)：**  在容量有限的背包中放入价值最大的物品组合。  例如，0-1 背包问题、完全背包问题、多重背包问题等。

  2. **最长公共子序列 (Longest Common Subsequence, LCS)：**  找到两个字符串的最长公共子序列。

  3.  **最长递增子序列 (Longest Increasing Subsequence, LIS)：**  在一个序列中找到最长的递增子序列。

  4.  **编辑距离 (Edit Distance) / 莱文斯坦距离 (Levenshtein Distance)：**  计算将一个字符串转换为另一个字符串所需的最少编辑操作次数 (插入、删除、替换)。

  5.  **路径计数问题：**  例如，在网格中从左上角走到右下角的路径数量、在图中从一个节点到另一个节点的路径数量等。

  6.  **区间 DP：**  例如，矩阵链乘法、石子合并等。

  7.  **树形 DP：**  例如，树的最大独立集、树的直径等。


### 学习动态规划的基本思想和步骤（定义状态、状态转移方程、初始条件）

学习动态规划，关键是掌握其基本思想和步骤。  解决动态规划问题，通常需要以下几个核心步骤：

#### 1. 定义状态 (Define State)：

**状态**  是对 **子问题**  的精确描述。  **状态定义必须满足“无后效性”**，即当前状态的决策不会影响未来的状态，未来的状态只取决于当前状态和之前的状态。  **状态通常用一个或多个变量来表示**，例如，`dp[i]`、`dp[i][j]`、`dp[i][j][k]`  等。  状态的定义需要根据具体问题来确定，**关键是要能够表示子问题，并且能够推导出状态转移方程。**



**如何定义状态？**

*   **考虑问题的“最后一步”：**  思考问题的最优解的“最后一步”是如何构成的，这通常能帮助你找到状态的定义。
*   **尝试用形式化的方式描述子问题：**  例如，对于背包问题，可以用 `dp[i][w]`  表示前 `i`  个物品，背包容量为 `w`  时的最大价值。  对于最长公共子序列问题，可以用 `dp[i][j]`  表示字符串 `s1`  的前 `i`  个字符和字符串 `s2`  的前 `j`  个字符的最长公共子序列长度。



#### 2. 定义状态转移方程 (Define State Transition Equation / Recurrence Relation)：  

**状态转移方程**  描述了 **状态之间是如何转移的，即如何从已知的子问题的解，推导出更大规模的问题的解。**  状态转移方程是动态规划的核心，它体现了 **最优子结构**  的性质。  状态转移方程通常是一个 **递推关系式**，例如，`dp[i] = max(dp[i-1] + value[i], dp[i-2] + value[i-1])`  等。  **推导状态转移方程的关键是要正确地分析问题结构，找到子问题之间的依赖关系。**



**如何推导状态转移方程？**

*   **基于状态定义，思考子问题之间的联系：**  例如，对于背包问题 `dp[i][w]`，考虑第 `i`  个物品放还是不放，从而将问题分解为 `dp[i-1][w]`  和 `dp[i-1][w - weight[i]]`  两种情况。
*   **画出状态转移图 (可选)：**  对于一些问题，可以画出状态转移图，帮助理清状态之间的依赖关系。



#### 3. 定义初始条件 (Define Initial Conditions / Base Cases)：  

**初始条件**  是 **最基本的、规模最小的子问题的解，它们是动态规划递推计算的起点。**  初始条件通常对应于状态的边界情况，例如，`dp[0] = 0`、`dp[1] = value[1]`  等。  **初始条件必须能够直接计算出来，并且能够正确地启动状态转移方程的递推过程。**



**如何确定初始条件？**

*   **考虑状态的最小可能取值：**  例如，对于背包问题 `dp[i][w]`，当 `i = 0`  或 `w = 0`  时，背包价值为 0，可以作为初始条件。
*   **根据状态转移方程反推：**  状态转移方程通常是递推关系，初始条件是递推的起点，可以根据状态转移方程反推初始条件应该是什么。



#### 4.确定计算顺序和实现方式：  

动态规划的计算顺序通常是 **自底向上 (bottom-up)**  或 **自顶向下 (top-down with memoization)** 。

*   **自底向上 (Bottom-up / 迭代)：**  **从规模最小的子问题开始计算**，逐步递推到更大规模的问题，直到计算出原问题的解。  自底向上通常使用 **循环 (for loop)**  来实现。  **更常用，效率更高 (通常)。**
*   **自顶向下 (Top-down with Memoization / 递归 + 记忆化搜索)：**  **从原问题开始，递归地求解子问题。**  为了避免重复计算，使用 **记忆化 (memoization)**  技术，将已经计算过的子问题的解存储起来 (例如，使用哈希表或数组)，下次遇到相同的子问题时，直接查表返回，而不需要重复计算。  自顶向下通常使用 **递归 + 记忆化**  来实现。  **代码更简洁，更符合人的思维习惯，但可能存在额外的递归调用开销。**



### 代码实现

 **(示例 - 斐波那契数列的动态规划实现，自底向上和自顶向下两种方式):**

**C++ (自底向上):**

```c++
#include <iostream>
#include <vector>

int fibonacciDP_BottomUp(int n) {
    if (n <= 1) return n;
    std::vector<int> dp(n + 1); // DP 数组，dp[i] 表示第 i 个斐波那契数
    dp[0] = 0; // 初始条件
    dp[1] = 1; // 初始条件
    for (int i = 2; i <= n; ++i) {
        dp[i] = dp[i - 1] + dp[i - 2]; // 状态转移方程
    }
    return dp[n];
}

int main() {
    int n = 10;
    std::cout << "斐波那契数列第 " << n << " 项 (自底向上 DP): " << fibonacciDP_BottomUp(n) << std::endl;
    return 0;
}
```

**Java (自底向上):**

```java
public class FibonacciDP {
    public static int fibonacciDP_BottomUp(int n) {
        if (n <= 1) return n;
        int[] dp = new int[n + 1]; // DP 数组，dp[i] 表示第 i 个斐波那契数
        dp[0] = 0; // 初始条件
        dp[1] = 1; // 初始条件
        for (int i = 2; i <= n; ++i) {
            dp[i] = dp[i - 1] + dp[i - 2]; // 状态转移方程
        }
        return dp[n];
    }

    public static void main(String[] args) {
        int n = 10;
        System.out.println("斐波那契数列第 " + n + " 项 (自底向上 DP): " + fibonacciDP_BottomUp(n));
    }
}
```

**Python (自底向上):**

```python
def fibonacci_dp_bottom_up(n):
    if n <= 1:
        return n
    dp = [0] * (n + 1) # DP 数组，dp[i] 表示第 i 个斐波那契数
    dp[0] = 0 # 初始条件
    dp[1] = 1 # 初始条件
    for i in range(2, n + 1):
        dp[i] = dp[i - 1] + dp[i - 2] # 状态转移方程
    return dp[n]

n = 10
print(f"斐波那契数列第 {n} 项 (自底向上 DP): {fibonacci_dp_bottom_up(n)}")
```

**C++ (自顶向下 - 记忆化搜索):**

```c++
#include <iostream>
#include <vector>
#include <unordered_map>

std::unordered_map<int, int> memo; // 记忆化表，存储已计算过的子问题的解

int fibonacciDP_TopDown(int n) {
    if (n <= 1) return n;
    if (memo.count(n)) { // 查表，如果已计算过，直接返回
        return memo[n];
    }
    int result = fibonacciDP_TopDown(n - 1) + fibonacciDP_TopDown(n - 2); // 递归计算
    memo[n] = result; // 存储计算结果
    return result;
}

int main() {
    int n = 10;
    std::cout << "斐波那契数列第 " << n << " 项 (自顶向下 DP): " << fibonacciDP_TopDown(n) << std::endl;
    return 0;
}
```

**Java (自顶向下 - 记忆化搜索):**

```java
import java.util.HashMap;
import java.util.Map;

public class FibonacciDP {
    static Map<Integer, Integer> memo = new HashMap<>(); // 记忆化表

    public static int fibonacciDP_TopDown(int n) {
        if (n <= 1) return n;
        if (memo.containsKey(n)) { // 查表
            return memo.get(n);
        }
        int result = fibonacciDP_TopDown(n - 1) + fibonacciDP_TopDown(n - 2); // 递归计算
        memo.put(n, result); // 存储结果
        return result;
    }

    public static void main(String[] args) {
        int n = 10;
        System.out.println("斐波那契数列第 " + n + " 项 (自顶向下 DP): " + fibonacciDP_TopDown(n));
    }
}
```

**Python (自顶向下 - 记忆化搜索):**

```python
memo = {} # 记忆化表

def fibonacci_dp_top_down(n):
    if n <= 1:
        return n
    if n in memo: # 查表
        return memo[n]
    result = fibonacci_dp_top_down(n - 1) + fibonacci_dp_top_down(n - 2) # 递归计算
    memo[n] = result # 存储结果
    return result

n = 10
print(f"斐波那契数列第 {n} 项 (自顶向下 DP): {fibonacci_dp_top_down(n)}")
```



## 总结

递归和动态规划是两种非常重要的算法设计技巧。 **递归**  通过函数调用自身来解决问题，代码简洁优雅，但需要注意终止条件和栈溢出问题。 **动态规划**  通过分解子问题、存储子问题解、避免重复计算来提高效率，尤其适用于解决优化问题。  掌握递归和动态规划的思想和方法，能够帮助你更好地解决各种复杂算法问题。