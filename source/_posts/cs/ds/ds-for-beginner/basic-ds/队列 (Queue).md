---
title: 队列 (Queue)
date: 2025/1/01 12:41:25
index_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201338383.jpg
banner_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201338383.jpg
categories:
  - [计算机科学基础,数据结构,初学者入门,2.基础数据结构]
tag:
  - 数据结构
  - 队列
published: true
---

## 队列 (Queue)

**概念：先进先出 (FIFO - First In First Out) 的数据结构**

想象一下，你在排队买东西。  先来排队的人，先买到东西，然后离开队伍，后来的人只能排在后面，依次轮到。  **队列 (Queue)**  这种数据结构就类似于排队，它遵循 **先进先出 (FIFO - First In First Out)** 的原则。  就像一个单端入口、单端出口的管道，你只能从队尾 (Rear/Back) 进入 (入队)，从队首 (Front) 出去 (出队)。

*   **先进先出 (FIFO)：** First In First Out。  最先进入队列的元素，将是第一个被取出来的元素。  反之，最后进入队列的元素，将是最后被取出来的元素。
*   **双端操作 (两端操作，但操作类型受限)：**  队列的操作在队列的两端进行：队尾 (Rear) 只负责入队（添加元素），队首 (Front) 只负责出队（移除元素）。  你不能直接访问队列中间的元素，必须按照排队的顺序进行处理。

![队列示意图](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201419949.png)

## 队列的类型 (Types)

队列根据其特性和实现方式，可以分为多种类型：

1. **普通队列 (Queue) / 单端队列 (Single-ended Queue)**

   这是最基本的队列形式，严格遵循 FIFO 原则。

   元素从队尾入队，从队首出队。

   通常简称 “队列” 时，指的就是这种普通队列。

2. **循环队列 (Circular Queue)**

   为了更有效地利用存储空间，尤其是在使用数组实现队列时，引入了循环队列。

   循环队列将队列的首尾相连，形成一个环状结构。

   当队尾指针到达数组末尾时，如果队首前面还有空闲空间，队尾指针可以“循环”到数组的头部，继续存放元素，避免了普通队列可能出现的“假溢出”问题（队列明明有空闲空间，却无法继续入队）。

3. **双端队列 (Deque - Double-ended Queue)** 

   双端队列是一种更灵活的队列，它允许在队列的**两端**进行入队和出队操作。

   也就是说，你可以从队首入队 (addFirst/offerFirst)，从队首出队 (removeFirst/pollFirst)，也可以从队尾入队 (addLast/offerLast)，从队尾出队 (removeLast/pollLast)。

   双端队列兼具队列和栈的特性，可以当作普通队列、栈，甚至双向队列来使用。

4. **优先级队列 (Priority Queue)** 

   优先级队列不是按照 FIFO 原则，而是按照元素的优先级进行出队。优先级高的元素先出队。

   优先级队列通常使用 **堆 (Heap)** 数据结构来实现，会在后续 “进阶数据结构” 部分介绍。

   在基础队列的学习阶段，可以先了解优先级队列的概念，知道它是一种特殊的队列即可。

## 队列的声明 (Declaration)

不同编程语言都提供了队列的实现，特别是双端队列 (Deque) 通常会被作为实现栈和队列的通用工具。

*   **Python:**

    Python 的标准库 `collections` 模块提供了 `deque` (双端队列)，它非常适合用作队列。  `deque` 支持高效的队首和队尾操作。

    ```python
    # 使用 collections.deque 实现队列
    from collections import deque

    # 声明一个双端队列，用作普通队列
    queue_deque = deque()
    ```

* **Java:**

  Java 提供了 `java.util.Queue` 接口，以及它的子接口 `java.util.Deque` (双端队列)。

  常用的实现类包括 `java.util.LinkedList` (实现了 `Queue` 和 `Deque` 接口) 和 `java.util.ArrayDeque` (实现了 `Deque` 接口，更高效的数组实现)。  

  通常推荐使用 `ArrayDeque` 或 `LinkedList` 作为队列的实现。

  ```java
  // 使用 LinkedList 实现队列 (实现了 Queue 接口和 Deque 接口)
  import java.util.LinkedList;
  java.util.Queue<Integer> queueLinked = new java.util.LinkedList<>();
  
  // 使用 ArrayDeque 实现队列 (实现了 Deque 接口，更高效)
  import java.util.ArrayDeque;
  java.util.Queue<Integer> queueArrayDeque = new java.util.ArrayDeque<>();
  
  // 或者直接使用 Deque 接口来声明，更灵活 (可以当作普通队列或双端队列使用)
  java.util.Deque<Integer> dequeQueue = new java.util.ArrayDeque<>(); // ArrayDeque 或 LinkedList
  ```

*   **C++:**

    C++ 标准库提供了 `<queue>` 头文件，其中 `std::queue` 是队列容器适配器 (默认基于 `std::deque` 实现)。  

    同时，`<deque>` 头文件提供了 `std::deque` 双端队列容器，也可以直接用作队列。  `std::list` 也可以作为 `std::queue` 的底层容器，或直接用作队列。
    
    ```c++
    #include <iostream>
    #include <queue>    // 队列容器适配器
#include <deque>    // 双端队列容器
    #include <list>     // 链表容器
    
    int main() {
    // 使用默认容器 deque 的队列
        std::queue<int> queueDefault;
    
    // 使用 list 作为底层容器的队列
        std::queue<int, std::list<int>> queueList;
    
        // 直接使用 deque 双端队列作为队列 (更灵活)
        std::deque<int> dequeQueue;
        return 0;
    }
    ```

## 队列的基本操作 (Operations)

队列的基本操作围绕着 FIFO 原则进行，主要操作包括：

1.  **入队 (Enqueue):**  将一个元素添加到队尾。  相当于排队时，新来的人站到队伍的末尾。

    *   **Python:** `queue.append(element)` (使用 `deque`)
    *   **Java:** `queue.offer(element)` 或 `queue.add(element)` (使用 `Queue` 接口实现类), `deque.offerLast(element)` 或 `deque.addLast(element)` (使用 `Deque` 接口实现类)
    *   **C++:** `queue.push(element)` (使用 `std::queue`), `deque.push_back(element)` 或 `deque.push_back(element)` (使用 `std::deque`)

    ```python
    from collections import deque
    queue = deque()
    queue.append(10) # 入队元素 10
    queue.append(20) # 入队元素 20
    queue.append(30) # 入队元素 30
    # 队列现在内容 (队首到队尾): [10, 20, 30]
    ```

2.  **出队 (Dequeue):**  从队首取出一个元素并删除。  相当于排在队伍最前面的人买完东西离开队伍。 **注意：出队操作通常会返回被出队的元素。**

    *   **Python:** `queue.popleft()` (使用 `deque`)
    *   **Java:** `queue.poll()` 或 `queue.remove()` (使用 `Queue` 接口实现类), `deque.pollFirst()` 或 `deque.removeFirst()` (使用 `Deque` 接口实现类)
    *   **C++:** `queue.pop()` (使用 `std::queue`), `deque.pop_front()` 或 `deque.pop_front()` (使用 `std::deque`)

    ```python
    from collections import deque
    queue = deque([10, 20, 30])
    front_element = queue.popleft() # 出队，取出队首元素 10
    print(front_element)       # 输出: 10
    # 队列现在内容: [20, 30]
    ```

3.  **查看队首 (Peek/Front):**  查看队首元素，但不取出。  相当于看看排在队伍最前面的人是谁，但不让他离开队伍。

    *   **Python:** `queue[0]` (使用 `deque`，索引 0 访问第一个元素),  更安全的方式是先判断队列是否为空再访问。
    *   **Java:** `queue.peek()` 或 `queue.element()` (使用 `Queue` 接口实现类), `deque.peekFirst()` 或 `deque.getFirst()` 或 `deque.peek()` (使用 `Deque` 接口实现类)
    *   **C++:** `queue.front()` (使用 `std::queue`), `deque.front()` 或 `deque.front()` (使用 `std::deque`)

    ```python
    from collections import deque
    queue = deque([10, 20, 30])
    front_element = queue[0] # 查看队首元素
    print(front_element)       # 输出: 10
    # 队列内容仍然是: [10, 20, 30]
    ```

4.  **查看队尾 (Rear/Back/Last):**  查看队尾元素，但不取出。  双端队列 `Deque` 支持查看队尾元素。  普通队列通常不直接提供查看队尾的操作，因为队尾主要用于入队。

    *   **Python:** `queue[-1]` (使用 `deque`，索引 -1 访问最后一个元素),  更安全的方式是先判断队列是否为空再访问。
    *   **Java:** `deque.peekLast()` 或 `deque.getLast()` 或 `deque.peekLast()` (使用 `Deque` 接口实现类)
    *   **C++:** `deque.back()` 或 `deque.back()` (使用 `std::deque`)

    ```python
    from collections import deque
    queue = deque([10, 20, 30])
    rear_element = queue[-1] # 查看队尾元素
    print(rear_element)        # 输出: 30
    # 队列内容仍然是: [10, 20, 30]
    ```

5.  **判空 (IsEmpty):**  检查队列是否为空。

    *   **Python:** `len(queue) == 0` (使用 `deque`)
    *   **Java:** `queue.isEmpty()` (使用 `Queue` 接口实现类或 `Deque` 接口实现类)
    *   **C++:** `queue.empty()` (使用 `std::queue` 或 `std::deque`)

    ```python
    from collections import deque
    queue = deque()
    is_empty = len(queue) == 0
    print(is_empty)          # 输出: True
    queue.append(10)
    is_empty = len(queue) == 0
    print(is_empty)          # 输出: False
    ```

6.  **获取队列大小 (Size):**  获取队列中元素的个数。

    *   **Python:** `len(queue)` (使用 `deque`)
    *   **Java:** `queue.size()` (使用 `Queue` 接口实现类或 `Deque` 接口实现类)
    *   **C++:** `queue.size()` (使用 `std::queue` 或 `std::deque`)

    ```python
    from collections import deque
    queue = deque([10, 20, 30])
    queue_size = len(queue)
    print(queue_size)        # 输出: 3
    ```

## 适用场景 (Use Cases) 及示例

队列的 FIFO 特性使其在很多需要按照 **到达顺序处理任务** 的场景中非常有用。

1. **任务调度 (Task Scheduling) / 作业调度 (Job Scheduling)：**  

   操作系统使用队列来管理等待执行的任务或进程。

   按照任务到达的先后顺序，将任务放入队列，调度器从队首取出任务执行，保证公平性。

   ```plaintext
   +---------------------+
   | CPU (执行中)        |
   +---------------------+
            |
            |
            ▼
   +---------------------+
   | 任务 1（执行中）     |
   +---------------------+
            |
            |
            ▼
   +---------------------+
   | 任务 2（等待中）     |
   +---------------------+
            |
            |
            ▼
   +---------------------+
   | 任务 3（等待中）     |
   +---------------------+
            |
            |
            ▼
   +---------------------+
   | 任务 4（等待中）     |
   +---------------------+
            |
            |
            ▼
   +---------------------+
   | 任务 5（等待中）     |
   +---------------------+
            |
            |
            ▼
   +---------------------+
   | 任务 n（等待中）     |
   +---------------------+
   ```

   **示例 (简化的任务调度模拟):**

   ```python
   import time
   from collections import deque
   
   task_queue = deque() # 任务队列
   
   def add_task(task_name):
       task_queue.append(task_name)
       print(f"任务 '{task_name}' 加入队列")
   
   def execute_task():
       if task_queue:
           task_name = task_queue.popleft()
           print(f"执行任务 '{task_name}' ...")
           time.sleep(1) # 模拟任务执行时间
           print(f"任务 '{task_name}' 执行完成")
       else:
           print("任务队列为空，等待新任务...")
   
   add_task("任务 A")
   add_task("任务 B")
   add_task("任务 C")
   
   while task_queue: # 当队列不为空时，持续执行任务
       execute_task()
   
   print("所有任务执行完毕")
   
   # 输出 (类似):
   # 任务 '任务 A' 加入队列
   # 任务 '任务 B' 加入队列
   # 任务 '任务 C' 加入队列
   # 执行任务 '任务 A' ...
   # 任务 '任务 A' 执行完成
   # 执行任务 '任务 B' ...
   # 任务 '任务 B' 执行完成
   # 执行任务 '任务 C' ...
   # 任务 '任务 C' 执行完成
   # 所有任务执行完毕
   ```

2. **消息队列 (Message Queue)** 

   在分布式系统和多线程编程中，消息队列用于异步地传递消息。

   生产者将消息放入队列，消费者从队列中取出消息进行处理。

   消息队列可以解耦生产者和消费者，提高系统的可靠性和可伸缩性。

   ![消息队列示意图，生产者和消费者通过队列传递消息](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201452413.png)

   **应用场景 (消息队列的例子):**

   *   **用户注册：**  用户注册成功后，将注册消息放入消息队列，后续的邮件发送、短信通知等操作由消费者异步处理，无需用户等待。
   *   **订单处理：**  用户下单后，将订单消息放入消息队列，库存服务、支付服务、物流服务等消费者从队列中获取订单消息进行后续处理。

3. **广度优先搜索 (BFS - Breadth-First Search)**  

   图算法中的广度优先搜索使用队列来辅助遍历图的节点。

   BFS 按照层级顺序访问节点，先访问离起点近的节点，再访问离起点远的节点，需要使用队列来保存待访问的邻居节点。

   ![二叉树](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201459636.jpeg)

   <center>广度优先搜索队列示意图，展示 BFS 算法中队列的使用</center>

   **BFS 算法基本步骤 (使用队列):**

   ```c++
   #include <iostream>
   #include <queue>
   #include <vector>
   
   // 定义二叉树节点结构
   struct TreeNode {
       int val;
       TreeNode *left;
       TreeNode *right;
       TreeNode(int x) : val(x), left(NULL), right(NULL) {}
   };
   
   // 广度优先搜索函数
   std::vector<int> bfs(TreeNode* root) {
       std::vector<int> result;
       if (root == nullptr) {
           return result; // 如果根节点为空，直接返回空的结果
       }
   
       std::queue<TreeNode*> q; // 创建一个队列用于存储节点
       q.push(root); // 将根节点入队
   
       while (!q.empty()) { // 当队列不为空时
           TreeNode* node = q.front(); // 取出队列头部的节点
           q.pop(); // 将该节点从队列中移除
   
           result.push_back(node->val); // 将节点的值加入 result
   
           if (node->left != nullptr) {
               q.push(node->left); // 如果左子节点不为空，将其入队
           }
   
           if (node->right != nullptr) {
               q.push(node->right); // 如果右子节点不为空，将其入队
           }
       }
   
       return result; // 返回存储了广度优先搜索结果的 result
   }
   
   int main() {
       // 构建示例二叉树
       TreeNode* root = new TreeNode(0);
       root->left = new TreeNode(1);
       root->right = new TreeNode(2);
       root->left->left = new TreeNode(3);
       root->left->right = new TreeNode(4);
       root->right->right = new TreeNode(5);
   
       std::vector<int> result = bfs(root);
       std::cout << "广度优先搜索结果: ";
       for (int val : result) {
           std::cout << val << " ";
       }
       std::cout << std::endl;
   
       // 释放内存，避免内存泄漏
       delete root->left->left;
       delete root->left->right;
       delete root->right->right;
       delete root->left;
       delete root->right;
       delete root;
   
       return 0;
   }
   ```

   

4. **其他应用场景：**
   *   **打印机队列：**  打印任务按照提交顺序排队打印。
   *   **客服呼叫中心：**  客服请求按照到达顺序排队等待客服人员处理。
   *   **网络数据包处理：**  路由器使用队列来缓冲和转发网络数据包。
   *   **多线程共享资源访问控制：**  可以使用队列作为公平锁或请求队列，控制多线程对共享资源的访问顺序。

## 总结

队列是一种基础且实用的数据结构，其核心思想是 **先进先出 (FIFO)** 。理解队列的概念、类型、操作和应用场景，对于理解任务调度、消息传递、图算法等重要概念至关重要。  队列在计算机系统中扮演着重要的角色，能够帮助我们构建更公平、有序、高效的系统。