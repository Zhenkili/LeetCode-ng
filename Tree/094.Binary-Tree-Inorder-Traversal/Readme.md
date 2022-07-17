### 094.Binary-Tree-Inorder-Traversal

此题的代码几乎和 144. Binary Tree Preorder Traversal 完全一致。唯一的区别就是记录元素的时机。先序遍历（preorder）是首先记录根节点，所以在入栈的时候就需要读数（读完根节点，再递归左子树）。而中序遍历（inorder）是先记录左子树，所以需要先一路入栈到最底层，在退栈的时候再开始依次读数。
```java
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode cur = root; //表示最左下角的node
        while(cur != null || !stack.isEmpty()) {
            while(cur != null){ //一直到达最左下，不是左下的存档
                stack.push(cur);
                cur = cur.left;
            }
            //已经到达左下
            cur = stack.pop();
            res.add(cur.val);
            //研究对象变为右节点
            cur = cur.right;
        }
        return res;
    }
```        


[Leetcode Link](https://leetcode.com/problems/binary-tree-inorder-traversal)
