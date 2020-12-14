## 21 复制带随机指针的链表

给定一个链表，每个节点包含一个额外增加的随机指针，该指针可以指向链表中的任何节点或空节点。要求返回这个链表的深拷贝。 

用一个由 n 个节点组成的链表来表示输入/输出中的链表。每个节点用一个 [val, random_index] 表示：

* val：一个表示 Node.val 的整数。
* random_index：随机指针指向的节点索引（范围从 0 到 n-1）；如果不指向任何节点，则为 null 。
 
[138. 复制带随机指针的链表](https://leetcode-cn.com/problems/copy-list-with-random-pointer/)

链表结构如下：

```java
class Node {
    int val;
    Node next;
    Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}
```

示例

<img src="./imglinklist/06-138-01.png" width=300>

```
输入：head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
输出：[[7,null],[13,0],[11,4],[10,2],[1,0]]
```

<img src="./imglinklist/06-138-02.png" width=300>

```
输入：head = [[1,1],[2,1]]
输出：[[1,1],[2,1]]
```

### O(1) 空间的迭代

1. 遍历原来的链表并拷贝每一个节点，将拷贝节点放在原来节点的旁边，创造出一个旧节点和新节点交错的链表。

2. 迭代这个新旧节点交错的链表，并用旧节点的 random 指针去更新对应新节点的 random 指针。比方说，B 的 random 指针指向 A ，意味着 B' 的 random 指针指向 A' 。

3. next 指针也需要被正确赋值，以便将新的节点正确链接同时将旧节点重新正确链接。

<img src="./imglinklist/06-138-03.png" width=600>




### 回溯





### O(N) 空间的迭代





