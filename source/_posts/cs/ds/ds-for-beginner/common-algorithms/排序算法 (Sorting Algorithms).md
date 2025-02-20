---
title: 排序算法 (Sorting Algorithms)
date: 2025/1/01 12:46:25
index_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201338383.jpg
banner_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201338383.jpg
categories:
  - [计算机科学基础,数据结构,初学者入门,4.常用算法]
tag:
  - 数据结构
  - 排序算法
published: true
---

## 排序算法 (Sorting Algorithms)

**概念：将一组数据按照某种规则 (例如，升序或降序) 重新排列的算法**

**排序算法 (Sorting Algorithms)** 是计算机科学中最基础和最重要的算法之一。 它的目标是将一组 **无序的数据**  （例如，数组、列表）重新排列成 **有序的序列**，使得数据按照某种预定的规则排列，例如：

*   **升序排序 (Ascending Order):**  将数据从小到大排列 (例如：1, 2, 3, 4, 5...)。
*   **降序排序 (Descending Order):**  将数据从大到小排列 (例如：5, 4, 3, 2, 1...)。
*   也可以根据其他自定义规则排序，例如，按照字符串的字典序、对象的某个属性值等。

排序在计算机应用中非常普遍，例如，对搜索结果排序、对商品价格排序、对学生成绩排序等等。  选择合适的排序算法对于提高程序效率至关重要。

**常见排序算法类型：**

排序算法有很多种，根据不同的特性可以进行不同的分类。  常见的分类方式包括：

*   **比较排序 (Comparison Sort):**  通过 **比较元素之间的大小**  来决定元素的相对顺序。  冒泡排序、选择排序、插入排序、归并排序、快速排序、堆排序等都属于比较排序。  **比较排序的理论时间复杂度下界是 Ω(n log n)**。
*   **非比较排序 (Non-comparison Sort):**  不通过比较元素之间的大小来排序，而是利用数据本身的特性 (例如，数值范围)。  计数排序、基数排序、桶排序等属于非比较排序。  非比较排序可以突破比较排序的下界，在特定条件下达到线性时间复杂度 O(n)。
*   **原地排序 (In-place Sort):**  **不**  需要额外的辅助空间（或只需要常数级别的辅助空间）就可以完成排序。  冒泡排序、选择排序、插入排序、堆排序、快速排序（某些实现）属于原地排序。  原地排序可以节省内存空间。
*   **非原地排序 (Not In-place Sort) / 外部排序 (Out-of-place Sort):**  需要额外的辅助空间来完成排序。  归并排序、计数排序、基数排序、桶排序等通常是非原地排序。  非原地排序可能需要更多的内存空间，但某些非原地排序算法 (例如，归并排序)  的性能更稳定。
*   **稳定排序 (Stable Sort):**  如果排序前 **值相等的元素**  在排序后 **相对位置保持不变**，则该排序算法是稳定的。  插入排序、归并排序、冒泡排序、计数排序、基数排序是稳定的。  选择排序、快速排序、堆排序是不稳定的。  稳定性在某些特定场景下很重要，例如，需要多次排序，并且希望保持之前排序结果的相对顺序时。

接下来，我们将介绍五种常见的比较排序算法：冒泡排序、选择排序、插入排序、归并排序和快速排序。

---

#### 1. 冒泡排序 (Bubble Sort)

**概念：重复遍历列表，比较相邻元素并交换，将较大 (或较小) 的元素逐渐“冒泡”到顶端**

**冒泡排序 (Bubble Sort)** 是一种非常简单直观的排序算法。

它的工作原理就像水中气泡从底部冒到水面一样：  **重复地遍历要排序的列表，每次遍历都比较相邻的两个元素，如果它们的顺序错误 (例如，前一个比后一个大，但要升序排序)，就交换它们的位置。**通过多次遍历，较大（或较小）的元素会像气泡一样逐渐“冒泡”到列表的顶端 (末尾)。

*   **算法步骤 (升序排序):**

    1.  **外层循环：**  控制遍历的轮数。  假设列表长度为 `n`，则需要进行 `n-1` 轮遍历。
    2.  **内层循环：**  在每一轮遍历中，从列表的 **第一个元素**  开始，**逐对比较相邻的两个元素**  (例如，比较索引 `j` 和 `j+1` 的元素)。
    3.  **比较和交换：**  如果 **前一个元素比后一个元素大**，则 **交换**  这两个元素的位置，使得较大的元素向后移动。
    4.  **标记优化 (可选):**  在每一轮遍历中，使用一个 **标记变量**  记录是否发生了元素交换。  如果在某轮遍历中没有发生任何交换，说明列表已经有序，可以提前结束排序，进行优化。

*   **动画演示 (冒泡排序过程):** 自己搜吧~

*   **特性：**

    *   **简单易懂，实现简单：**  冒泡排序是所有排序算法中最简单的之一，易于理解和实现，适合初学者入门。
    *   **原地排序 (In-place Sort):**  只需要常数级别的辅助空间，就可以完成排序。
    *   **稳定排序 (Stable Sort):**  当相邻元素相等时，冒泡排序不会交换它们的位置，因此是稳定的排序算法。
    *   **效率较低：**  冒泡排序的时间复杂度较高，平均和最坏情况时间复杂度都为 **O(n^2)**，对于大规模数据排序效率较低。

* **适用场景：**

  *   **小规模数据：**  对于数据量非常小的列表，冒泡排序的性能尚可接受。
  *   **基本有序的数据：**  如果列表本身已经基本有序，冒泡排序的效率可能会有所提高（最佳情况时间复杂度为 O(n)）。
  *   **不适合大规模、性能敏感的排序任务。**

*   **代码示例 (C++, Java, Python):**

    **C++:**

    ```c++
    #include <iostream>
    #include <vector>
    #include <algorithm> // swap

    void bubbleSort(std::vector<int>& arr) {
        int n = arr.size();
        for (int i = 0; i < n - 1; ++i) {
            bool swapped = false; // 标记是否发生交换，用于优化
            for (int j = 0; j < n - i - 1; ++j) {
                if (arr[j] > arr[j + 1]) {
                    std::swap(arr[j], arr[j + 1]);
                    swapped = true;
                }
            }
            if (!swapped) { // 如果本轮没有发生交换，说明已经有序
                break;
            }
        }
    }

    int main() {
        std::vector<int> numbers = {64, 34, 25, 12, 22, 11, 90};
        bubbleSort(numbers);
        std::cout << "排序后的数组: ";
        for (int number : numbers) {
            std::cout << number << " ";
        }
        std::cout << std::endl;
        return 0;
    }
    ```

    **Java:**

    ```java
    public class BubbleSort {
        public static void bubbleSort(int[] arr) {
            int n = arr.length;
            for (int i = 0; i < n - 1; ++i) {
                boolean swapped = false; // 标记是否发生交换，用于优化
                for (int j = 0; j < n - i - 1; ++j) {
                    if (arr[j] > arr[j + 1]) {
                        int temp = arr[j];
                        arr[j] = arr[j + 1];
                        arr[j + 1] = temp;
                        swapped = true;
                    }
                }
                if (!swapped) { // 如果本轮没有发生交换，说明已经有序
                    break;
                }
            }
        }

        public static void main(String[] args) {
            int[] numbers = {64, 34, 25, 12, 22, 11, 90};
            bubbleSort(numbers);
            System.out.print("排序后的数组: ");
            for (int number : numbers) {
                System.out.print(number + " ");
            }
            System.out.println();
        }
    }
    ```

    **Python:**

    ```python
    def bubble_sort(arr):
        n = len(arr)
        for i in range(n - 1):
            swapped = False # 标记是否发生交换，用于优化
            for j in range(n - i - 1):
                if arr[j] > arr[j + 1]:
                    arr[j], arr[j + 1] = arr[j + 1], arr[j]
                    swapped = True
            if not swapped: # 如果本轮没有发生交换，说明已经有序
                break
        return arr

    numbers = [64, 34, 25, 12, 22, 11, 90]
    sorted_numbers = bubble_sort(numbers)
    print("排序后的数组:", sorted_numbers)
    ```

---

#### 2. 选择排序 (Selection Sort)

**概念：每次从未排序部分选择最小值 (或最大值)，放到已排序部分的末尾**

**选择排序 (Selection Sort)**  的思路也很简单直观。  它将列表分为 **已排序部分**  和 **未排序部分**。  初始时，已排序部分为空，未排序部分包含所有元素。  **每次从未排序部分选择一个最小值 (或最大值)**，将其 **放到已排序部分的末尾**，直到未排序部分为空，排序完成。

*   **算法步骤 (升序排序):**

    1.  **外层循环：**  控制选择的轮数。  假设列表长度为 `n`，则需要进行 `n-1` 轮选择。
    2.  **内层循环：**  在每一轮选择中，从 **未排序部分**  中找到 **最小值**  的索引。
    3.  **交换：**  将找到的 **最小值**  与 **未排序部分的第一个元素**  交换位置，将最小值放到已排序部分的末尾。
    4.  **已排序部分扩大，未排序部分缩小：**  经过一轮选择和交换，未排序部分的最左边元素就成为了已排序部分的新元素。

*   **动画演示 (选择排序过程):**

*   **特性：**

    *   **简单直观，实现简单：**  选择排序也比较容易理解和实现。
    *   **原地排序 (In-place Sort):**  只需要常数级别的辅助空间。
    *   **不稳定排序 (Unstable Sort):**  选择排序在交换元素位置时，可能会改变相等元素的相对顺序，因此是不稳定的排序算法。
    *   **效率较低：**  选择排序的时间复杂度也较高，平均和最坏情况时间复杂度都为 **O(n^2)**，效率不如更高级的排序算法。
    *   **交换次数少：**  选择排序的 **交换次数**  相对较少，最多只需要交换 `n-1` 次（n 为列表长度），这在某些交换操作代价较高的场景下可能是一个优点。

*   **适用场景：**

    *   **与冒泡排序类似**
    *   **当交换操作代价较高，而比较操作代价较低时，选择排序可能比冒泡排序略有优势，因为选择排序的交换次数更少。**
    *   **不适合大规模、性能敏感的排序任务。**

*   **代码示例 (C++, Java, Python):**

    **C++:**

    ```c++
    #include <iostream>
    #include <vector>
    #include <algorithm> // swap, min_element, distance

    void selectionSort(std::vector<int>& arr) {
        int n = arr.size();
        for (int i = 0; i < n - 1; ++i) {
            // 找到未排序部分最小值
            auto min_it = std::min_element(arr.begin() + i, arr.end());
            int min_index = std::distance(arr.begin(), min_it);
            // 交换最小值和未排序部分第一个元素
            std::swap(arr[i], arr[min_index]);
        }
    }

    int main() {
        std::vector<int> numbers = {64, 34, 25, 12, 22, 11, 90};
        selectionSort(numbers);
        std::cout << "排序后的数组: ";
        for (int number : numbers) {
            std::cout << number << " ";
        }
        std::cout << std::endl;
        return 0;
    }
    ```

    **Java:**

    ```java
    public class SelectionSort {
        public static void selectionSort(int[] arr) {
            int n = arr.length;
            for (int i = 0; i < n - 1; ++i) {
                int minIndex = i;
                // 找到未排序部分最小值索引
                for (int j = i + 1; j < n; ++j) {
                    if (arr[j] < arr[minIndex]) {
                        minIndex = j;
                    }
                }
                // 交换最小值和未排序部分第一个元素
                int temp = arr[i];
                arr[i] = arr[minIndex];
                arr[minIndex] = temp;
            }
        }

        public static void main(String[] args) {
            int[] numbers = {64, 34, 25, 12, 22, 11, 90};
            selectionSort(numbers);
            System.out.print("排序后的数组: ");
            for (int number : numbers) {
                System.out.print(number + " ");
            }
            System.out.println();
        }
    }
    ```

    **Python:**

    ```python
    def selection_sort(arr):
        n = len(arr)
        for i in range(n - 1):
            min_index = i
            # 找到未排序部分最小值索引
            for j in range(i + 1, n):
                if arr[j] < arr[min_index]:
                    min_index = j
            # 交换最小值和未排序部分第一个元素
            arr[i], arr[min_index] = arr[min_index], arr[i]
        return arr

    numbers = [64, 34, 25, 12, 22, 11, 90]
    sorted_numbers = selection_sort(numbers)
    print("排序后的数组:", sorted_numbers)
    ```

---

#### 3. 插入排序 (Insertion Sort)

**概念：将列表分为已排序部分和未排序部分，每次从未排序部分取出一个元素，插入到已排序部分的合适位置**

**插入排序 (Insertion Sort)**  就像我们整理扑克牌一样。  我们通常会把牌面朝上放在手中，每次摸到一张新牌，就将它 **插入到手中已排好序的牌的合适位置**，使得手中的牌始终保持有序。  插入排序的原理与之类似：  将列表分为 **已排序部分**  和 **未排序部分**。  初始时，已排序部分只包含第一个元素 (或为空)，未排序部分包含剩余元素。  **每次从未排序部分取出一个元素**，**扫描已排序部分**，找到合适的位置 **插入**，使得插入后已排序部分仍然保持有序。

*   **算法步骤 (升序排序):**

    1.  **外层循环：**  从列表的 **第二个元素**  开始 (索引 1)，遍历到最后一个元素。  当前遍历的元素作为 **待插入元素**。
    2.  **内层循环 (或直接比较和移动):**  将 **待插入元素**  与 **已排序部分**  的元素 **从后向前依次比较**。
    3.  **移动元素，找到插入位置：**  如果 **已排序部分的元素**  比 **待插入元素**  **大**，则将 **已排序元素向后移动一位**，为待插入元素腾出位置。  直到找到一个 **已排序元素小于或等于待插入元素**  的位置，或扫描完已排序部分。
    4.  **插入元素：**  将 **待插入元素**  插入到找到的位置之后 (或已排序部分的最前面)。
    5.  **已排序部分扩大，未排序部分缩小：**  经过一轮插入，待插入元素就成为了已排序部分的新元素。

*   **动画演示 (插入排序过程):**

*   **特性：**

    *   **简单直观，实现简单：**  插入排序也比较容易理解和实现，尤其是在数据量较小时。
    *   **原地排序 (In-place Sort):**  只需要常数级别的辅助空间。
    *   **稳定排序 (Stable Sort):**  插入排序在比较和移动元素时，不会改变相等元素的相对顺序，因此是稳定的排序算法。
    *   **效率相对较高 (对于小规模数据和基本有序数据):**  插入排序的平均时间复杂度为 **O(n^2)**，最坏情况时间复杂度也为 **O(n^2)**，但 **最佳情况时间复杂度为 O(n)**  (当列表已经有序时)。  对于小规模数据和基本有序的数据，插入排序的效率通常比冒泡排序和选择排序更高。
    *   **在线排序算法：**  插入排序是一种 **在线排序算法**，可以一边接收数据，一边进行排序，每次插入新元素时，都能够将当前列表维护成有序状态。

*   **适用场景：**

    *   **小规模数据：**  插入排序对于小规模数据的排序效率较高，在数据量较小时，通常比更复杂的排序算法 (例如，快速排序、归并排序) 性能更好，因为常数因子较小。
    *   **基本有序的数据：**  当列表已经基本有序时，插入排序只需要少量移动操作，效率接近 O(n)，非常高效。
    *   **在线排序：**  适用于需要一边接收数据一边排序的场景。
    *   **作为其他排序算法的优化部分：**  例如，在快速排序和归并排序的优化版本中，当子问题规模较小时，可以切换到插入排序进行排序，以提高整体性能。
    *   **不适合大规模完全无序数据的排序任务，性能不如 O(n log n) 级别的排序算法。**

*   **代码示例 (C++, Java, Python):**

    **C++:**

    ```c++
    #include <iostream>
    #include <vector>

    void insertionSort(std::vector<int>& arr) {
        int n = arr.size();
        for (int i = 1; i < n; ++i) {
            int key = arr[i]; // 待插入元素
            int j = i - 1;
            // 将已排序部分中大于 key 的元素向后移动
            while (j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                --j;
            }
            arr[j + 1] = key; // 插入 key 到合适位置
        }
    }

    int main() {
        std::vector<int> numbers = {64, 34, 25, 12, 22, 11, 90};
        insertionSort(numbers);
        std::cout << "排序后的数组: ";
        for (int number : numbers) {
            std::cout << number << " ";
        }
        std::cout << std::endl;
        return 0;
    }
    ```

    **Java:**

    ```java
    public class InsertionSort {
        public static void insertionSort(int[] arr) {
            int n = arr.length;
            for (int i = 1; i < n; ++i) {
                int key = arr[i]; // 待插入元素
                int j = i - 1;
                // 将已排序部分中大于 key 的元素向后移动
                while (j >= 0 && arr[j] > key) {
                    arr[j + 1] = arr[j];
                    --j;
                }
                arr[j + 1] = key; // 插入 key 到合适位置
            }
        }

        public static void main(String[] args) {
            int[] numbers = {64, 34, 25, 12, 22, 11, 90};
            insertionSort(numbers);
            System.out.print("排序后的数组: ");
            for (int number : numbers) {
                System.out.print(number + " ");
            }
            System.out.println();
        }
    }
    ```

    **Python:**

    ```python
    def insertion_sort(arr):
        n = len(arr)
        for i in range(1, n):
            key = arr[i] # 待插入元素
            j = i - 1
            # 将已排序部分中大于 key 的元素向后移动
            while j >= 0 and arr[j] > key:
                arr[j + 1] = arr[j]
                j -= 1
            arr[j + 1] = key # 插入 key 到合适位置
        return arr

    numbers = [64, 34, 25, 12, 22, 11, 90]
    sorted_numbers = insertion_sort(numbers)
    print("排序后的数组:", sorted_numbers)
    ```

---

#### 4. 归并排序 (Merge Sort)

**概念：分而治之 (Divide and Conquer) 的思想，将列表递归地分成小块，排序小块，然后将排序好的小块合并成更大的有序块**

**归并排序 (Merge Sort)** 是一种基于 **分而治之 (Divide and Conquer)**  思想的高效排序算法。  它的核心思想是将一个大问题分解成若干个小问题，解决小问题，然后将小问题的解合并成大问题的解。  在归并排序中，**将要排序的列表递归地分成越来越小的子列表，直到子列表只包含一个元素 (或为空，此时子列表自然有序)。  然后将这些有序的子列表两两合并 (归并) 成更大的有序列表，直到最终合并成一个完整的有序列表。**

*   **算法步骤 (升序排序):**

    1.  **分解 (Divide):**  将原始列表 **递归地**  分成 **两个子列表**，直到子列表只包含一个元素 (或为空)。  分解过程通常是从列表中间位置将列表分成左右两半。
    2.  **解决 (Conquer):**  当子列表只包含一个元素时，子列表被认为 **已经有序**  (递归的 **base case**)。
    3.  **合并 (Merge):**  将两个 **已排序的子列表**  **合并**  成一个 **更大的有序列表**。  合并过程是归并排序的核心步骤。  合并两个有序列表的基本思路是：
        *   创建一个新的空列表，用于存放合并后的有序列表。
        *   同时遍历两个已排序的子列表，比较两个子列表的当前元素，将 **较小 (或较小) 的元素**  添加到新的列表中，并将对应子列表的指针向后移动一位。
        *   重复比较和添加操作，直到其中一个子列表遍历完。
        *   将另一个子列表的剩余元素 (如果有)  **直接追加**  到新的列表末尾。
    4.  **递归合并：**  递归地将合并后的有序列表作为输入，继续进行合并操作，直到最终合并成一个完整的有序列表。

*   **动画演示 (归并排序过程):**

*   **特性：**

    *   **高效稳定：**  归并排序是一种非常高效的排序算法，平均、最佳、最坏情况时间复杂度都为 **O(n log n)**。  并且是 **稳定排序 (Stable Sort)**。
    *   **分而治之思想：**  归并排序体现了经典的分而治之算法思想，可以将复杂问题分解成更小的、易于解决的子问题。
    *   **递归实现和迭代实现：**  归并排序既可以使用递归方式实现，也可以使用迭代 (循环) 方式实现。  递归实现代码更简洁，但可能存在递归深度限制；迭代实现代码稍复杂，但避免了递归调用开销。
    *   **非原地排序 (Not In-place Sort) / 外部排序 (Out-of-place Sort):**  归并排序在合并过程中 **需要额外的辅助空间**  来存储合并后的有序列表，因此是非原地排序。  辅助空间复杂度为 **O(n)**  (通常需要与原始列表相同大小的辅助空间)。  但也正因为非原地排序的特性，归并排序非常适合用于 **外部排序** (对磁盘上存储的大规模数据进行排序，数据量太大无法一次性加载到内存中)。

*   **适用场景：**

    *   **大规模数据排序：**  归并排序的 O(n log n) 时间复杂度使其非常适合对大规模数据进行排序，效率较高且稳定。
    *   **外部排序：**  归并排序适合对磁盘文件等外部存储介质中的数据进行排序，因为归并排序可以分块处理数据，减少内存需求。
    *   **稳定排序要求：**  如果需要稳定排序算法，归并排序是一个很好的选择。
    *   **并行排序：**  归并排序可以很容易地并行化处理，提高排序速度 (例如，可以将子列表的排序和合并操作并行执行)。
    *   **不适合对内存空间要求非常苛刻的场景，因为归并排序需要额外的 O(n) 辅助空间。**

*   **代码示例 (C++, Java, Python):**

    **C++:**

    ```c++
    #include <iostream>
    #include <vector>
    #include <algorithm> // std::copy

    // 合并两个有序子数组
    void merge(std::vector<int>& arr, int left, int mid, int right) {
        int n1 = mid - left + 1;
        int n2 = right - mid;

        // 创建临时数组
        std::vector<int> L(n1), R(n2);

        // 复制数据到临时数组 L[] 和 R[]
        for (int i = 0; i < n1; ++i)
            L[i] = arr[left + i];
        for (int j = 0; j < n2; ++j)
            R[j] = arr[mid + 1 + j];

        // 合并临时数组到 arr[left...right]
        int i = 0, j = 0, k = left;
        while (i < n1 && j < n2) {
            if (L[i] <= R[j]) {
                arr[k] = L[i];
                ++i;
            } else {
                arr[k] = R[j];
                ++j;
            }
            ++k;
        }

        // 复制 L[] 中剩余的元素
        while (i < n1) {
            arr[k] = L[i];
            ++i;
            ++k;
        }

        // 复制 R[] 中剩余的元素
        while (j < n2) {
            arr[k] = R[j];
            ++j;
            ++k;
        }
    }

    // 归并排序
    void mergeSort(std::vector<int>& arr, int left, int right) {
        if (left < right) {
            int mid = left + (right - left) / 2; // 计算中间索引

            // 递归排序左半部分和右半部分
            mergeSort(arr, left, mid);
            mergeSort(arr, mid + 1, right);

            // 合并已排序的两半部分
            merge(arr, left, mid, right);
        }
    }

    int main() {
        std::vector<int> numbers = {64, 34, 25, 12, 22, 11, 90};
        mergeSort(numbers, 0, numbers.size() - 1);
        std::cout << "排序后的数组: ";
        for (int number : numbers) {
            std::cout << number << " ";
        }
        std::cout << std::endl;
        return 0;
    }
    ```

    **Java:**

    ```java
    public class MergeSort {
        // 合并两个有序子数组
        public static void merge(int[] arr, int left, int mid, int right) {
            int n1 = mid - left + 1;
            int n2 = right - mid;

            // 创建临时数组
            int[] L = new int[n1];
            int[] R = new int[n2];

            // 复制数据到临时数组 L[] 和 R[]
            for (int i = 0; i < n1; ++i)
                L[i] = arr[left + i];
            for (int j = 0; j < n2; ++j)
                R[j] = arr[mid + 1 + j];

            // 合并临时数组到 arr[left...right]
            int i = 0, j = 0, k = left;
            while (i < n1 && j < n2) {
                if (L[i] <= R[j]) {
                    arr[k] = L[i];
                    ++i;
                } else {
                    arr[k] = R[j];
                    ++j;
                }
                ++k;
            }

            // 复制 L[] 中剩余的元素
            while (i < n1) {
                arr[k] = L[i];
                ++i;
                ++k;
            }

            // 复制 R[] 中剩余的元素
            while (j < n2) {
                arr[k] = R[j];
                ++j;
                ++k;
            }
        }

        // 归并排序
        public static void mergeSort(int[] arr, int left, int right) {
            if (left < right) {
                int mid = left + (right - left) / 2; // 计算中间索引

                // 递归排序左半部分和右半部分
                mergeSort(arr, left, mid);
                mergeSort(arr, mid + 1, right);

                // 合并已排序的两半部分
                merge(arr, left, mid, right);
            }
        }

        public static void main(String[] args) {
            int[] numbers = {64, 34, 25, 12, 22, 11, 90};
            mergeSort(numbers, 0, numbers.length - 1);
            System.out.print("排序后的数组: ");
            for (int number : numbers) {
                System.out.print(number + " ");
            }
            System.out.println();
        }
    }
    ```

    **Python:**

    ```python
    def merge_sort(arr):
        if len(arr) <= 1: # 递归终止条件
            return arr

        mid = len(arr) // 2 # 计算中间索引
        left_half = arr[:mid]
        right_half = arr[mid:]

        # 递归排序左右两半部分
        left_half = merge_sort(left_half)
        right_half = merge_sort(right_half)

        # 合并已排序的两半部分
        return merge(left_half, right_half)

    # 合并两个有序列表
    def merge(left, right):
        merged = []
        i = j = 0
        while i < len(left) and j < len(right):
            if left[i] <= right[j]:
                merged.append(left[i])
                i += 1
            else:
                merged.append(right[j])
                j += 1

        # 添加剩余元素
        merged.extend(left[i:])
        merged.extend(right[j:])
        return merged

    numbers = [64, 34, 25, 12, 22, 11, 90]
    sorted_numbers = merge_sort(numbers)
    print("排序后的数组:", sorted_numbers)
    ```

---

#### 5. 快速排序 (Quick Sort)

**概念：分而治之的思想，选择一个基准值 (Pivot)，将列表划分为两部分，小于基准值的放左边，大于基准值的放右边，递归排序左右两部分**

**快速排序 (Quick Sort)**  也是一种基于 **分而治之 (Divide and Conquer)**  思想的高效排序算法，被广泛应用于实际中，例如，C++ 标准库的 `std::sort`  和 Java 的 `Arrays.sort`  在很多情况下都使用了快速排序 (或其变种)。  快速排序的核心思想是：  **选择一个元素作为基准值 (Pivot)**，然后 **将列表划分为两个子列表**：  **小于基准值的元素**  放到 **左边**，**大于基准值的元素**  放到 **右边**。  **基准值**  放到 **中间** (作为分隔)。  然后 **递归地对左右两个子列表进行快速排序**，直到子列表为空或只包含一个元素，排序完成。

*   **算法步骤 (升序排序):**

    1.  **选择基准值 (Pivot):**  从列表中 **选择一个元素**  作为基准值 (Pivot)。  常见的基准值选择策略有：
        *   **选择第一个元素。**
        *   **选择最后一个元素。**
        *   **选择中间元素。**
        *   **随机选择一个元素。**
        *   **三数取中 (Median-of-Three):**  从列表的第一个、中间和最后一个元素中选择中位数作为基准值，可以一定程度上提高算法性能，避免最坏情况。

    2.  **划分 (Partition):**  **重新排列列表**，使得：
        *   **所有小于基准值的元素**  都移动到 **基准值左边**。
        *   **所有大于基准值的元素**  都移动到 **基准值右边**。
        *   **基准值**  位于划分后的 **中间位置**。
        *   **划分过程：**  通常使用 **双指针法**  或 **单指针法**  进行划分。  双指针法 (例如，Lomuto 分区方案、Hoare 分区方案)  较为常用。

    3.  **递归排序子列表：**  **递归地**  对 **基准值左边的子列表**  和 **基准值右边的子列表**  进行快速排序。
    4.  **合并 (隐含)：**  快速排序是原地排序算法，不需要显式的合并操作。  当递归调用结束时，整个列表自然就变成有序的了。

*   **动画演示 (快速排序过程):**

*   **特性：**

    *   **高效快速：**  快速排序在平均情况下非常高效，平均时间复杂度为 **O(n log n)**。  通常比归并排序的常数因子更小，因此在实际应用中，快速排序往往比归并排序更快。
    *   **原地排序 (In-place Sort) (某些实现):**  使用原地划分算法 (例如，Lomuto 分区方案) 的快速排序是原地排序，只需要常数级别的辅助空间。  非原地划分算法 (需要额外数组来存储划分结果)  的快速排序是非原地排序。
    *   **不稳定排序 (Unstable Sort):**  快速排序在划分过程中可能会改变相等元素的相对顺序，因此是不稳定的排序算法。
    *   **最坏情况性能：**  快速排序在 **最坏情况下**  时间复杂度会退化为 **O(n^2)**  (例如，当每次选择的基准值都是列表的最小值或最大值，导致划分不均匀，递归深度增加)。  为了避免最坏情况，可以采用 **随机选择基准值**  或 **三数取中**  等策略来优化基准值的选择。

*   **适用场景：**

    *   **大多数通用排序场景：**  快速排序以其平均 O(n log n) 的高效性能，成为最常用的排序算法之一，适用于大多数通用排序场景。
    *   **内存排序：**  由于原地排序的特性，快速排序在内存排序中表现出色。
    *   **分而治之算法思想的典型应用：**  快速排序是学习分而治之算法思想的经典示例。
    *   **不适合对稳定性有严格要求的场景 (如果使用不稳定版本的快速排序)。**
    *   **对于非常小规模的数据，插入排序可能比快速排序更快，因为快速排序存在一定的递归开销。**

*   **代码示例 (C++, Java, Python):**

    **C++:**

    ```c++
    #include <iostream>
    #include <vector>
    #include <algorithm> // swap

    // 划分函数 (Lomuto 分区方案)
    int partition(std::vector<int>& arr, int low, int high) {
        int pivot = arr[high]; // 选择最后一个元素作为基准值
        int i = (low - 1); // 较小元素索引
        for (int j = low; j <= high - 1; ++j) {
            if (arr[j] < pivot) {
                ++i;
                std::swap(arr[i], arr[j]);
            }
        }
        std::swap(arr[i + 1], arr[high]);
        return (i + 1);
    }

    // 快速排序
    void quickSort(std::vector<int>& arr, int low, int high) {
        if (low < high) {
            // 划分
            int pi = partition(arr, low, high);

            // 递归排序划分的两部分
            quickSort(arr, low, pi - 1);
            quickSort(arr, pi + 1, high);
        }
    }

    int main() {
        std::vector<int> numbers = {64, 34, 25, 12, 22, 11, 90};
        quickSort(numbers, 0, numbers.size() - 1);
        std::cout << "排序后的数组: ";
        for (int number : numbers) {
            std::cout << number << " ";
        }
        std::cout << std::endl;
        return 0;
    }
    ```

    **Java:**

    ```java
    public class QuickSort {
        // 划分函数 (Lomuto 分区方案)
        public static int partition(int[] arr, int low, int high) {
            int pivot = arr[high]; // 选择最后一个元素作为基准值
            int i = (low - 1); // 较小元素索引
            for (int j = low; j <= high - 1; ++j) {
                if (arr[j] < pivot) {
                    ++i;
                    int temp = arr[i];
                    arr[i] = arr[j];
                    arr[j] = temp;
                }
            }
            int temp = arr[i + 1];
            arr[i + 1] = arr[high];
            arr[high] = temp;
            return (i + 1);
        }

        // 快速排序
        public static void quickSort(int[] arr, int low, int high) {
            if (low < high) {
                // 划分
                int pi = partition(arr, low, high);

                // 递归排序划分的两部分
                quickSort(arr, low, pi - 1);
                quickSort(arr, pi + 1, high);
            }
        }

        public static void main(String[] args) {
            int[] numbers = {64, 34, 25, 12, 22, 11, 90};
            quickSort(numbers, 0, numbers.length - 1);
            System.out.print("排序后的数组: ");
            for (int number : numbers) {
                System.out.print(number + " ");
            }
            System.out.println();
        }
    }
    ```

    **Python:**

    ```python
    def partition(arr, low, high):
        pivot = arr[high] # 选择最后一个元素作为基准值
        i = low - 1 # 较小元素索引
        for j in range(low, high):
            if arr[j] < pivot:
                i += 1
                arr[i], arr[j] = arr[j], arr[i]
        arr[i + 1], arr[high] = arr[high], arr[i + 1]
        return i + 1

    def quick_sort(arr, low, high):
        if low < high:
            # 划分
            pi = partition(arr, low, high)

            # 递归排序划分的两部分
            quick_sort(arr, low, pi - 1)
            quick_sort(arr, pi + 1, high)

    numbers = [64, 34, 25, 12, 22, 11, 90]
    quick_sort(numbers, 0, len(numbers) - 1)
    print("排序后的数组:", numbers)
    ```

*   **排序算法性能比较 (平均情况):**

    | 排序算法     | 时间复杂度 (平均) | 时间复杂度 (最坏) | 空间复杂度 | 稳定性   | 适用场景                                     |
    | ------------ | --------------- | --------------- | -------- | ------ | --------------------------------------------- |
    | 冒泡排序     | O(n^2)          | O(n^2)          | O(1)     | 稳定     | 小规模数据，教学示例，基本有序数据                 |
    | 选择排序     | O(n^2)          | O(n^2)          | O(1)     | 不稳定   | 小规模数据，交换操作代价高                       |
    | 插入排序     | O(n^2)          | O(n^2)          | O(1)     | 稳定     | 小规模数据，基本有序数据，在线排序                   |
    | 归并排序     | **O(n log n)**  | **O(n log n)**  | O(n)     | 稳定     | 大规模数据，外部排序，稳定排序要求，并行排序         |
    | 快速排序     | **O(n log n)**  | O(n^2)          | O(log n) | 不稳定   | 大多数通用排序场景，内存排序                     |


## 总结

排序算法是计算机科学的基础，掌握各种排序算法的原理、特性和适用场景，能够帮助你根据实际需求选择合适的排序算法，编写更高效、更强大的程序。  在实际应用中，通常会根据数据规模、性能要求、稳定性要求、空间限制等因素综合考虑，选择最合适的排序算法。 对于大规模通用排序任务，归并排序和快速排序是更优的选择。 对于小规模数据或基本有序的数据，插入排序可能更简单高效。