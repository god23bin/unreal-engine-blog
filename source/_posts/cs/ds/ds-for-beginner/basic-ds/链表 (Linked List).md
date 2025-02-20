---
title: 链表 (Linked List)
date: 2025/1/01 12:39:25
index_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201338383.jpg
banner_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201338383.jpg
categories:
  - [计算机科学基础,数据结构,初学者入门,2.基础数据结构]
tag:
  - 数据结构
  - 链表
published: true
---
## 链表

**概念：非连续内存空间，通过指针连接的节点序列**

如果说数组是一排紧密相连的柜子，那么 **链表 (Linked List)**  就像是一串珍珠项链。  每一颗珍珠（**节点 (Node)**）  本身包含了数据，并且还连接着下一颗珍珠（通过 **指针 (Pointer)**）。  与数组的连续内存空间不同，链表的节点可以分散在内存的各个角落，它们之间通过指针相互“记住”对方的位置，从而形成一个逻辑上的序列。

*   **节点 (Node)：** 链表的基本单元。每个节点通常包含两个部分：
    *   **数据域 (Data)：** 用于存储实际的数据，例如数字、文本、对象等。
    *   **指针域 (Pointer)：**  指向下一个节点（或上一个节点，对于双链表而言）的内存地址。这个指针就像一条线，将节点连接起来。
*   **非连续内存空间：**  链表的节点不需要存储在连续的内存空间中。 这意味着你可以更灵活地分配内存，不会像数组那样受限于必须找到一大块连续的空闲内存。

![单链表数据结构示意图](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201345601.png)

## 链表的类型 (Types)

链表主要有三种常见的类型，它们的主要区别在于指针的连接方式：

1. **单链表 (Singly Linked List)：**  这是最简单的链表类型。  每个节点只有一个指针，指向序列中的下一个节点。  就像一条单向的链条，只能从前往后遍历。

   ![单链表：每个节点指向下一个节点](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201345601.png)

2. **双向链表 (Doubly Linked List)：**  每个节点有两个指针，一个指向下一个节点，另一个指向上一个节点。  就像一条双向的链条，可以双向遍历，更方便地向前或向后访问节点。

   ![双链表：每个节点同时指向前一个和后一个节点](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201347647.png)

3. **循环链表 (Circular Linked List)：**  循环链表的最后一个节点指向第一个节点，形成一个环状结构。  可以是单循环或双循环。  想象一下，项链的末端又连接回了项链的开头。

## 链表的声明 (Conceptual Declaration)

链表本身是一种抽象的数据结构，实际编程中，我们通常需要自定义节点结构，并使用指针（或引用）来实现节点之间的连接。  这里用概念性的方式来描述链表的声明，而不是具体的代码语法：

```
// 节点结构定义 (概念)
Node:
    data:  // 存储数据
    next_pointer: // 指向下一个节点的指针 (单链表)
                 //  或
    previous_pointer: // 指向上一个节点的指针 (双链表)
    next_pointer:     // 指向下一个节点的指针 (双链表)
```

**头指针 (Head Pointer)：**  每个链表都需要一个特殊的指针，称为头指针。  头指针指向链表的第一个节点。  如果链表为空，则头指针通常为空（null 或 None）。  头指针是访问链表的入口，必须妥善保存。

## 链表的基本操作 (Operations)

链表在插入和删除节点方面具有比数组更高的效率，但在访问特定位置的节点时可能效率较低。  链表的主要操作包括：

1. **插入节点 (Insert):**  在链表的指定位置插入一个新的节点。  由于链表的非连续性，插入操作只需要修改指针的指向，而不需要像数组那样移动大量元素。

   *   **在头部插入 (Insert at Head)：**  新的节点成为链表的第一个节点，头指针指向新节点，新节点的 `next` 指针指向原来的头节点。
   *   **在尾部插入 (Insert at Tail)：**  遍历到链表的最后一个节点，将最后一个节点的 `next` 指针指向新节点。
   *   **在中间插入 (Insert in Middle)：**  找到要插入位置的前一个节点，修改前一个节点的 `next` 指针指向新节点，新节点的 `next` 指针指向原来前一个节点的 `next` 指针指向的节点。

2. **删除节点 (Delete):**  从链表中删除指定节点。  同样，删除操作也只需要修改指针指向，无需移动元素。

   *   **删除头部节点 (Delete Head)：**  将头指针指向原头节点的下一个节点，原头节点被移除。
   *   **删除尾部节点 (Delete Tail)：**  找到倒数第二个节点，将其 `next` 指针设为 null（或指向头节点，如果是循环链表），最后一个节点被移除。
   *   **删除中间节点 (Delete in Middle)：**  找到要删除节点的前一个节点，修改前一个节点的 `next` 指针，使其跳过要删除的节点，直接指向要删除节点的下一个节点。

3.  **遍历链表 (Traverse):**  访问链表中的每个节点，通常从头节点开始，沿着 `next` 指针逐个访问，直到遇到 `null` 指针（单链表或双链表）或回到头节点（循环链表）。

    ```
    current_node = head  // 从头节点开始
    while current_node is not None: // 当当前节点不为空时 (对于单链表和双链表)
    // while current_node is not head (对于循环链表，需要特殊判断循环结束条件)
        访问 current_node 的数据域
        current_node = current_node.next_pointer // 移动到下一个节点
    ```

4.  **查找节点 (Search):**  在链表中查找具有特定值的节点。  需要从头节点开始遍历，逐个比较节点的数据域，直到找到目标节点或遍历完整个链表。

## 代码示例

C++：

```c++
#include <iostream>

// 定义链表节点结构体
struct Node {
    int data; // 节点数据
    Node* next; // 指向下一个节点的指针

    // 构造函数，初始化节点
    Node(int val) : data(val), next(nullptr) {}
};

class LinkedList {
public:
    Node* head; // 链表头指针

    // 构造函数，初始化空链表
    LinkedList() : head(nullptr) {}

    // 头插法
    void insertAtHead(int data) {
        Node* newNode = new Node(data); // 创建新节点
        newNode->next = head; // 新节点的下一个指针指向当前头部
        head = newNode; // 更新头部指针
    }

    // 尾插法
    void insertAtTail(int data) {
        Node* newNode = new Node(data); // 创建新节点
        if (head == nullptr) { // 如果链表为空
            head = newNode; // 新节点成为头部
            return;
        }
        Node* current = head; // 从头部开始遍历
        while (current->next != nullptr) { // 找到尾部节点
            current = current->next;
        }
        current->next = newNode; // 尾部节点的下一个指针指向新节点
    }

    // 在指定位置插入节点
    void insertAt(int position, int data) {
        if (position == 0) { // 如果插入位置为头部
            insertAtHead(data);
            return;
        }
        Node* newNode = new Node(data); // 创建新节点
        Node* current = head; // 从头部开始遍历
        int count = 0;
        while (current != nullptr && count < position - 1) { // 找到插入位置的前一个节点
            current = current->next;
            count++;
        }
        if (current == nullptr) { // 如果插入位置超出链表长度
            std::cout << "Invalid position" << std::endl;
            delete newNode; // 释放新节点内存
            return;
        }
        newNode->next = current->next; // 新节点的下一个指针指向插入位置的后一个节点
        current->next = newNode; // 前一个节点的下一个指针指向新节点
    }

    // 删除头部节点
    void deleteAtHead() {
        if (head == nullptr) { // 如果链表为空
            return;
        }
        Node* temp = head; // 暂存头部节点
        head = head->next; // 更新头部指针
        delete temp; // 释放头部节点内存
    }

    // 删除尾部节点
    void deleteAtTail() {
        if (head == nullptr) { // 如果链表为空
            return;
        }
        if (head->next == nullptr) { // 如果链表只有一个节点
            delete head; // 释放头部节点内存
            head = nullptr; // 更新头部指针
            return;
        }
        Node* current = head; // 从头部开始遍历
        while (current->next->next != nullptr) { // 找到尾部节点的前一个节点
            current = current->next;
        }
        delete current->next; // 释放尾部节点内存
        current->next = nullptr; // 更新尾部指针
    }

    // 删除指定位置的节点
    void deleteAt(int position) {
        if (head == nullptr) { // 如果链表为空
            return;
        }
        if (position == 0) { // 如果删除位置为头部
            deleteAtHead();
            return;
        }
        Node* current = head; // 从头部开始遍历
        int count = 0;
        while (current != nullptr && count < position - 1) { // 找到删除位置的前一个节点
            current = current->next;
            count++;
        }
        if (current == nullptr || current->next == nullptr) { // 如果删除位置超出链表长度
            std::cout << "Invalid position" << std::endl;
            return;
        }
        Node* temp = current->next; // 暂存要删除的节点
        current->next = current->next->next; // 更新前一个节点的下一个指针
        delete temp; // 释放要删除的节点内存
    }

    // 遍历链表
    void traverse() {
        Node* current = head; // 从头部开始遍历
        while (current != nullptr) { // 遍历到尾部
            std::cout << current->data << " "; // 输出节点数据
            current = current->next; // 移动到下一个节点
        }
        std::cout << std::endl;
    }
};

int main() {
    LinkedList list;

    list.insertAtTail(1);
    list.insertAtTail(2);
    list.insertAtTail(3);

    std::cout << "链表元素：";
    list.traverse(); // 输出：1 2 3

    list.insertAtHead(0);

    std::cout << "链表元素：";
    list.traverse(); // 输出：0 1 2 3

    list.deleteAtTail();

    std::cout << "链表元素：";
    list.traverse(); // 输出：0 1 2

    list.deleteAtHead();

    std::cout << "链表元素：";
    list.traverse(); // 输出：1 2

    return 0;
}
```



## 适用场景 (Use Cases)

链表由于其动态性和高效的插入/删除操作，在以下场景中非常有用：

1.  **动态数据集合：**  当数据集合的大小在运行时动态变化，并且频繁进行插入和删除操作时，链表比数组更适合，因为链表可以灵活地扩展和收缩，而无需像数组那样预先分配固定大小的空间。
2.  **实现其他数据结构：**  链表可以用来实现更复杂的数据结构，例如栈、队列、哈希表（链地址法解决冲突）、图的邻接表表示等。
3.  **内存受限的场景：**  链表节点可以分散存储，更有效地利用碎片化的内存空间，在内存资源紧张的情况下更具优势。
4.  **不需要频繁按索引访问的场景：**  如果你的程序主要进行插入、删除和顺序访问操作，而很少需要像数组那样通过索引直接访问特定位置的元素，那么链表可能是一个更好的选择。
5.  **应用示例：**
    *   **浏览器历史记录：**  可以使用双链表来实现，方便前进和后退浏览。
    *   **音乐播放列表：**  可以使用循环链表来实现歌曲的循环播放。
    *   **操作系统的进程调度：**  可以使用链表来管理等待执行的进程队列。
    *   **哈希表的链地址法：**  使用链表来解决哈希冲突，将哈希到同一个位置的键值对链接成一个链表。

*   **优缺点总结：**

    | 特性         | 数组 (Array)                                  | 链表 (Linked List)                             |
    | ------------ | --------------------------------------------- | ----------------------------------------------- |
    | 内存空间     | 连续                                          | 非连续                                            |
    | 大小         | 通常固定 (静态数组)，或动态可调整 (动态数组)       | 动态可变                                        |
    | 访问元素     | **快速 (通过索引，O(1))**                      | 慢速 (需要遍历，平均 O(n))                        |
    | 插入/删除元素 | 慢速 (可能需要移动大量元素，平均 O(n))          | **快速 (仅需修改指针，O(1) - 插入/删除操作本身)** |
    | 适用场景     | 快速访问元素，大小相对固定，同类型数据集合     | 频繁插入/删除，动态数据集合，内存利用率要求高       |

## 总结

链表是另一种重要的基础数据结构，与数组互为补充。  它以非连续的节点和指针连接的方式，提供了动态性、高效插入删除的特性。  理解链表的不同类型、操作和适用场景，能够帮助你根据实际需求选择合适的数据结构，构建更灵活、高效的程序。在接下来的学习中，我们将继续探索更多的数据结构，例如栈、队列等等。