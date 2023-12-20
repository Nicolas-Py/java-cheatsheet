An `Iterator` is an object that can be used to loop through collections, like [ArrayList](https://www.w3schools.com/java/java_arraylist.asp) and [HashSet](https://www.w3schools.com/java/java_hashset.asp). It is called an "iterator" because "iterating" is the technical term for looping.

### Trees
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

### Nested Lists
Pretty bad but "elegant"
```java
public class NestedIterator implements Iterator<Integer> {
    
    private Queue<Integer> flatInt;  
    private ArrayList<Integer> flatInteger = new ArrayList<>();
    public NestedIterator(List<NestedInteger> nestedList) {
        for (NestedInteger x: nestedList) {
            unZip(x, flatInteger);
        }
        flatInt = new LinkedList<>(flatInteger);
    }

    @Override
    public Integer next() {
        return flatInt.remove();
    }

    @Override
    public boolean hasNext() {
         return !flatInt.isEmpty();
    }

    private void unZip(NestedInteger x, ArrayList<Integer> list) {
        if (x.isInteger()) {
            list.add(x.getInteger());
        } else {
	        List<NestedInteger> temp = x.getList();
	        for (int i = 0; i<temp.size(); i++) {
	          if (temp.get(i).isInteger()) {
	                list.add(temp.get(i).getInteger());
	          } else {
	                unZip(temp.get(i), list);
	          }
	        }
        }
    }
}
```