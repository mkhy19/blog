
## Binary search tree is a very common type of a tree used in computer science. 
![Alt Stack](https://i.imgur.com/Po3en7B.png "trees 1")

The binary search tree (BST) is defined by the fact that it's binary, so that means it has at most two children at each node. And we have the property that at the root node, the value of that root node is greater than or equal to all of the nodes in the left child, and it's less than the nodes in the right child.  
 ![Alt Stack](https://i.imgur.com/Iac1ASO.jpg "example")


### In this example
Here less than or greater than, we're talking about alphabetically not numerically. So Les is greater than Alex, Cathy, and Frank, but is less than Nancy, Sam, Violet, Tony, and Wendy. And then that same thing is true for every node in the tree has the same thing.  
**For instance**, Violet is greater than or equal to Tony and strictly less than Wendy.  

### Why using BST?
**The binary search tree allows you to search quickly.**  
For instance:  
* if we wanted to search in this tree for Tony, we could start at Les. 
* Notice that Tony is greater than Les, so therefore, we're going to go right.
* Notice that Tony is greater than Sam so we'll go right. 
* Notice that Tony is less than Violet so we'll go left and then we find Tony. 

And we do that in just four comparisons. And it's a lot like a binary search in a sorted array. So the actual definition of a tree is...
**A tree is either empty or it's a node that has a key and it has a list of child trees .... This is a recursive definition.**

So if we go back to our example here:
* Les is a node that has the key Les and two child trees, the Cathy child tree and the Sam child tree. 
* The Cathy child tree is a node with a key Cathy and two child trees, the Alex child tree and the Frank child tree. 
* Let's look at the Frank child tree. It's a node with a key Frank and two, well, does it have any child trees ?????? No, it has no child trees. 

### Let's look at some other terminology for trees.
![Alt Stack](https://i.imgur.com/I07SBz8.png "example")
 
* **Root**: is the top node in the tree so here, Fred is the root of the tree.
* **A child**: has a line down directly from a parent, Kate is a parent of Sam, and Sam is a child of Kate. 
* **The children** of Fred are Kate, Sally, and Jim.
* **An ancestor** : is a parent or parent's parents and so on. So Sam's ancestors are Kate and Fred. Hugh's ancestors are also Kate and Fred. Sally's ancestors are just Fred. 
* **The descendant** is an inverse of the ancestor, so it's the child or child of child and so on. So the descendants of Fred are all of the other nodes since it's the root, Sam, Hugh, Kate, Sally and Jim. The descendants of Kate would just be Sam and Hugh. 
* **Sibling** is two nodes sharing the same parent, so Kate, Sally and Jim are all siblings. Sam and Hugh are also siblings. 
* **A leaf** is a node that has no children. So that's Sam, Hugh, Sally, and Jim. 
* **An interior node (non-leaf)** : are all nodes that aren't leaves. So this is Kate and Fred ... Another way to describe it is all nodes that do have children. 

* **A level** : 1 plus the number of edges between the root and a node, 
1- let's think about that. Fred, how many edges are there between the root and the Fred node??? Well, since the Fred node is the root, there are no edges. So its level would be 0+1=1. 
2- Kate has one edge between Fred and Kate, so its level would be 1+1=2, along with its siblings, Sally and Jim. 
3- And Sam and Hugh are level 3.

* **The height** : the maximum depth of the subtree node in the farthest leaf
1- so here we want to look, for instance, if we want to look at the height of Fred, we want to look at what is its farthest down descendant. 
And so its farthest down descendant would either be Sam or Hugh. 
And its height would be 3. 
2- So the leaf (Sam or Hugh) heights are 1. 
3- Kate has height 2. 
4- Fred has height 3. 

* **Forest** : We also have the idea of a forest. So it's a collection of trees.. So we have here two trees with a root Kate and a root Sally, and those form a forest.
 
![Alt Stack](https://i.imgur.com/q6aBy6l.png "Forest")


### Binary trees are very commonly used. 
So a binary tree has, at most, two children. Rather than having in this general list of children, for a binary tree, we normally have an explicit left and right child, either of which can be nil.  

### Let's look at a couple of procedures operating on trees. 
Since trees are recursively defined, it's very common to write routines that operate on trees that are themselves recursive.  
1. So for instance, if we want to calculate the height of a tree, that is the height of a root node:  
We can go ahead and recursively do that, going through the tree. So we can say:  
* For instance, if we have a nil tree, then its height is a 0. 
* Otherwise, We're 1 plus the maximum of the left child tree and the right child tree. 
* So if we look at a leaf for example, that height would be 1 because the height of the left child is nil, is 0, and the height of the nil right child is also 0. 
So the max of that is 0, then 1 plus 0. 

### Height(tree) algorithm
```
if tree = nil:
    return 0
return 1 + Max(Height(tree.left),Height(tree.right))
```
Here is the code in C++
```c++
int maxDepth(struct node* node)
{
    if (node==NULL)
        return 0;
   else
   {
       int rDepth = maxDepth(node->right);
       int lDepth = maxDepth(node->left);
       
       if (lDepth > rDepth)
       {
           return(lDepth+1);
       }
       else
       {
            return(rDepth+1);
       }
   }
}
```

2- We could also look at calculating the size of a tree that is the number of nodes. 
* Again, if we have a nil tree, we have zero nodes. 
* Otherwise, we have the number of nodes in the left child plus 1 for ourselves plus the number of nodes in the right child. So 1 plus the size of the left tree plus the size of the right tree.

### Size(tree) algorithm
```c++
if tree = nil
    return 0
return 1 + Size(tree.left) + Size(tree.right)
```
Here is the code in C++
```
int treeSize(struct node* node)
{
    if (node==NULL)
        return 0;
    else
        return 1+(treeSize(node->left) + treeSize(node->right));
}
```
### Finally … [Here](https://github.com/mohamedkhaledyousef/Crash-courses/blob/master/Trees/height-size-tree.cpp) is full example in the repo, And you can find all source code in c++.

#### Next, I am going to discuss if we want to visit the nodes of a tree in a particular order ... DFS and BFS.


