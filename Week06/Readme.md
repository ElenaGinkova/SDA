## триене
```c
template <typename T>
void BinarySearchTree<T>::remove(const T& value) {
	root = _remove(root, value);
}

template <typename T>
Node<T>* BinarySearchTree<T>::_remove(Node<T>* current, const T& value) {
	if (!current) {
		return nullptr;
	}

	if (value < current->value) {
		current->left = _remove(current->left, value);
	}
	else if (current->value < value) {
		current->right = _remove(current->right, value);
	}
	else {
		if (!current->left && !current->right) {
			return nullptr;
		}
		if (!current->left) {
			return current->right;
		}
		if (!current->right) {
			return current->left;
		}

		Node<T>* iter = current->right;
		while (iter->left) {
			iter = iter->left;
		}

		current->value = iter->value;
		current->right = _remove(current->right, current->value);
	}

	return current;
}
```
## Depth search
```c
template <typename T>
void BinarySearchTree<T>::inorder(const Node<T>* current) const {
	if (!current) {
		return;
	}

	inorder(current->left);
	std::cout << current->value << " "; // 0 2 3 4 5 8 
	inorder(current->right);
}
```
```c
template <typename T>
void BinarySearchTree<T>::iterativeDfs() const { // inorder
	std::stack<Node<T>*> stack;
	Node<T>* current = root;

	while (current != nullptr || !stack.empty()) {
		while (current != nullptr) {
			stack.push(current);
			current = current->left;
		}

		current = stack.top();
		stack.pop();
		std::cout << current->value << " ";
		current = current->right;
	}
}
```
## Breadth search
```c
template <typename T>
void BinarySearchTree<T>::bfs() const {
	std::queue<Node<T>*> container;
	container.push(root);

	while (!container.empty()) {
		size_t levelSize = container.size();
		while (levelSize > 0) {
			Node<T>* current = container.front();
			container.pop();

			if (current) {
				std::cout << current->value << " ";
				container.push(current->left);
				container.push(current->right);
			}
			levelSize--;
		}
		std::cout << std::endl;
	}
}
```
## validate
```c
bool _BST(TreeNode* root, long minn, long maxx) {
        if(!root) return true;

        if(root->val <= minn || root->val >= maxx) return false;

        return _BST(root->left, minn, root->val) && _BST(root->right, root->val, maxx);
    }
    bool isValidBST(TreeNode* root)
    {
        return _BST(root, LONG_MIN, LONG_MAX);
    }
```
```c
void dfs(TreeNode* root, vector<int>& v)
    {
        if(!root) return;

        dfs(root->left, v);
        v.push_back(root->val);
        dfs(root->right, v);
    }
    bool isValidBST(TreeNode* root) {
        vector<int> order;
        dfs(root, order);

        for(int i = 1; i < order.size(); i++)
        {
            if(order[i - 1] >= order[i]) return false;
        }
        return true;
    }
```
### inorder - left, root, right
### postorder - left, right, root
### preorder - root, left, right
### levelorder
```c
vector<vector<int>> levelOrder(TreeNode* root) {//bfs
        if(!root) {
            return {};
        }
        vector<vector<int>> v;
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty())
        {
            int size = q.size();
            vector<int> lv;
            for(int i = 0; i < size; i++)
            {
                TreeNode* curr = q.front(); q.pop();
                lv.push_back(curr->val);
                if(curr->left) q.push(curr->left);
                if(curr->right) q.push(curr->right);
            }
            v.push_back(lv);
        }
        return v;
    }
```
