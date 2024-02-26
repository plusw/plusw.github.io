### [数据结构和算法](https://plusw.github.io/blog/#article/article06someCodeNode)
*2024,02.19*  
    我的个人code笔记

##### 算法常用数据结构java
1. 链表（LinkedList）
特点：由一系列节点组成，每个节点包含数据和指向下一个节点的链接。支持双向链表（java.util.LinkedList）。
应用：适用于频繁的插入和删除操作。
2. 栈（Stack）
特点：后进先出（LIFO）的数据结构。java.util.Stack 类已过时，推荐使用 Deque 接口的实现，如 ArrayDeque。
应用：解析表达式，回溯算法等。
3. 队列（Queue）
特点：先进先出（FIFO）的数据结构。java.util.Queue 接口有多种实现，如 LinkedList 和 PriorityQueue。
应用：宽度优先搜索（BFS）、缓存实现等。
4. 树（Tree）
特点：非线性的数据结构，以分层方式存储数据。二叉树、红黑树等。
应用：TreeMap 和 TreeSet 在内部使用红黑树实现。
5. 哈希表（HashTable/HashMap）
特点：基于键的哈希值来存储数据，允许快速的插入、搜索和删除操作。
应用：HashMap、HashSet 等。
6. 图（Graph）
特点：由节点（或顶点）和边组成，可以是有向的或无向的。Java 标准库中没有直接支持，需要自定义实现或使用第三方库。
应用：表示和处理对象之间的多对多关系。
7. 堆（Heap）
特点：一种特殊的完全二叉树，所有节点都满足堆属性（例如，任意节点的值都不大于其子节点的值，这样的堆称为最小堆）。
应用：PriorityQueue 类实现了最小堆。
8. 集合（Set）
特点：不允许元素重复的集合。HashSet、LinkedHashSet 和 TreeSet 是三个主要实现。
应用：数据去重，集合运算等。
9. 映射（Map）
特点：存储键值对，键不允许重复。HashMap、LinkedHashMap 和 TreeMap 是三个主要实现。
应用：快速查找、数据字典等。