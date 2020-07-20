#### 13. 2-1

------

> Write pseudocode for RIGHT-ROTATE.

##### Answer

```pseudocode
RIGHT-ROTATE(T, y)
    x = y.left
    y.left = x.right
    if x.right != T.nil
        x.right.p = y
    x.p = y.p
    if y.p == T.nil
        T.root = x
    elseif y == y.p.right
        y.p.right = x
    else y.p.left = x
    x.right = y
    y.p = x
```

#### 13. 2-2

------

> Argue that in every n-node binary search tree, there are exactly n - 1 possible rotations.

##### Answer

- 每次旋转都以一条边为“支轴”进行旋转。n个节点的二叉搜索树中有n-1条边，对应n-1种可能的旋转

#### 13. 2-3

------

> Let a, b, and c be arbitrary nodes in subtrees α,β and 􏰈γ, respectively, in the left tree of Figure 13.2. How do the depths of a, b, and c change when a left rotation is performed on node x in the figure?

##### Answer

- α,β,γ的变化和a,b,c的变化是一致的。
  1. a.depth + 1
  2. b.depth 不变
  3. c.depth - 1

#### 13. 2-4

------

> Show that any arbitrary n-node binary search tree can be transformed into any other arbitrary n-node binary search tree using O(n) rotations. (*Hint:* First show that at most n -1 right rotations suffice to transform the tree into a right-going chain.)

##### Answer

- 假定初始的根结点和根结点的所有后继右孩子结点为 *right-going chain* 的初始状态，对于该初始链中的任何一个节点，如果该节点有左孩子，则对该节点进行Right-Rotate操作，操作的结果可以将该节点的左孩子加入到该链中，最坏情况下，初始情况是 *left-going chain*，我们需要n-1次Right-Rotate才能得到目标链
- 任何一棵树T1都可以转变为右侧展开的链，目标树T2也可以转变为目标链。我们可以在O(n)的操作内将T1转变为 *right-going chain*，再通过Left-Rotate转变得到T2。Rotation操作的复杂度为O(1)，则总时间复杂度为O(n)

#### 13. 2-5

------

> We say that a binary search tree T1 can be **right-converted** to binary search tree T2 if it is possible to obtain T2 from T1 via a series of calls to RIGHT-ROTATE. Give an example of two trees T1 and T2 such that T1 cannot be right-converted to T2. Then, show that if a tree T1 can be right-converted to T2, it can be right-converted using O(n^2) calls to RIGHT-ROTATE.

##### Answer - 1

- 很容易找到一种符合题目要求的例子：T1无法 **right-converted** 得到T2，但T1可以 **left-converted** 得到T2。
- 反例如：T1[0,#,1],T2[1,0,#]

##### Answer - 2

- 通过13. 2-4我们可以得到结论 *Show that any arbitrary n-node binary search tree can be transformed into any other arbitrary n-node binary search tree using O(n) rotations.*，且我们已知，Rotation操作保持了二叉搜索树的性质
- 我们可以使用O(n)的时间令T1的根结点等同于T2的根结点，之后在T1的子树中递归调用该操作。因为树中共有n个结点，所以时间复杂度为O(n^2)