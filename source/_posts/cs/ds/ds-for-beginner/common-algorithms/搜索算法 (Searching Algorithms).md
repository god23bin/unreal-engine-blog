---
title: 搜索算法 (Searching Algorithms)
date: 2025/1/01 12:47:25
index_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201338383.jpg
banner_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201338383.jpg
categories:
  - [计算机科学基础,数据结构,初学者入门,4.常用算法]
tag:
  - 数据结构
  - 搜索算法
published: true
---

## 搜索算法 (Searching Algorithms)

**概念：在数据集合中查找特定元素 (目标值) 的算法**

**搜索算法 (Searching Algorithms)** ，也称为查找算法，是计算机科学中另一类基础且重要的算法。  它的目标是在一个 **数据集合**  （例如，数组、列表、集合、树、图）中 **查找**  是否 **存在**  一个 **特定的元素**  （称为 **目标值** 或 **键值**），如果存在，则返回该元素的位置或相关信息，如果不存在，则返回未找到的标识。

搜索在各种应用中都非常常见，例如，在网页中搜索关键词、在数据库中查找记录、在文件中搜索内容等等。  

高效的搜索算法可以显著提高程序的运行效率。

**常见搜索算法类型：**

搜索算法根据不同的搜索策略和数据结构，可以分为多种类型。  主要的分类方式可以根据数据是否 **有序**  来划分：

*   **无序数据搜索：**  当数据集合是 **无序的**  （元素之间没有特定的排列顺序）时，只能采用 **线性搜索**  等方法逐个比较元素。  线性查找 (Linear Search) 是最基本的无序数据搜索算法。
*   **有序数据搜索：**  当数据集合是 **有序的**  （例如，升序或降序排列）时，可以利用数据的有序性，采用更高效的搜索算法，例如 **二分查找 (Binary Search)** 。  二分查找比线性查找效率更高，但前提是数据必须有序。
*   **基于数据结构的搜索：**  某些数据结构本身就支持高效的搜索操作，例如 **哈希表 (Hash Table)**  可以在平均 O(1) 时间内完成查找，**二叉搜索树 (Binary Search Tree - BST)**  和 **平衡二叉树 (Balanced BST)**  可以在 O(log n) 时间内完成查找。  这些数据结构本身就内置了搜索算法。
*   **图搜索算法：**  在 **图 (Graph)**  数据结构中，需要使用专门的图搜索算法，例如 **广度优先搜索 (BFS)**  和 **深度优先搜索 (DFS)**  来查找节点或路径。

接下来，我们将重点介绍两种最基本的搜索算法：**线性查找**  和 **二分查找**。

---

### 1. 线性查找 (Linear Search)

**概念：从数据集合的第一个元素开始，逐个比较每个元素，直到找到目标值或遍历完整个集合**

**线性查找 (Linear Search)** ，也称为 **顺序查找 (Sequential Search)** ，是最简单、最直接的搜索算法。  它的思想非常朴素：  **从数据集合的第一个元素开始，按照顺序逐个遍历数据集合中的每个元素，将当前元素与目标值进行比较。  如果当前元素等于目标值，则查找成功，返回当前元素的位置 (索引)。  如果遍历完整个数据集合仍然没有找到目标值，则查找失败，返回未找到标识 (例如，返回 -1)。**

*   **算法步骤：**

    1.  **从数据集合的第一个元素开始遍历 (索引 0)。**
    2.  **将当前元素与目标值进行比较。**
    3.  **如果当前元素等于目标值，则查找成功，返回当前元素的索引。**
    4.  **如果当前元素不等于目标值，则移动到下一个元素 (索引加 1)，继续比较。**
    5.  **如果遍历完整个数据集合仍然没有找到目标值，则查找失败，返回未找到标识 (例如，-1)。**

*   **动画演示 (线性查找过程):**

*   **特性：**

    *   **简单易懂，实现简单：**  线性查找是所有搜索算法中最简单的，易于理解和实现。
    *   **适用性广：**  线性查找 **对数据集合的结构没有特殊要求**，可以用于 **无序**  和 **有序**  的数据集合。  对于链表等线性结构的数据集合，线性查找是唯一可行的搜索方法 (如果数据无序)。
    *   **原地搜索 (In-place Search):**  线性查找不需要额外的辅助空间，空间复杂度为 **O(1)** 。
    *   **效率较低：**  线性查找的时间复杂度较高，平均和最坏情况时间复杂度都为 **O(n)** ，n 为数据集合的大小。  当数据量很大时，线性查找效率较低。

*   **适用场景：**

    *   **小规模数据：**  对于数据量较小的数据集合，线性查找的性能尚可接受。
    *   **无序数据：**  当数据集合是无序的时，只能使用线性查找。
    *   **链表等线性结构：**  对于链表等不支持随机访问的数据结构，线性查找可能是唯一的选择。
    *   **作为更复杂算法的组成部分：**  例如，在某些情况下，线性查找可以作为更复杂算法的子程序使用。
    *   **不适合大规模、性能敏感的搜索任务。**

*   **代码示例 (C++, Java, Python):**

    **C++:**

    ```c++
    #include <iostream>
    #include <vector>

    int linearSearch(const std::vector<int>& arr, int target) {
        int n = arr.size();
        for (int i = 0; i < n; ++i) {
            if (arr[i] == target) {
                return i; // 找到目标值，返回索引
            }
        }
        return -1; // 未找到目标值，返回 -1
    }

    int main() {
        std::vector<int> numbers = {2, 5, 8, 12, 16, 23, 38, 56, 72, 91};
        int targetValue = 23;
        int index = linearSearch(numbers, targetValue);
        if (index != -1) {
            std::cout << "元素 " << targetValue << " 在数组中的索引为: " << index << std::endl;
        } else {
            std::cout << "元素 " << targetValue << " 未在数组中找到" << std::endl;
        }
        return 0;
    }
    ```

    **Java:**

    ```java
    public class LinearSearch {
        public static int linearSearch(int[] arr, int target) {
            int n = arr.length;
            for (int i = 0; i < n; ++i) {
                if (arr[i] == target) {
                    return i; // 找到目标值，返回索引
                }
            }
            return -1; // 未找到目标值，返回 -1
        }

        public static void main(String[] args) {
            int[] numbers = {2, 5, 8, 12, 16, 23, 38, 56, 72, 91};
            int targetValue = 23;
            int index = linearSearch(numbers, targetValue);
            if (index != -1) {
                System.out.println("元素 " + targetValue + " 在数组中的索引为: " + index);
            } else {
                System.out.println("元素 " + targetValue + " 未在数组中找到");
            }
        }
    }
    ```

    **Python:**

    ```python
    def linear_search(arr, target):
        n = len(arr)
        for i in range(n):
            if arr[i] == target:
                return i # 找到目标值，返回索引
        return -1 # 未找到目标值，返回 -1

    numbers = [2, 5, 8, 12, 16, 23, 38, 56, 72, 91]
    target_value = 23
    index = linear_search(numbers, target_value)
    if index != -1:
        print(f"元素 {target_value} 在数组中的索引为: {index}")
    else:
        print(f"元素 {target_value} 未在数组中找到")
    ```

---

### 2. 二分查找 (Binary Search)

**概念：在有序数据集合中，每次将搜索范围缩小一半，快速查找目标值**  (**前提：有序数据**)

**二分查找 (Binary Search)** ，也称为 **折半查找 (Half-interval Search)** ，是一种效率非常高的搜索算法，但 **前提是数据集合必须是有序的**  (例如，升序排列)。  二分查找的思想类似于猜数字游戏：  如果要在 1 到 100 之间猜一个数字，每次猜测后，告诉你猜大了还是猜小了，你通常会从中间值开始猜，例如先猜 50，然后根据反馈缩小猜测范围。  **二分查找的核心思想就是每次将搜索范围缩小一半，从而快速定位目标值。**

*   **算法步骤 (升序数组):**

    1.  **初始化搜索范围：**  设置 **左边界 `left`**  为数据集合的 **起始索引 (0)** ，**右边界 `right`**  为数据集合的 **末尾索引 (n-1)** 。
    2.  **循环查找：**  当 `left <= right`  时，循环执行以下操作：
        a.  计算 **中间索引 `mid`**：`mid = left + (right - left) / 2`  (为了防止 `(left + right)`  溢出，推荐使用这种写法)。
        b.  **比较中间元素 `arr[mid]`  与目标值 `target`：**
            *   **如果 `arr[mid] == target`，则查找成功，返回中间索引 `mid`。**
                *   **如果 `arr[mid] < target`，说明目标值在中间元素的右侧，将左边界 `left`  更新为 `mid + 1`，继续在右半部分搜索。**
                    *   **如果 `arr[mid] > target`，说明目标值在中间元素的左侧，将右边界 `right`  更新为 `mid - 1`，继续在左半部分搜索。**
    3.  **查找失败：**  如果循环结束时 `left > right`，说明搜索范围为空，未找到目标值，返回未找到标识 (例如，-1)。

*   **动画演示 (二分查找过程):**

*   **特性：**

    *   **高效快速：**  二分查找的时间复杂度非常低，平均、最佳、最坏情况时间复杂度都为 **O(log n)** ，n 为数据集合的大小。  这意味着，即使数据量很大，二分查找也能在很少的次数内找到目标值。  例如，在 10 亿个有序数据中查找一个元素，二分查找最多只需要约 30 次比较。
    *   **前提条件严格：**  **二分查找只能用于有序的数据集合。**  如果数据无序，则无法使用二分查找。  如果数据集合需要频繁插入和删除元素，维护有序性可能会带来额外的开销。
    *   **要求随机访问：**  二分查找需要 **随机访问**  数据集合中的元素 (通过索引访问)，因此 **不适合用于链表**  等不支持高效随机访问的数据结构。  通常用于 **数组**  等顺序存储结构。
    *   **原地搜索 (In-place Search):**  二分查找只需要常数级别的辅助空间，空间复杂度为 **O(1)** 。

*   **适用场景：**

    *   **有序数组的查找：**  二分查找最典型的应用场景就是在有序数组中查找元素。
    *   **字典、电话簿等有序数据查找：**  例如，在字典中查找单词、在电话簿中查找电话号码，都可以使用类似于二分查找的思想。
    *   **数值范围查找：**  在某个有序数值范围内查找满足特定条件的值，例如，在排序数组中查找第一个大于等于某个值的元素、查找最后一个小于等于某个值的元素等。
    *   **作为其他算法的子程序：**  例如，在某些高级算法中，二分查找可以作为快速定位搜索范围的子步骤使用。
    *   **不适合无序数据、动态变化数据、或不支持随机访问的数据结构。**

*   **代码示例 (C++, Java, Python):**

    **C++:**

    ```c++
    #include <iostream>
    #include <vector>

    int binarySearch(const std::vector<int>& arr, int target) {
        int left = 0, right = arr.size() - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2; // 计算中间索引
            if (arr[mid] == target) {
                return mid; // 找到目标值，返回索引
            } else if (arr[mid] < target) {
                left = mid + 1; // 目标值在右半部分
            } else {
                right = mid - 1; // 目标值在左半部分
            }
        }
        return -1; // 未找到目标值，返回 -1
    }

    int main() {
        std::vector<int> numbers = {2, 5, 8, 12, 16, 23, 38, 56, 72, 91}; // 有序数组
        int targetValue = 23;
        int index = binarySearch(numbers, targetValue);
        if (index != -1) {
            std::cout << "元素 " << targetValue << " 在数组中的索引为: " << index << std::endl;
        } else {
            std::cout << "元素 " << targetValue << " 未在数组中找到" << std::endl;
        }
        return 0;
    }
    ```

    **Java:**

    ```java
    public class BinarySearch {
        public static int binarySearch(int[] arr, int target) {
            int left = 0, right = arr.length - 1;
            while (left <= right) {
                int mid = left + (right - left) / 2; // 计算中间索引
                if (arr[mid] == target) {
                    return mid; // 找到目标值，返回索引
                } else if (arr[mid] < target) {
                    left = mid + 1; // 目标值在右半部分
                } else {
                    right = mid - 1; // 目标值在左半部分
                }
            }
            return -1; // 未找到目标值，返回 -1
        }

        public static void main(String[] args) {
            int[] numbers = {2, 5, 8, 12, 16, 23, 38, 56, 72, 91}; // 有序数组
            int targetValue = 23;
            int index = binarySearch(numbers, targetValue);
            if (index != -1) {
                System.out.println("元素 " + targetValue + " 在数组中的索引为: " + index);
            } else {
                System.out.println("元素 " + targetValue + " 未在数组中找到");
            }
        }
    }
    ```

    **Python:**

    ```python
    def binary_search(arr, target):
        left, right = 0, len(arr) - 1
        while left <= right:
            mid = left + (right - left) // 2 # 计算中间索引
            if arr[mid] == target:
                return mid # 找到目标值，返回索引
            elif arr[mid] < target:
                left = mid + 1 # 目标值在右半部分
            else:
                right = mid - 1 # 目标值在左半部分
        return -1 # 未找到目标值，返回 -1

    numbers = [2, 5, 8, 12, 16, 23, 38, 56, 72, 91] # 有序数组
    target_value = 23
    index = binary_search(numbers, target_value)
    if index != -1:
        print(f"元素 {target_value} 在数组中的索引为: {index}")
    else:
        print(f"元素 {target_value} 未在数组中找到")
    ```

*   **不同查找算法的效率和使用条件比较：**

    | 查找算法     | 数据是否有序 | 时间复杂度 (平均/最坏) | 空间复杂度 | 适用场景                                     |
    | ------------ | -------- | ------------------ | -------- | --------------------------------------------- |
    | 线性查找     | **无序/有序** | O(n)              | O(1)     | 小规模数据，无序数据，链表等线性结构               |
    | 二分查找     | **有序**   | **O(log n)**       | O(1)     | 大规模有序数据，有序数组，静态数据集合，快速查找         |


## 总结

选择合适的搜索算法取决于数据的特点和应用场景。  **线性查找**  简单通用，但效率较低，适用于小规模无序数据。  **二分查找**  高效快速，但要求数据必须有序，适用于大规模有序数据。  在实际应用中，需要根据数据量、数据是否有序、是否需要频繁插入删除、性能要求等因素综合考虑，选择最合适的搜索算法。  对于需要频繁查找的数据，可以考虑使用更高级的数据结构，例如哈希表或平衡二叉搜索树，以获得更高的搜索效率。