---
title: STL 模板类
date: 2022-06-05 23:25:40
categories:
  - 算法
tags:
  - STL
---
本文介绍了一些 STL 模板类。
<!-- more -->
## 什么是 STL

1. STL（Standard Template Library），即标准模板库，是一个高效的 C++ 程序库，包含了诸多常用的基本数据结构和基本算法。
2. 从逻辑层次来看，在STL中体现了泛型化程序设计的思想。在这种思想里，大部分基本算法被抽象，被泛化，独立于与之对应的数据结构，用于以相同或相近的方式处理各种不同情形。
3. 从实现层次看，整个STL是以一种类型参数化的方式实现的，基于模板（template）。

STL有六大组件，分别是容器（Containers）、迭代器（Iterators）、空间配置器（Allocators）、配接器（Adapters）、算法（Algorithms）、仿函数（Functors）。

容器（Containers）：用来管理某类对象的集合。每一种容器都有其优点和缺点，所以，为了应付程序中的不同需求，STL 准备了七种基本容器类型。
迭代器（Iterators）：用来在一个对象集合的元素上进行遍历动作。这个对象集合或许是个容器，或许是容器的一部分。每一种容器都提供了自己的迭代器，而这些迭代器了解该种容器的内部结构。
算法（Algorithms）：用来处理对象集合中的元素，比如 sort，search，copy，erase 那些元素。通过迭代器的协助，我们只需撰写一次算法，就可以将它应用于任意容器之上，这是因为所有容器的迭代器都提供一致的接口。
STL 的基本观念就是将数据和操作分离。数据由容器进行管理，操作则由算法进行，而迭代器在两者之间充当粘合剂，使任何算法都可以和任何容器交互运作。

## 容器（Container）

### deque：双端队列

一种序列式容器。由一段一段的连续空间（块）拼接构成。

块内的实现类似于 `vector`；块与块之间的实现类似于 `list`。

#### 优点

- 支持随机访问，`[]` 操作的时间复杂度为 $O(m)$（$m$ 为块的个数）。
- `pop`、`push` 时间复杂度为 $O(1)$。

#### 缺点

- 不适合中间的插入删除操作。

### vector：向量

一种序列式容器。拥有一段 **连续** 的内存空间，并且起始地址不变。

#### 优点

- 支持随机访问，即 `[]` 操作的时间复杂度为 $O(1)$。
- 避免了数组的越界与空间浪费问题。

#### 缺点

- 当加入元素后 `size()` 将大于 `capacity()` 时，需要重新申请一块足够大的内存并进行内存的复制。
- 当向其头部或中部插入或删除元素时，为了保持原本的顺序，插入或删除点之后的所有元素都必须移动，所以插入的效率比较低。

### list：双向链表

前后顺序是靠指针来维系的序列式容器。

#### 优点

- 每放入一个元素都会从内存中分配，每删除一个元素都会释放它占用的内存。
- 在哪里添加删除元素性能都很高，不需要移动内存。

#### 缺点

- 不支持随机访问。

### set：集合

关联容器，含有键值类型对象的已排序集，搜索、移除和插入拥有对数复杂度。其内部通常采用红黑树实现。平衡二叉树的特性使得 `set` 非常适合处理需要同时兼顾查找、插入与删除的情况。

#### 优点

- 使用平衡二叉树实现，便于元素查找，且保持了元素的唯一性，以及能自动排序。

#### 缺点

- 每次修改值的时候，都需要调整红黑树，效率有一定影响。

### map：映射

关联容器，`map` 是有序键值对容器，它的元素的键是唯一的。搜索、移除和插入操作拥有对数复杂度。`map` 通常实现为红黑树。

#### 优点

- 当要存储的数据需要用 `std::string`、`std::vector` 等类型索引时，`map` 可以方便地实现。

#### 缺点

- 每次修改值的时候，都需要调整红黑树，效率有一定影响。

### string：字符串

string 则是一个简单的类，提供了字符串的操作。

#### 优点

- 动态分配空间，不用担心越界。
- 重载了加法运算符和比较运算符。使得可以轻松拼接字符串和将 `string` 作为 `map` 的键存储数据。

#### 缺点

- 相比于字符数组要慢一点点。