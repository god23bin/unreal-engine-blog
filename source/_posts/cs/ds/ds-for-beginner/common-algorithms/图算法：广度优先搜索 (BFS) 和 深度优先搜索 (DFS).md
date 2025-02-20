---
title: 图算法：广度优先搜索 (BFS) 和 深度优先搜索 (DFS)
date: 2025/1/01 12:48:25
index_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201338383.jpg
banner_img: https://pic-bed-of-god23bin.oss-cn-shenzhen.aliyuncs.com/img/202502201338383.jpg
categories:
  - [计算机科学基础,数据结构,初学者入门,4.常用算法]
tag:
  - 数据结构
  - 图算法
published: true
---

## 图算法：广度优先搜索 (BFS) 和 深度优先搜索 (DFS)

**概念：图遍历算法，用于系统地访问图中的所有节点**

**图遍历算法** 是图论中最基础和重要的算法之一。它们的目标是从图中的某个 **起始节点** 出发，按照一定的规则 **系统地访问图中的所有节点**，确保每个节点都被访问到，并且只被访问一次（对于某些应用场景，可能会允许多次访问，但基本思想仍然是遍历）。 图遍历算法是许多更高级图算法的基础，例如，最短路径算法、最小生成树算法、网络流算法等都离不开图遍历。

我们之前已经简要介绍过图的 **广度优先搜索 (BFS)**  和 **深度优先搜索 (DFS)** ， 这两种算法是最经典、最常用的图遍历算法。它们采用了不同的搜索策略，适用于不同的应用场景。

## 广度优先搜索 (Breadth-First Search - BFS)

**概念：层序遍历图的算法，逐层探索节点**

**广度优先搜索 (BFS)**  是一种 **层序遍历**  图的算法。  它从图的 **起始节点**  开始，**逐层**  地探索图的节点。  就像水波纹扩散一样，先访问起始节点的所有邻居节点（第一层邻居），然后访问邻居节点的邻居节点（第二层邻居），以此类推，一层一层地向外扩展，直到访问完所有可达节点。  BFS 保证了 **先访问离起始节点近的节点，再访问离起始节点远的节点**。

* **算法步骤 (使用队列 Queue 实现):**

  BFS 通常使用 **队列 (Queue)**  这种数据结构来实现。  队列的 **先进先出 (FIFO)**  特性保证了 BFS 的层序遍历特性。

  1.  **初始化：**
      *   创建一个 **队列 `queue`** ，用于存储待访问的节点。
      *   创建一个 **集合 `visited `** ，用于记录已访问的节点，防止重复访问和无限循环。
      *   将 **起始节点 `start_node`**  加入队列 `queue`，并将 `start_node`  加入 `visited` 集合。

  2.  **循环遍历：**
      *   当队列 `queue`  **不为空**  时，循环执行以下操作：
          
          a.  **出队：**  从队列 `queue`  **队首**  取出一个节点 `current_node`  (出队)。
          
          b.  **访问：**  **访问 `current_node`**  (例如，打印节点值、进行某种处理)。
          
          c.  **探索邻居：**  遍历 `current_node`  的 **所有邻居节点 `neighbor`** ：
      
          - **检查是否已访问：**  如果 `neighbor`  **未被访问过**  (不在 `visited` 集合中)：
            - **入队：** 将 `neighbor`  加入队列 `queue`  (入队)。
            - **标记已访问：** 将 `neighbor`  加入 `visited`  集合。
      
  3.  **结束：** 当队列 `queue`  为空时，BFS 结束，所有可达节点都已被访问。

*   **应用示例和代码实现 (C++, Java, Python):**

    **应用场景：查找从起始节点到目标节点的最短路径 (无权图)**

    在 **无权图** 中，从起始节点到目标节点的最短路径 (路径长度最小) 可以使用 BFS 算法来查找。  因为 BFS 是按层遍历的，第一次访问到目标节点时，所经过的路径一定是起始节点到目标节点的最短路径 (边数最少)。

    **代码实现 (以查找最短路径为例):**

    **C++:**

    ```c++
    #include <iostream>
    #include <vector>
    #include <queue>
    #include <unordered_map>
    #include <unordered_set>

    std::vector<int> breadthFirstSearch(int startNode, int endNode, const std::unordered_map<int, std::vector<int>>& graph) {
        std::queue<std::pair<int, std::vector<int>>> queue; // 队列，存储节点和路径
        std::unordered_set<int> visited; // 记录已访问节点

        queue.push({startNode, {startNode}}); // 初始节点入队，路径为起始节点本身
        visited.insert(startNode);

        while (!queue.empty()) {
            std::pair<int, std::vector<int>> currentPair = queue.front();
            queue.pop();
            int currentNode = currentPair.first;
            std::vector<int> currentPath = currentPair.second;

            if (currentNode == endNode) { // 找到目标节点，返回路径
                return currentPath;
            }

            for (int neighbor : graph.at(currentNode)) {
                if (visited.find(neighbor) == visited.end()) { // 邻居节点未被访问过
                    visited.insert(neighbor);
                    std::vector<int> newPath = currentPath; // 复制当前路径
                    newPath.push_back(neighbor); // 添加邻居节点到新路径
                    queue.push({neighbor, newPath}); // 邻居节点入队
                }
            }
        }

        return {}; // 未找到路径，返回空路径
    }

    int main() {
        // 图的邻接表表示
        std::unordered_map<int, std::vector<int>> graph = {
            {0, {1, 2}},
            {1, {0, 3, 4}},
            {2, {0, 4}},
            {3, {1, 5}},
            {4, {1, 2, 5}},
            {5, {3, 4, 6}},
            {6, {5}}
        };

        int startNode = 0;
        int endNode = 6;
        std::vector<int> shortestPath = breadthFirstSearch(startNode, endNode, graph);

        if (!shortestPath.empty()) {
            std::cout << "从节点 " << startNode << " 到节点 " << endNode << " 的最短路径: ";
            for (int node : shortestPath) {
                std::cout << node << " ";
            }
            std::cout << std::endl;
        } else {
            std::cout << "从节点 " << startNode << " 到节点 " << endNode << " 没有路径" << std::endl;
        }

        return 0;
    }
    ```

    **Java:**

    ```java
    import java.util.*;

    public class BFS {
        public static List<Integer> breadthFirstSearch(int startNode, int endNode, Map<Integer, List<Integer>> graph) {
            Queue<Pair<Integer, List<Integer>>> queue = new LinkedList<>(); // 队列，存储节点和路径
            Set<Integer> visited = new HashSet<>(); // 记录已访问节点

            queue.offer(new Pair<>(startNode, Collections.singletonList(startNode))); // 初始节点入队，路径为起始节点本身
            visited.add(startNode);

            while (!queue.isEmpty()) {
                Pair<Integer, List<Integer>> currentPair = queue.poll();
                int currentNode = currentPair.getKey();
                List<Integer> currentPath = currentPair.getValue();

                if (currentNode == endNode) { // 找到目标节点，返回路径
                    return currentPath;
                }

                for (int neighbor : graph.getOrDefault(currentNode, Collections.emptyList())) {
                    if (!visited.contains(neighbor)) { // 邻居节点未被访问过
                        visited.add(neighbor);
                        List<Integer> newPath = new ArrayList<>(currentPath); // 复制当前路径
                        newPath.add(neighbor); // 添加邻居节点到新路径
                        queue.offer(new Pair<>(neighbor, newPath)); // 邻居节点入队
                    }
                }
            }

            return Collections.emptyList(); // 未找到路径，返回空路径
        }

        public static void main(String[] args) {
            // 图的邻接表表示
            Map<Integer, List<Integer>> graph = new HashMap<>();
            graph.put(0, Arrays.asList(1, 2));
            graph.put(1, Arrays.asList(0, 3, 4));
            graph.put(2, Arrays.asList(0, 4));
            graph.put(3, Arrays.asList(1, 5));
            graph.put(4, Arrays.asList(1, 2, 5));
            graph.put(5, Arrays.asList(3, 4, 6));
            graph.put(6, Arrays.asList(5));

            int startNode = 0;
            int endNode = 6;
            List<Integer> shortestPath = breadthFirstSearch(startNode, endNode, graph);

            if (!shortestPath.isEmpty()) {
                System.out.print("从节点 " + startNode + " 到节点 " + endNode + " 的最短路径: ");
                for (int node : shortestPath) {
                    System.out.print(node + " ");
                }
                System.out.println();
            } else {
                System.out.println("从节点 " + startNode + " 到节点 " + endNode + " 没有路径");
            }
        }

        // 辅助类 Pair
        static class Pair<K, V> {
            private K key;
            private V value;

            public Pair(K key, V value) {
                this.key = key;
                this.value = value;
            }

            public K getKey() {
                return key;
            }

            public V getValue() {
                return value;
            }
        }
    }
    ```

    **Python:**

    ```python
    from collections import deque

    def breadth_first_search(start_node, end_node, graph):
        queue = deque([(start_node, [start_node])]) # 队列，存储节点和路径
        visited = {start_node} # 记录已访问节点

        while queue:
            current_node, current_path = queue.popleft()

            if current_node == end_node: # 找到目标节点，返回路径
                return current_path

            for neighbor in graph.get(current_node, []):
                if neighbor not in visited: # 邻居节点未被访问过
                    visited.add(neighbor)
                    new_path = list(current_path) # 复制当前路径
                    new_path.append(neighbor) # 添加邻居节点到新路径
                    queue.append((neighbor, new_path)) # 邻居节点入队

        return [] # 未找到路径，返回空路径

    if __name__ == "__main__":
        # 图的邻接表表示
        graph = {
            0: [1, 2],
            1: [0, 3, 4],
            2: [0, 4],
            3: [1, 5],
            4: [1, 2, 5],
            5: [3, 4, 6],
            6: [5]
        }

        start_node = 0
        end_node = 6
        shortest_path = breadth_first_search(start_node, end_node, graph)

        if shortest_path:
            print(f"从节点 {start_node} 到节点 {end_node} 的最短路径: {shortest_path}")
        else:
            print(f"从节点 {start_node} 到节点 {end_node} 没有路径")
    ```

*   **BFS 的其他应用场景：**

    *   **社交网络关系查询 (一度好友、二度好友等)。**
    *   **网络爬虫 (按层抓取网页)。**
    *   **游戏地图搜索 (例如，迷宫游戏最短路径)。**
    *   **判断图的连通性。**

## 深度优先搜索 (Depth-First Search - DFS)

**概念：尽可能深地探索图的分支，回溯搜索**

**深度优先搜索 (DFS)**  是一种 **递归地**  探索图的算法。  它从图的 **起始节点**  开始，沿着一条路径 **尽可能深地**  探索下去，直到到达最深处 (无法继续前进)  或遇到已访问过的节点，然后 **回溯**  到上一个节点，再探索另一条路径。  DFS  类似于走迷宫，一条路走到黑，不行就退回，再换一条路。  DFS 倾向于 **优先探索图的深度**。

* **算法步骤 (递归实现):**

  DFS  可以使用 **递归**  或 **栈 (Stack)**  两种方式来实现。

  递归实现代码更简洁直观。

  1. **初始化：**

     - 创建一个 **集合 `visited`** ，用于记录已访问的节点。

  2. **递归函数 `DFS(node)`：**

     a.  **标记已访问：**  将当前节点 `node`  标记为 **已访问** ，并加入 `visited`  集合。

     b.  **访问：**  **访问 `node`**  (例如，打印节点值、进行某种处理)。

     c.  **递归探索邻居：**  遍历 `node`  的 **所有邻居节点 `neighbor`** ：

     - **检查是否已访问**：如果 `neighbor`  **未被访问过**  (不在 `visited` 集合中)：
       - **递归调用**  `DFS(neighbor)` ，继续深入探索。

  3. **启动搜索：** 从 **起始节点 `start_node`**  开始，调用 `DFS(start_node)`  启动深度优先搜索。

* **算法步骤 (使用栈 Stack 实现，非递归):**

  DFS  也可以使用 **栈 (Stack)**  来实现非递归版本。  栈的 **后进先出 (LIFO)**  特性符合 DFS 的深入探索和回溯的策略。

  1.  **初始化：**
      *   创建一个 **栈 `stack`** ，用于存储待访问的节点。
      *   创建一个 **集合 `visited`** ，用于记录已访问的节点。
      *   将 **起始节点 `start_node`**  压入栈 `stack`。

  2.  **循环遍历：**
      *   当栈 `stack`  **不为空**  时，循环执行以下操作：
          
          a.  **弹栈：**  从栈 `stack`  **栈顶**  弹出一个节点 `current_node`  (弹栈)。
          
          b.  **检查是否已访问：**  如果 `current_node`  **未被访问过**  (不在 `visited` 集合中)：
          
      - **标记已访问：**  将 `current_node`  标记为 **已访问**，并加入 `visited`  集合。
          - **访问：** **访问 `current_node`** 。
          - **压栈邻居：**  将 `current_node`  的 **所有邻居节点 `neighbor`**  **逆序压入栈 `stack`**  (逆序压栈是为了保证邻居节点的访问顺序与递归版本一致，如果邻居节点访问顺序没有要求，则可以顺序压栈)。
      
  3.  **结束：** 当栈 `stack`  为空时，DFS 结束，所有可达节点都已被访问。

*   **应用示例和代码实现 (C++, Java, Python):**

    **应用场景：判断图中两个节点之间是否存在路径**

    DFS  可以用来判断图中 **两个节点之间是否存在路径**。  从起始节点开始进行 DFS 遍历，如果在遍历过程中访问到了目标节点，则说明存在路径，否则不存在。

    **代码实现 (以判断路径是否存在为例，递归版本):**

    **C++:**

    ```c++
    #include <iostream>
    #include <vector>
    #include <unordered_map>
    #include <unordered_set>

    bool depthFirstSearch(int currentNode, int endNode, const std::unordered_map<int, std::vector<int>>& graph, std::unordered_set<int>& visited) {
        visited.insert(currentNode); // 标记当前节点为已访问

        if (currentNode == endNode) { // 找到目标节点
            return true;
        }

        for (int neighbor : graph.at(currentNode)) {
            if (visited.find(neighbor) == visited.end()) { // 邻居节点未被访问过
                if (depthFirstSearch(neighbor, endNode, graph, visited)) { // 递归搜索邻居节点
                    return true; // 如果在邻居节点找到了路径，则返回 true
                }
            }
        }

        return false; // 所有邻居节点都搜索完毕，未找到路径，返回 false
    }

    int main() {
        // 图的邻接表表示
        std::unordered_map<int, std::vector<int>> graph = {
            {0, {1, 2}},
            {1, {0, 3, 4}},
            {2, {0, 4}},
            {3, {1, 5}},
            {4, {1, 2, 5}},
            {5, {3, 4, 6}},
            {6, {5}}
        };

        int startNode = 0;
        int endNode = 6;
        std::unordered_set<int> visitedNodes; // 记录已访问节点
        bool pathExists = depthFirstSearch(startNode, endNode, graph, visitedNodes);

        if (pathExists) {
            std::cout << "从节点 " << startNode << " 到节点 " << endNode << " 存在路径" << std::endl;
        } else {
            std::cout << "从节点 " << startNode << " 到节点 " << endNode << " 不存在路径" << std::endl;
        }

        return 0;
    }
    ```

    **Java:**

    ```java
    import java.util.*;

    public class DFS {
        public static boolean depthFirstSearch(int currentNode, int endNode, Map<Integer, List<Integer>> graph, Set<Integer> visited) {
            visited.add(currentNode); // 标记当前节点为已访问

            if (currentNode == endNode) { // 找到目标节点
                return true;
            }

            for (int neighbor : graph.getOrDefault(currentNode, Collections.emptyList())) {
                if (!visited.contains(neighbor)) { // 邻居节点未被访问过
                    if (depthFirstSearch(neighbor, endNode, graph, visited)) { // 递归搜索邻居节点
                        return true; // 如果在邻居节点找到了路径，则返回 true
                    }
                }
            }

            return false; // 所有邻居节点都搜索完毕，未找到路径，返回 false
        }

        public static void main(String[] args) {
            // 图的邻接表表示
            Map<Integer, List<Integer>> graph = new HashMap<>();
            graph.put(0, Arrays.asList(1, 2));
            graph.put(1, Arrays.asList(0, 3, 4));
            graph.put(2, Arrays.asList(0, 4));
            graph.put(3, Arrays.asList(1, 5));
            graph.put(4, Arrays.asList(1, 2, 5));
            graph.put(5, Arrays.asList(3, 4, 6));
            graph.put(6, Arrays.asList(5));

            int startNode = 0;
            int endNode = 6;
            Set<Integer> visitedNodes = new HashSet<>(); // 记录已访问节点
            boolean pathExists = depthFirstSearch(startNode, endNode, graph, visitedNodes);

            if (pathExists) {
                System.out.println("从节点 " + startNode + " 到节点 " + endNode + " 存在路径");
            } else {
                System.out.println("从节点 " + startNode + " 到节点 " + endNode + " 不存在路径");
            }
        }
    }
    ```

    **Python:**

    ```python
    def depth_first_search(current_node, end_node, graph, visited):
        visited.add(current_node) # 标记当前节点为已访问

        if current_node == end_node: # 找到目标节点
            return True

        for neighbor in graph.get(current_node, []):
            if neighbor not in visited: # 邻居节点未被访问过
                if depth_first_search(neighbor, end_node, graph, visited): # 递归搜索邻居节点
                    return True # 如果在邻居节点找到了路径，则返回 True

        return False # 所有邻居节点都搜索完毕，未找到路径，返回 False

    if __name__ == "__main__":
        # 图的邻接表表示
        graph = {
            0: [1, 2],
            1: [0, 3, 4],
            2: [0, 4],
            3: [1, 5],
            4: [1, 2, 5],
            5: [3, 4, 6],
            6: [5]
        }

        start_node = 0
        end_node = 6
        visited_nodes = set() # 记录已访问节点
        path_exists = depth_first_search(start_node, end_node, graph, visited_nodes)

        if path_exists:
            print(f"从节点 {start_node} 到节点 {end_node} 存在路径")
        else:
            print(f"从节点 {start_node} 到节点 {end_node} 不存在路径")
    ```

*   **DFS 的其他应用场景：**

    *   **路径查找 (所有路径、特定条件路径)。**
    *   **图的连通性判断 (类似于 BFS)。**
    *   **环检测。**
    *   **拓扑排序 (有向无环图 DAG)。**
    *   **迷宫求解 (所有路径)。**
    *   **树的先序遍历、中序遍历、后序遍历 (DFS 在树上的应用)。**

*   **BFS vs DFS 的应用场景总结：**

    | 特性         | 广度优先搜索 (BFS)                                 | 深度优先搜索 (DFS)                               |
    | ------------ | ------------------------------------------------ | ------------------------------------------------ |
    | 搜索策略     | 层序遍历，逐层扩展                                 | 尽可能深入，回溯探索                               |
    | 数据结构     | 队列 (Queue)                                     | 栈 (Stack) (或递归调用栈)                         |
    | 最短路径     | **擅长查找无权图最短路径**                           | 不擅长查找最短路径 (但可用于判断路径是否存在)       |
    | 空间复杂度   | 可能较高 (需要存储每层节点，尤其在广度较大的图中)         | 通常较低 (只需存储当前路径节点，递归深度受树的深度限制)     |
    | 应用场景     | 最短路径查找，层级关系探索，网络爬虫，社交关系分析，检查邻近性 | 路径存在性判断，环路检测，拓扑排序，迷宫求解，深度探索，树的遍历 |


## 总结

BFS 和 DFS 是图遍历算法中最基础也是最重要的两种算法。  它们各有特点，适用于不同的应用场景。  **BFS 擅长查找最短路径和检查邻近性**，例如，社交网络中查找最短关系链、地图导航中查找最短路径等。  **DFS 擅长探索图的深度和连通性**，例如，判断图中是否存在环路、查找所有可能的路径、进行拓扑排序等。  在实际应用中，需要根据具体的问题需求选择合适的图遍历算法。  掌握 BFS 和 DFS 的原理和应用，是深入学习图论算法和解决实际问题的关键一步。