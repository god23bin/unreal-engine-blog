---
title: 栈 (Stack)
date: 2025/1/01 12:40:25
index_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201338383.jpg
banner_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201338383.jpg
categories:
  - [计算机科学基础,数据结构,初学者入门,2.基础数据结构]
tag:
  - 数据结构
  - 栈
published: true
---
## 栈 (Stack)

**概念：后进先出 (LIFO - Last In First Out) 的数据结构**

想象一下，你叠放一摞盘子。  你总是从最上面拿走盘子，最后放上去的盘子总是最先被拿走。  **栈 (Stack)** 这种数据结构就类似于叠盘子，它遵循 **后进先出 (LIFO - Last In First Out)** 的原则。  就像一个桶或者一个单端开口的管道，你只能从顶端放入 (压栈) 和取出 (弹栈) 元素。

*   **后进先出 (LIFO)：**  Last In First Out。  最后放入栈的元素，将是第一个被取出来的元素。  反之，最先放入栈的元素，将是最后被取出来的元素。
*   **单端操作：**  栈的操作只在栈顶 (Top) 进行。  你不能直接访问栈中间或底部的元素，必须先将上面的元素取出才能访问下面的。

![栈数据结构示意图](https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201403417.png)

## **栈的类型 (Types)**

从概念上讲，栈主要关注的是 **LIFO 的操作原则**。  在具体实现上，栈可以使用不同的底层数据结构来实现，例如：

  *   **顺序栈 (Array-based Stack)：**  使用数组作为底层存储结构来实现栈。  由于数组的连续内存特性，顺序栈的实现相对简单，访问速度快，但容量固定或扩展需要一定开销。
  *   **链式栈 (Linked-list Stack)：**  使用链表作为底层存储结构来实现栈。  链式栈的优点是容量可以动态扩展，插入和删除操作高效，但访问速度相对顺序栈稍慢，并且需要额外的指针存储空间。

尽管实现方式不同，但它们都遵循栈的 LIFO 原则，对外提供的操作接口（压栈、弹栈、查看栈顶等）是相同的。

因此，在概念上，我们通常不严格区分栈的类型，除非特别强调实现细节。

## 栈的声明 (Declaration)

不同编程语言中，栈的实现方式和声明语法略有不同。很多语言的标准库中都提供了栈的实现。

*   **Python:**

    Python 的标准库中没有直接名为 "Stack" 的类，但可以使用 `list`  列表来模拟栈的操作，因为列表提供了 `append()` (压栈) 和 `pop()` (弹栈) 方法，可以方便地实现 LIFO 原则。  或者，可以使用 `collections.deque` 双端队列，它也支持高效的栈操作。

    ```python
    # 使用 list 模拟栈
    stack_list = []

    # 使用 collections.deque 实现栈 (更高效，尤其在频繁操作栈顶时)
    from collections import deque
    stack_deque = deque()
    ```

*   **Java:**

    Java 提供了 `java.util.Stack` 类来实现栈。  但官方推荐使用 `Deque` 接口的实现类，例如 `ArrayDeque` 或 `LinkedList` 来作为栈使用，因为 `Stack` 类是遗留类，效率和设计上存在一些问题。  通常使用 `ArrayDeque` 作为栈的实现。

    ```java
    // 使用 java.util.Stack 类 (不推荐)
    java.util.Stack<Integer> stackLegacy = new java.util.Stack<>();

    // 使用 ArrayDeque 作为栈 (推荐)
    import java.util.ArrayDeque;
    java.util.Deque<Integer> stackDeque = new java.util.ArrayDeque<>();

    // 或者使用 LinkedList 作为栈 (Deque 接口的实现)
    import java.util.LinkedList;
    java.util.Deque<Integer> stackLinked = new java.util.LinkedList<>();
    ```

*   **C++:**

    C++ 标准库提供了 `<stack>`  头文件，其中 `std::stack`  是栈的容器适配器。  默认情况下，`std::stack`  使用 `std::deque`  作为底层容器实现，也可以指定 `std::vector`  或 `std::list`  作为底层容器。

    ```c++
    #include <iostream>
    #include <stack> // 栈容器

    int main() {
        // 使用默认容器 deque 的栈
        std::stack<int> stackDefault;

        // 使用 vector 作为底层容器的栈
        std::stack<int, std::vector<int>> stackVector;

        // 使用 list 作为底层容器的栈
        std::stack<int, std::list<int>> stackList;
        return 0;
    }
    ```

## 栈的基本操作 (Operations)

栈的基本操作非常简洁，主要包括以下几种：

1.  **压栈 (Push):**  将一个元素放入栈顶。  相当于把一个新盘子放到盘子堆的最上面。

    *   **Python:**  `stack.append(element)` (使用 `list` 模拟栈), `stack.append(element)` (使用 `deque`)
    *   **Java:**  `stack.push(element)` (使用 `Stack` 类), `stack.push(element)` 或 `stack.addLast(element)` (使用 `Deque` 接口实现类)
    *   **C++:**  `stack.push(element)`

    ```python
    stack = [] # 或者 stack = deque()
    stack.append(10) # 压栈元素 10
    stack.append(20) # 压栈元素 20
    stack.append(30) # 压栈元素 30
    # 栈现在内容 (从栈底到栈顶): [10, 20, 30]
    ```

2.  **弹栈 (Pop):**  从栈顶取出一个元素并删除。  相当于从盘子堆的最上面拿走一个盘子。  **注意：弹栈操作通常会返回被弹出的元素。**

    *   **Python:**  `stack.pop()` (使用 `list` 或 `deque`)
    *   **Java:**  `stack.pop()` (使用 `Stack` 类), `stack.pop()` 或 `stack.removeLast()` (使用 `Deque` 接口实现类)
    *   **C++:**  `stack.pop()`

    ```python
    stack = [10, 20, 30] # 或者 stack = deque([10, 20, 30])
    top_element = stack.pop() # 弹栈，取出栈顶元素 30
    print(top_element)      # 输出: 30
    # 栈现在内容: [10, 20]
    ```

3.  **查看栈顶 (Peek/Top):**  查看栈顶元素，但不取出。  相当于看一下盘子堆最上面的盘子是什么，但不把它拿走。

    *   **Python:**  `stack[-1]` (使用 `list` 模拟栈，索引 -1 访问最后一个元素), `stack[-1]` (使用 `deque`，索引 -1 也访问最后一个元素),  或者更安全的方式是先判断栈是否为空再访问。
    *   **Java:**  `stack.peek()` (使用 `Stack` 类), `stack.peek()` 或 `stack.getLast()` 或 `stack.peekLast()` (使用 `Deque` 接口实现类)
    *   **C++:**  `stack.top()`

    ```python
    stack = [10, 20, 30] # 或者 stack = deque([10, 20, 30])
    top_element = stack[-1] # 查看栈顶元素
    print(top_element)      # 输出: 30
    # 栈内容仍然是: [10, 20, 30]
    ```

4.  **判空 (IsEmpty):**  检查栈是否为空。

    *   **Python:**  `len(stack) == 0` (使用 `list` 或 `deque`)
    *   **Java:**  `stack.isEmpty()` (使用 `Stack` 类或 `Deque` 接口实现类)
    *   **C++:**  `stack.empty()`

    ```python
    stack = [] # 或者 stack = deque()
    is_empty = len(stack) == 0
    print(is_empty)         # 输出: True
    stack.append(10)
    is_empty = len(stack) == 0
    print(is_empty)         # 输出: False
    ```

5.  **获取栈大小 (Size):**  获取栈中元素的个数。

    *   **Python:**  `len(stack)` (使用 `list` 或 `deque`)
    *   **Java:**  `stack.size()` (使用 `Stack` 类或 `Deque` 接口实现类)
    *   **C++:**  `stack.size()`

    ```python
    stack = [10, 20, 30] # 或者 stack = deque([10, 20, 30])
    stack_size = len(stack)
    print(stack_size)       # 输出: 3
    ```

## 代码示例

C++顺序栈：

```c++
#include <iostream>

// 定义顺序栈结构体
template <typename T> // 使用模板，使栈可以存储不同类型的数据
class SeqStack {
private:
    T* data; // 存储栈元素的数组
    int top; // 栈顶指针，指向栈顶元素的下一个位置
    int capacity; // 栈的容量

public:
    // 构造函数，初始化栈
    SeqStack(int size) : capacity(size), top(0) {
        data = new T[capacity]; // 分配存储空间
    }

    // 析构函数，释放栈的存储空间
    ~SeqStack() {
        delete[] data;
    }

    // 判断栈是否为空
    bool isEmpty() {
        return top == 0;
    }

    // 判断栈是否已满
    bool isFull() {
        return top == capacity;
    }

    // 入栈操作
    void push(const T& value) {
        if (isFull()) {
            std::cout << "Stack is full, cannot push." << std::endl;
            return;
        }
        data[top++] = value; // 将元素放入栈顶，并更新栈顶指针
    }

    // 出栈操作
    T pop() {
        if (isEmpty()) {
            std::cout << "Stack is empty, cannot pop." << std::endl;
            return T{}; // 返回默认值
        }
        return data[--top]; // 先更新栈顶指针，然后返回栈顶元素
    }

    // 获取栈顶元素
    T peek() {
        if (isEmpty()) {
            std::cout << "Stack is empty, cannot peek." << std::endl;
            return T{}; // 返回默认值
        }
        return data[top - 1]; // 返回栈顶元素，但不更新栈顶指针
    }

    // 打印栈中所有元素
    void printStack() {
        if (isEmpty()) {
            std::cout << "Stack is empty." << std::endl;
            return;
        }
        std::cout << "Stack elements: ";
        for (int i = 0; i < top; i++) {
            std::cout << data[i] << " ";
        }
        std::cout << std::endl;
    }
};

int main() {
    SeqStack<int> stack(5); // 创建一个容量为 5 的整型栈

    stack.push(1);
    stack.push(2);
    stack.push(3);

    stack.printStack(); // 输出：Stack elements: 1 2 3

    std::cout << "Top element: " << stack.peek() << std::endl; // 输出：Top element: 3

    std::cout << "Popped element: " << stack.pop() << std::endl; // 输出：Popped element: 3

    stack.printStack(); // 输出：Stack elements: 1 2

    return 0;
}
```

C++ 链式栈：

```c++
#include <iostream>

// 定义链式栈节点结构体
template <typename T> // 使用模板，使栈可以存储不同类型的数据
struct Node {
    T data; // 节点数据
    Node<T>* next; // 指向下一个节点的指针

    // 构造函数，初始化节点
    Node(const T& value) : data(value), next(nullptr) {}
};

template <typename T>
class LinkedStack {
private:
    Node<T>* top; // 栈顶指针

public:
    // 构造函数，初始化空栈
    LinkedStack() : top(nullptr) {}

    // 析构函数，释放栈的存储空间
    ~LinkedStack() {
        while (!isEmpty()) {
            pop();
        }
    }

    // 判断栈是否为空
    bool isEmpty() {
        return top == nullptr;
    }

    // 入栈操作
    void push(const T& value) {
        Node<T>* newNode = new Node<T>(value); // 创建新节点
        newNode->next = top; // 新节点的下一个指针指向当前栈顶
        top = newNode; // 更新栈顶指针
    }

    // 出栈操作
    T pop() {
        if (isEmpty()) {
            std::cout << "Stack is empty, cannot pop." << std::endl;
            return T{}; // 返回默认值
        }
        T value = top->data; // 获取栈顶元素
        Node<T>* temp = top; // 暂存栈顶节点
        top = top->next; // 更新栈顶指针
        delete temp; // 释放栈顶节点内存
        return value; // 返回弹出的元素
    }

    // 获取栈顶元素
    T peek() {
        if (isEmpty()) {
            std::cout << "Stack is empty, cannot peek." << std::endl;
            return T{}; // 返回默认值
        }
        return top->data; // 返回栈顶元素
    }

    // 打印栈中所有元素
    void printStack() {
        if (isEmpty()) {
            std::cout << "Stack is empty." << std::endl;
            return;
        }
        std::cout << "Stack elements: ";
        Node<T>* current = top; // 从栈顶开始遍历
        while (current != nullptr) {
            std::cout << current->data << " ";
            current = current->next;
        }
        std::cout << std::endl;
    }
};

int main() {
    LinkedStack<int> stack; // 创建一个整型链式栈

    stack.push(1);
    stack.push(2);
    stack.push(3);

    stack.printStack(); // 输出：Stack elements: 3 2 1

    std::cout << "Top element: " << stack.peek() << std::endl; // 输出：Top element: 3

    std::cout << "Popped element: " << stack.pop() << std::endl; // 输出：Popped element: 3

    stack.printStack(); // 输出：Stack elements: 2 1

    return 0;
}
```



Python 顺序栈：

```python
class SeqStack:
    def __init__(self, size):
        self.data = [None] * size  # 使用列表存储栈元素，初始化为空列表
        self.top = -1  # 栈顶指针，初始值为 -1，表示栈为空
        self.capacity = size  # 栈的容量

    def is_empty(self):
        return self.top == -1  # 判断栈是否为空

    def is_full(self):
        return self.top == self.capacity - 1  # 判断栈是否已满

    def push(self, value):
        if self.is_full():
            print("Stack is full, cannot push.")
            return
        self.top += 1  # 栈顶指针加 1
        self.data[self.top] = value  # 将元素放入栈顶

    def pop(self):
        if self.is_empty():
            print("Stack is empty, cannot pop.")
            return None  # 返回 None 表示栈为空
        value = self.data[self.top]  # 获取栈顶元素
        self.top -= 1  # 栈顶指针减 1
        return value  # 返回弹出的元素

    def peek(self):
        if self.is_empty():
            print("Stack is empty, cannot peek.")
            return None  # 返回 None 表示栈为空
        return self.data[self.top]  # 返回栈顶元素，但不弹出

    def print_stack(self):
        if self.is_empty():
            print("Stack is empty.")
            return
        print("Stack elements:", end=" ")
        for i in range(self.top + 1):  # 遍历栈中所有元素
            print(self.data[i], end=" ")
        print()


if __name__ == "__main__":
    stack = SeqStack(5)  # 创建一个容量为 5 的栈

    stack.push(1)
    stack.push(2)
    stack.push(3)

    stack.print_stack()  # 输出：Stack elements: 1 2 3

    print("Top element:", stack.peek())  # 输出：Top element: 3

    print("Popped element:", stack.pop())  # 输出：Popped element: 3

    stack.print_stack()  # 输出：Stack elements: 1 2
```

Python 链式栈：

```python
class Node:  # 定义链式栈节点类
    def __init__(self, data):
        self.data = data  # 节点数据
        self.next = None  # 指向下一个节点的指针


class LinkedStack:  # 定义链式栈类
    def __init__(self):
        self.top = None  # 栈顶指针，初始为空

    def is_empty(self):  # 判断栈是否为空
        return self.top is None

    def push(self, value):  # 入栈操作
        new_node = Node(value)  # 创建新节点
        new_node.next = self.top  # 新节点的下一个指针指向当前栈顶
        self.top = new_node  # 更新栈顶指针

    def pop(self):  # 出栈操作
        if self.is_empty():  # 如果栈为空
            print("Stack is empty, cannot pop.")
            return None  # 返回 None 表示栈为空
        value = self.top.data  # 获取栈顶元素
        self.top = self.top.next  # 更新栈顶指针
        return value  # 返回弹出的元素

    def peek(self):  # 获取栈顶元素
        if self.is_empty():  # 如果栈为空
            print("Stack is empty, cannot peek.")
            return None  # 返回 None 表示栈为空
        return self.top.data  # 返回栈顶元素

    def print_stack(self):  # 打印栈中所有元素
        if self.is_empty():  # 如果栈为空
            print("Stack is empty.")
            return
        print("Stack elements:", end=" ")
        current = self.top  # 从栈顶开始遍历
        while current is not None:  # 遍历到栈底
            print(current.data, end=" ")  # 输出节点数据
            current = current.next  # 移动到下一个节点
        print()


if __name__ == "__main__":  # 测试代码
    stack = LinkedStack()  # 创建一个链式栈

    stack.push(1)
    stack.push(2)
    stack.push(3)

    stack.print_stack()  # 输出：Stack elements: 3 2 1

    print("Top element:", stack.peek())  # 输出：Top element: 3

    print("Popped element:", stack.pop())  # 输出：Popped element: 3

    stack.print_stack()  # 输出：Stack elements: 2 1
```



## 适用场景 (Use Cases) 及示例

栈的 LIFO 特性使其在很多场景下非常有用，尤其是在需要**回溯**或**反向处理**的场合。

1. **函数调用栈 (Function Call Stack)：**  这是栈最经典的应用之一。  当程序调用一个函数时，会将函数的相关信息（例如，返回地址、局部变量、参数等）压入栈中，当函数执行完毕返回时，再从栈顶弹出这些信息，程序才能正确地返回到调用函数的位置继续执行。  **递归调用**  也依赖于函数调用栈来管理每一层递归的状态。

   **示例 (递归阶乘函数):**

   ```python
   def factorial(n):
       if n == 0:
           return 1
       else:
           return n * factorial(n-1)
   
   result = factorial(3) # 调用 factorial(3)
   print(result) # 输出 6
   
   # 函数调用栈的变化 (简化示意):
   # 1. 调用 factorial(3)，信息入栈 (factorial(3))
   # 2. 调用 factorial(2)，信息入栈 (factorial(2))
   # 3. 调用 factorial(1)，信息入栈 (factorial(1))
   # 4. 调用 factorial(0)，信息入栈 (factorial(0))，返回 1
   # 5. factorial(0) 返回，栈顶信息弹出
   # 6. factorial(1) 得到返回值 1，计算 1*1=1，返回 1，栈顶信息弹出
   # 7. factorial(2) 得到返回值 1，计算 2*1=2，返回 2，栈顶信息弹出
   # 8. factorial(3) 得到返回值 2，计算 3*2=6，返回 6，栈顶信息弹出
   # 9. 最终结果 6
   ```

2. **表达式求值 (Expression Evaluation)：**  编译器和解释器使用栈来解析和计算数学表达式，例如中缀表达式到后缀表达式的转换，以及后缀表达式的求值。

   **示例 (简单的后缀表达式求值):**  假设有后缀表达式 "3 4 + 2 * "

   ```python
   # 算法步骤 (使用栈):
   # 1. 遇到数字 "3"，压栈 (栈: [3])
   # 2. 遇到数字 "4"，压栈 (栈: [3, 4])
   # 3. 遇到运算符 "+"，弹栈两次，得到 4 和 3，计算 3+4=7，结果 7 压栈 (栈: [7])
   # 4. 遇到数字 "2"，压栈 (栈: [7, 2])
   # 5. 遇到运算符 "*"，弹栈两次，得到 2 和 7，计算 7*2=14，结果 14 压栈 (栈: [14])
   # 6. 表达式结束，栈中唯一的值 14 就是结果
   
   # Python 代码 (简化版，仅处理加法和乘法，假设输入是有效的后缀表达式)
   def evaluate_postfix_expression(expression):
       tokens = expression.split() # 分割成 token 列表
       stack = []
       for token in tokens:
           if token.isdigit(): # 如果是数字
               stack.append(int(token)) # 压栈数字 (转换为整数)
           else: # 如果是运算符
               operand2 = stack.pop() # 弹出第二个操作数 (注意顺序)
               operand1 = stack.pop() # 弹出第一个操作数
               if token == '+':
                   result = operand1 + operand2
               elif token == '*':
                   result = operand1 * operand2
               else:
                   raise ValueError("Unsupported operator")
               stack.append(result) # 将计算结果压栈
       return stack.pop() # 最终结果在栈顶
   
   expression = "3 4 + 2 * "
   result = evaluate_postfix_expression(expression)
   print(result) # 输出 14
   ```

   

3.  **浏览器历史记录 (Browser History):**  浏览器使用栈来管理用户的浏览历史。  每当你访问一个新的网页时，该网页的 URL 会被压入栈中。  当你点击 “后退” 按钮时，浏览器会从栈顶弹出一个 URL，并加载该网页。  “前进” 功能通常可以用另一个栈来实现，或者在原历史栈的基础上进行操作。

    **操作流程 (简化示意):**
    
*   **访问网页 A：**  网页 A 的 URL 压栈 (栈: [A])
    *   **访问网页 B：**  网页 B 的 URL 压栈 (栈: [A, B])
*   **访问网页 C：**  网页 C 的 URL 压栈 (栈: [A, B, C])
    *   **点击 "后退"：**  栈顶 URL (C) 弹出，加载网页 B (栈: [A, B])
    *   **再次点击 "后退"：**  栈顶 URL (B) 弹出，加载网页 A (栈: [A])
    *   **点击 "前进" (假设前进栈存在且有内容)：**  从前进栈弹出一个 URL，压入历史栈，加载该网页。
    
4.  **其他应用场景：**
    *   **撤销操作 (Undo/Redo)：**  编辑器、绘图软件等使用栈来记录用户的操作历史，实现撤销和重做功能。
    *   **括号匹配 (Parentheses Matching)：**  编译器使用栈来检查代码中的括号是否正确匹配。
    *   **深度优先搜索 (DFS - Depth First Search)：**  图算法中的深度优先搜索可以使用栈来辅助实现。

## 总结

栈是一种简单但非常强大的数据结构，其核心思想是 **后进先出 (LIFO)** 。  理解栈的概念、操作和应用场景，对于理解程序运行的底层机制，以及解决特定类型的问题非常有帮助。  在后续的学习中，你会在更多算法和数据结构的应用中看到栈的身影。