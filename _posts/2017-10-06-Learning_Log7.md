---
layout: post
title:  "Learning Log 7"
date:   2017-10-06
categories: C++ Python Leetcode
image:  /preview.jpg
---

### Binary Search Tree (BST)

In a BST or ordered binary tree, 
- the left subtree of a node contains only nodes with keys less than the node's key;
- the right subtree of a node contains only nodes with keys greater than the node's key;
- both the left and right subtrees must also be binary search trees
- inorder traversal will output an ordered list in ascending order

(reference) [https://www.laurentluce.com/posts/binary-search-tree-library-in-python/comment-page-1/]

```python
class Node():
    
    def __init__(self, value):
        self.left = None
        self.right = None
        self.val = value
        
    
    # insert method
    def insert(self, value):
        if value < self.val:
            if self.left is None:
                self.left = Node(value)
            else:
                self.left.insert(value)
        elif value > self.val:
            if self.right is None:
                self.right = Node(value)
            else:
                self.right.insert(value)
        else:
            self.val = value
            
    # lookup, return the node and node's parent
    def lookup(self, value, parent = None):
        if value < self.val:
            if self.left is None:
                return None, None
            return self.left.lookup(value, self)
        
        elif value > self.val:
            if self.right is None:
                return None, None
            return self.right.lookup(value, self)
        
        else:
            return self, parent
        
    # children counts, helper function for delete
    def children_count(self):
        cnt = 0
        if self.left:
            cnt += 1
        if self.right:
            cnt += 1
        return cnt
        
    # delete
    def delete(self, value):
        node, parent = self.lookup(value)
        if node is not None:
            children_count = node.children_count()
            
            # case 1, the node has no children
            if children_count == 0:
                if parent:
                    if parent.left is node:
                        parent.left = None
                    else:
                        parent.right = None
                    del node
                else:
                    self.val = None
                    
            # case 2, the node has one children, replace the node with its child
            elif children_count == 1:
                if node.left:
                    n = node.left
                else:
                    n = node.right
                    
                if parent:
                    if parent.left is node:
                        parent.left = n
                    else:
                        parent.right = n
                    del node
                else:
                    self.left = n.left
                    self.right = n.right
                    self.val = n.val
                    
            # case 3, the node has two children
            # use the left leaf node of the immediate right subtree to replace the node
            else:
                parent = node
                successor = node.right
                while successor.left:
                    parent = successor
                    successor = successor.left
                
                node.val = successor.val
                if parent.left == successor:
                    parent.left = successor.right
                else:
                    parent.right = successor.right
                    
    # print, inorder print will give an ordered list
    def print_tree(self):
        # inorder print
        if self.left:
            self.left.print_tree()
        print(self.val)
        if self.right:
            self.right.print_tree()
                
    # compare 2 trees
    def compare_tree(self, node):
        if node is None:
            return False
        if self.val != node.val:
            return False
        res = True
        if self.left is None:
            if node.left:
                return False
        else:
            res = self.left.compare_tree(node.left)
        if res is False:
            return False
        if self.right is None:
            if node.right:
                return False
        else:
            res = self.right.compare_tree(node.right)
        return res

    # generator returning the tree elements one by one
    def tree_data(self):
        stack = []
        node = self
        while stack or node:
            if node:
                stack.append(node)
                node = node.left
            else:
                node = stack.pop()
                yield node.val
                node = node.right
```


