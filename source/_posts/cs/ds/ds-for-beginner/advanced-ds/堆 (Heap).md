---
title: 堆 (Heap)
date: 2025/1/01 12:44:25
index_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201338383.jpg
banner_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201338383.jpg
categories:
  - [计算机科学基础,数据结构,初学者入门,3.进阶数据结构]
tag:
  - 数据结构
  - 哈希表
published: true
---

## 堆 (Heap)

**概念：一种特殊的树形数据结构，满足堆属性**

**堆 (Heap)** 是一种特殊的 **树形数据结构**，但请注意，这里的 “堆” 和内存中的 “堆区 (Heap Memory)” 不是同一个概念，虽然都叫 “堆”，但在数据结构领域，堆特指这种特殊的树形结构。

堆最核心的特点是 **堆属性 (Heap Property)**，它决定了父节点和子节点之间的值关系。

![堆数据结构示意图](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201539209.png)

堆属性主要有两种类型，它们定义了两种不同的堆：

1. **最大堆 (Max Heap)：父节点的值总是大于或等于其子节点的值**

   在 **最大堆 (Max Heap)**  中，对于 **任何一个父节点**，它的值都 **大于或等于**  它的 **所有子节点的值**。  这意味着，**根节点 (Root Node)**  的值一定是整棵树中 **最大的**。

   最大堆常用于需要快速访问最大值的场景。

2.  **最小堆 (Min Heap)：父节点的值总是小于或等于其子节点的值**

    与最大堆相反，在 **最小堆 (Min Heap)**  中，对于 **任何一个父节点**，它的值都 **小于或等于**  它的 **所有子节点的值**。  这意味着，**根节点 (Root Node)**  的值一定是整棵树中 **最小的**。 

    最小堆常用于需要快速访问最小值的场景。

**总结堆属性的关键：**  堆是一种 **部分有序** 的数据结构，它只保证了父节点和子节点之间的关系，而 **兄弟节点之间没有明确的大小关系**，左右子树之间也没有特定的顺序。这种部分有序性使得堆在某些操作上非常高效。

## 二叉堆 (Binary Heap)

**二叉堆 (Binary Heap)：通常用完全二叉树实现**

**二叉堆 (Binary Heap)**  是最常用的一种堆的实现方式。  它是一种特殊的 **完全二叉树 (Complete Binary Tree)**，并满足堆属性（可以是最大堆或最小堆属性）。  由于完全二叉树的特性，二叉堆可以使用 **数组**  来高效地表示和存储，这使得二叉堆的实现非常简洁高效。

*   **完全二叉树特性：**  回顾一下完全二叉树的定义：除了最后一层外，其他层的节点数都达到最大值，并且最后一层的叶节点都连续地集中在最左边。这种结构非常规整，可以使用数组来顺序存储树的节点，而不会浪费空间。

*   **数组表示二叉堆：**  对于一个二叉堆，我们可以将其节点按层序遍历的顺序存储到一个数组中。  数组的索引与树节点之间的关系如下（假设数组索引从 1 开始，实际编程中索引从 0 开始更常见，这里为了概念更清晰先从 1 开始）：

    *   索引为 `i` 的节点：
        *   父节点索引：`i / 2`  (整数除法)
        *   左子节点索引：`2 * i`
        *   右子节点索引：`2 * i + 1`

**例如，对于一个最大堆，其数组表示可能如下 (索引从 1 开始)：**

| 索引 (Index) | 1   | 2   | 3   | 4   | 5   | 6   | 7   |
| ----------- | --- | --- | --- | --- | --- | --- | --- |
| 值 (Value)   | 16  | 14  | 10  | 8   | 7   | 9   | 3   |

**对应的树形结构：**

```
          16 (索引 1)
         /  \
       14 (索引 2)  10 (索引 3)
      /  \    /  \
     8 (索引 4)  7 (索引 5) 9 (索引 6) 3 (索引 7)
```

可以看到，数组的索引关系完美地映射了二叉堆的父子节点关系，通过简单的索引计算就可以找到节点的父节点和子节点。这使得二叉堆的插入、删除等操作可以通过数组的索引操作高效地实现。

**C++ 二叉堆-最小堆**：

```c++
#include <iostream>
#include <vector>
#include <algorithm> // 使用 swap 函数

// 使用模板类，使二叉堆可以存储不同类型的数据
template <typename T>
class BinaryHeap {
private:
    std::vector<T> heap; // 使用 vector 存储堆元素

    // 交换两个元素
    void swap(int i, int j) {
        std::swap(heap[i], heap[j]);
    }

    // 上浮操作，用于维护堆的性质（最小堆或最大堆）
    void heapifyUp(int i) {
        int parent = (i - 1) / 2; // 计算父节点索引
        // 如果当前节点比父节点小（最小堆），则交换
        if (parent >= 0 && heap[i] < heap[parent]) {
            swap(i, parent);
            heapifyUp(parent); // 递归上浮
        }
    }

    // 下沉操作，用于维护堆的性质（最小堆或最大堆）
    void heapifyDown(int i) {
        int left = 2 * i + 1; // 计算左子节点索引
        int right = 2 * i + 2; // 计算右子节点索引
        int smallest = i; // 假设当前节点是最小的

        // 找到左子节点、右子节点和当前节点中最小的
        if (left < heap.size() && heap[left] < heap[smallest]) {
            smallest = left;
        }
        if (right < heap.size() && heap[right] < heap[smallest]) {
            smallest = right;
        }

        // 如果最小的不是当前节点，则交换并递归下沉
        if (smallest != i) {
            swap(i, smallest);
            heapifyDown(smallest);
        }
    }

public:
    // 构造函数，初始化空堆
    BinaryHeap() {}

    // 插入元素
    void push(const T& value) {
        heap.push_back(value); // 将元素添加到堆的末尾
        heapifyUp(heap.size() - 1); // 上浮，维护堆的性质
    }

    // 删除堆顶元素
    T pop() {
        if (heap.empty()) {
            throw std::out_of_range("Heap is empty");
        }

        T top = heap[0]; // 获取堆顶元素
        heap[0] = heap.back(); // 将最后一个元素放到堆顶
        heap.pop_back(); // 删除最后一个元素
        heapifyDown(0); // 下沉，维护堆的性质
        return top;
    }

    // 获取堆顶元素
    T top() const {
        if (heap.empty()) {
            throw std::out_of_range("Heap is empty");
        }
        return heap[0];
    }

    // 判断堆是否为空
    bool empty() const {
        return heap.empty();
    }

    // 获取堆的大小
    size_t size() const {
        return heap.size();
    }

    // 打印堆中所有元素
    void print() const {
        for (const T& value : heap) {
            std::cout << value << " ";
        }
        std::cout << std::endl;
    }
};

int main() {
    BinaryHeap<int> minHeap; // 创建一个最小堆

    minHeap.push(5);
    minHeap.push(2);
    minHeap.push(8);
    minHeap.push(1);
    minHeap.push(9);

    std::cout << "Min Heap: ";
    minHeap.print(); // 输出：Min Heap: 1 2 8 5 9

    std::cout << "Top element: " << minHeap.top() << std::endl; // 输出：Top element: 1

    std::cout << "Popped element: " << minHeap.pop() << std::endl; // 输出：Popped element: 1

    std::cout << "Min Heap after pop: ";
    minHeap.print(); // 输出：Min Heap after pop: 2 5 8 9

    return 0;
}
```



## 优先级队列 (Priority Queue)：常用堆实现

**优先级队列 (Priority Queue)**  是一种特殊的队列。普通的队列遵循 FIFO 原则，元素出队顺序取决于入队顺序。而 **优先级队列**  则不同，**元素的出队顺序取决于元素的优先级**。优先级高的元素先出队，优先级低的元素后出队。如果优先级相同，则可以按照 FIFO 原则或自定义规则出队。

**堆 (Heap)  是实现优先级队列最常用的数据结构。**

具体来说：

*   **最大堆实现优先级队列：**可以使用 **最大堆**  来实现优先级队列，优先级 **高**  的元素值 **大**。  每次出队操作都取出 **根节点 (最大值)**，即优先级最高的元素。
*   **最小堆实现优先级队列：**可以使用 **最小堆**  来实现优先级队列，优先级 **高**  的元素值 **小**。  每次出队操作都取出 **根节点 (最小值)**，即优先级最高的元素 (值越小优先级越高)。  **更常见**  的是使用最小堆来实现优先级队列，因为通常用较小的数值来表示较高的优先级，例如任务优先级，优先级 1 比优先级 5 更高。

**优先级队列的基本操作 (基于堆实现)：**

1.  **入队 (Enqueue) / 插入 (Insert)：**  将一个带有优先级的元素插入到优先级队列中。  在堆的实现中，相当于将新元素添加到堆的末尾，然后 **上浮 (Heapify Up) **  调整堆，以维持堆属性。  时间复杂度通常为 **O(log n)**，n 为堆中元素数量。

2.  **出队 (Dequeue) / 取出 (Extract Max/Min)：**  从优先级队列中取出优先级最高的元素（最大堆取最大值，最小堆取最小值）。  在堆的实现中，相当于取出 **根节点**，然后将堆的 **最后一个元素**  移动到 **根节点**，再 **下沉 (Heapify Down) **  调整堆，以维持堆属性。  时间复杂度通常为 **O(log n)**。

3.  **查看队首 (Peek/Get Max/Min)：**  查看优先级最高的元素，但不取出。  在堆的实现中，直接返回 **根节点**  的值即可，时间复杂度为 **O(1)**。

4.  **判空 (IsEmpty)：**  检查优先级队列是否为空。  时间复杂度为 **O(1)**。

5.  **获取队列大小 (Size)：**  获取优先级队列中元素的个数。  时间复杂度为 **O(1)**。

**C++ 最小堆实现优先级队列**：

```c++
// 优先级队列类，使用二叉堆实现
template <typename T>
class PriorityQueue {
private:
    BinaryHeap<T> heap; // 使用二叉堆存储元素

public:
    // 插入元素
    void push(const T& value) {
        heap.push(value); // 调用二叉堆的 push 方法
    }

    // 删除优先级最高的元素
    T pop() {
        return heap.pop(); // 调用二叉堆的 pop 方法
    }

    // 获取优先级最高的元素
    T top() const {
        return heap.top(); // 调用二叉堆的 top 方法
    }

    // 判断优先级队列是否为空
    bool empty() const {
        return heap.empty(); // 调用二叉堆的 empty 方法
    }

    // 获取优先级队列的大小
    size_t size() const {
        return heap.size(); // 调用二叉堆的 size 方法
    }
};

int main() {
    PriorityQueue<int> pq; // 创建一个优先级队列

    pq.push(5);
    pq.push(2);
    pq.push(8);
    pq.push(1);
    pq.push(9);

    std::cout << "Priority Queue: ";
    while (!pq.empty()) {
        std::cout << pq.top() << " "; // 输出：1 2 5 8 9
        pq.pop();
    }
    std::cout << std::endl;

    return 0;
}
```



## 适用场景 (Use Cases)

堆和优先级队列在很多算法和应用中都有重要作用，尤其是在需要高效地管理和访问具有优先级的元素的场景。

1.  **优先级队列 (Priority Queue)：**  这是堆最直接的应用。  
    
    例如：
    
    *   **任务调度系统：**  操作系统中的任务调度器可以使用优先级队列来管理等待执行的任务，优先级高的任务优先执行。  例如，实时操作系统中，需要优先处理实时性要求高的任务。
    *   **事件驱动模拟：**  在事件驱动的模拟系统中，可以使用优先级队列来管理待处理的事件，事件的优先级通常是事件发生的时间，时间最早的事件优先处理。
    *   **Dijkstra 算法和 A\* 算法：**  图算法中的 Dijkstra 最短路径算法和 A\* 启发式搜索算法，都需要使用优先级队列来高效地选择下一个要处理的节点。
*   **哈夫曼编码 (Huffman Coding)：**  数据压缩算法哈夫曼编码中，可以使用优先级队列来构建哈夫曼树，频率较低的字符优先级较高。
    *   **中位数/顺序统计量查找：**  可以使用最大堆和最小堆结合来动态维护数据集合的中位数或任意顺序统计量。
    *   **在线算法：**  在数据流处理、在线算法中，优先级队列可以用于维护滑动窗口中的最大值/最小值，或Top-K 问题。
    
2. **堆排序 (Heap Sort)：**  堆排序是一种高效的排序算法，时间复杂度为 **O(n log n)** ，并且是 **原地排序 (In-place Sorting)** ，只需要常数级的额外空间。  堆排序的步骤如下：

   *   **建堆 (Build Heap)：**  将待排序的数组构建成一个堆（最大堆或最小堆）。  通常使用 **自底向上 (Bottom-up) 的堆化方法**  来高效建堆，时间复杂度为 **O(n)** 。
   *   **排序 (Sorting)：**  循环执行以下操作，直到堆为空：
       a.  取出堆顶元素（最大堆取出最大值，最小堆取出最小值），将其放到排序结果的末尾。
       b.  将堆的最后一个元素移动到堆顶，然后 **下沉 (Heapify Down)**  调整堆，以维持堆属性。

   **堆排序的优势：**  平均和最坏情况时间复杂度都为 O(n log n)，效率较高；原地排序，空间效率高；性能稳定，不像快速排序那样在最坏情况下可能退化到 O(n^2)。

3. **其他应用场景：**
   *   **海量数据处理：**  例如，在 1 亿个整数中找出最大的前 100 个数 (Top-K 问题)，可以使用最小堆来维护一个大小为 100 的小顶堆，遍历数据，将比堆顶元素大的元素替换堆顶元素并调整堆，遍历结束后，堆中的元素就是最大的前 100 个数。
   *   **系统内核：**  操作系统的内核中，堆也常用于内存管理、任务调度等方面。

## 总结

堆是一种非常有用的数据结构，尤其是二叉堆，以其高效的性能和简洁的实现，成为优先级队列的基石，并在排序算法、海量数据处理等领域有着广泛的应用。  理解堆的概念、类型、堆属性、以及优先级队列和堆排序的应用场景，能够帮助你更好地解决需要高效处理优先级数据的实际问题。