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
		return dfs(root, 1);
	}

	private int dfs(Node root, int depth) {
		if (root == null) return 0;
		
		int maxDepth = depth;
		for (Node child: root.children) {
			maxDepth = Math.max(maxDepth, dfs(child, depth+1));
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
        if (p == null && q == null) return true;
		if (p == null || q == null) return false;
		if (p.val != q.val) return false;
		return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
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

# List to Tree

### Sorted array to balanced BST
#### no helper function
```java
class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        if(nums.length==1) {return new TreeNode(nums[0]);}
        if(nums.length==0) {return null;}
        int half = nums.length/2;
        TreeNode root = new TreeNode(nums[half]);
        int[] left = new int[half];
        int i = 0;
        for (; i<half; i++) {
            left[i]=nums[i];
        }
        i++;
        int[] right = new int[nums.length-left.length-1];
        for (int j = 0; i<nums.length; j++) {
            right[j]=nums[i];
            i++;
        }
        root.left = sortedArrayToBST(left);
        root.right = sortedArrayToBST(right);
    
        return root;
    }
}
```
#### with helper funciton
```Java
class Solution {
	public TreeNode sortedArrayToBST(int[] nums) {
		return dfs(nums, 0, nums.length-1);
	}
		
	private TreeNode dfs(int[] nums, int start, int end) {
		if (start > end) return null;
		int middle = (start+end)/2;
		TreeNode root = new TreeNode(nums[middle]);
		root.left = dfs(nums, start, middle-1);
		root.right = dfs(nums, middle+1, end);
		return root;
	}
}
```

# Merge two binary trees
```Java
class Solution {
	public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
		if (root1 == null) return root2;
		if (root2 == null) return root1;
		root1.val+=root2.val;
		
		root1.left = mergeTrees(root1.left, root2.left);
		root1.right = mergeTrees(root1.right, root2.right);
		return root1;
	}
}
```