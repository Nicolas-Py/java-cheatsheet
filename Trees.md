
# Binary tree in order
### Iterative
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

### - Recursive
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

# Binary tree pre order:
## - Iterative
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

## - Recursive
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

# Binary tree post order
## - Iterative
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

## - Recursive
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

# N-ary tree Pre order:
## Recursive
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

