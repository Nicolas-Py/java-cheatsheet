# Depth first search
## Binary tree
### Inorder
If you search a BST "Inorder" you will receive the nodes "sorted"
#### Iterative
```Java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        List<Integer> result = new ArrayList<>();
        while(!stack.isEmpty() || root != null) {
            while(root != null) {
                stack.add(root);
                root = root.left;
            }
            root = stack.pop();
            result.add(root.val);
            root = root.right;
        }
        return result;
    }
}
```

#### Recursive
```Java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        return dfs(root, new ArrayList<Integer>());
    }
    
    private List<Integer> dfs(TreeNode root, List<Integer> list) {
        if (root == null) return list;
        list = dfs(root.left, list);
        list.add(root.val);
        list = dfs(root.right, list);
        return list;
    }
}
```

### Binary tree pre order:
#### Iterative
```Java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        
        stack.push(root);
        while(!stack.isEmpty()) {
            root = stack.pop();
            if(root != null) {
                list.add(root.val);
                stack.push(root.right);
                stack.push(root.left);
            }
        }
        return list;
    }
}
```

#### Recursive
```Java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        return dfs(root, new ArrayList<Integer>());
    }
    
    private List<Integer> dfs(TreeNode root, List<Integer> list) {
        if (root == null) return list;
        list.add(root.val);
        list = dfs(root.left, list);
        list = dfs(root.right, list);
        return list;
    }
}
```

### Binary tree post order
#### Iterative
```Java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> list = new LinkedList<>();
        Stack<TreeNode> stack = new Stack<>();
        
        stack.push(root);
        while(!stack.isEmpty()) {
            root = stack.pop();
            if (root != null) {
                list.add(0, root.val);
                stack.push(root.left);
                stack.push(root.right);
            }
        }
        return list;
    }
}
```

#### Recursive
```Java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
       return dfs(root, new ArrayList<Integer>());
    }
    
    private List<Integer> dfs(TreeNode root, List<Integer> list) {
        if (root == null) return list;
        list = dfs(root.left, list);
        list = dfs(root.right, list);
        list.add(root.val);
        return list;
    }
}
```

## N-ary tree
### Pre order
#### Recursive
```Java
class Solution {
	public List<Integer> preorder(Node root) {
		return dfs(root, new ArrayList<Integer>());
	}
	
	private List<Integer> dfs(Node root, List<Integer> list) {
	if (root == null) return list;
	list.add(root.val);
	
	for (Node child : root.children) {
		list = dfs(child, list);
	}
	return list;
	}
}
```

### Post order
#### Recursive
```Java
class Solution {
	public List<Integer> postorder(Node root) {
		return dfs(root, new ArrayList<Integer>());
	}
	
	private List<Integer> dfs(Node root, List<Integer> list) {
	if (root == null) return list;
	
	for (Node child: root.children) {
		list = dfs(child, list);
	}
	
	list.add(root.val);
	return list;
	}
}
```
# Breadth first search
## Binary tree
#### Iterative
```Java
class Solution {
	public List<List<Integer>> levelOrder(TreeNode root) {
		List<List<Integer>> result = new ArrayList<>();
		
		if (root == null) return result;
		Queue<TreeNode> queue = new LinkedList<>();
		
		queue.add(root);
		
		while(!queue.isEmpty()) {
			int size = queue.size();
			List<Integer> level = new ArrayList<>(); // will store the levels
			
			for (int i=0; i<size; i++) {
				TreeNode curr = queue.poll(); //takes out the first item;
				level.add(curr.val);
				if (curr.left != null) {
					queue.add(curr.left);
				}
				if (curr.right != null) {
					queue.add(curr.right);
				}
			}
			result.add(level);
		}
		return result;
	}
}
```

# Max Depth of  tree
### Binary tree
```Java
class Solution {
	public int maxDepth(TreeNode root) {
		if (root == null) return 0;
		return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
	}
}
```
### N-ary tree
```Java
class Solution {
	public int maxDepth(Node root) {
		return (getMaxDepth(root, 0));
	}

	public int getMaxDepth(Node root, int depth) {
		if (root == null) return 0;
			int maxDepth = depth+1;
		for (Node child: root.children) {
			maxDepth = Math.max(maxDepth, getMaxDepth(child, depth+1));
		}
		return maxDepth;
		}
}
```

# Identical

### Binary Tree

(Scuffed Nico Approach)
```Java
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if(q==null&&p==null) {
            return true;
        } else if (q==null||p==null) {
            return false;
        }
        return Objects.equals(traverse(p), traverse(q));
    }

    public List<Integer> traverse(TreeNode root) {
        return traverse(root, new ArrayList<Integer>());
    }


    public List<Integer> traverse(TreeNode root, List<Integer> list) {
        list.add(root.val);
        list.addAll(traverseL(root.left, list));
        list.addAll(traverseR(root.right, list));
        return list;
    }

    public List<Integer> traverseL(TreeNode root, List<Integer> list) {
        if (root==null) {
            list.add(-2);
            return list;
        }
        list.add(root.val);
        list = traverseL(root.left, list);
        list = traverseR(root.right, list);
        return list;
    }

    public List<Integer> traverseR(TreeNode root, List<Integer> list) {
        if (root==null) {
            list.add(-1);
            return list;
            }
        list.add(root.val);
        list = traverseL(root.left, list);
        list = traverseR(root.right, list);
        return list;
    }
}
```

# Invert
### Binary Tree
``` java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        dfs(root);
        return root;
    }

    private void dfs(TreeNode root) {
        if (root==null) {
            return;
        }
        TreeNode temp = root.left;
        root.left=root.right;
        root.right=temp;
        dfs(root.left);
        dfs(root.right);
    }
}
```