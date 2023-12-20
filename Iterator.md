
BST with stack
```java
public class BSTIterator {
    private Stack<TreeNode> stack = new Stack<TreeNode>();
    
    public BSTIterator(TreeNode root) {
        pushAll(root); // gets all from root.left... nodes
    }

    public boolean hasNext() {
        return !stack.isEmpty();
    }

    /** @return the next smallest number */
    public int next() {
        TreeNode tmpNode = stack.pop(); // gets number on top of stack (most left)
        pushAll(tmpNode.right); // adds all .right.left... nodes (if .right exists)
        return tmpNode.val; // returns former top of stack val
    }
    
    private void pushAll(TreeNode node) {
        for (; node != null; stack.push(node), node = node.left);
    }
}
```