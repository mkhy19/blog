
![Alt Stack](https://i.imgur.com/c1wSp4O.png "trees 2")
## Before you start reading it, We have discussed intro about tree and binary search tree [here](https://mohamedkhaledyousef.github.io/Trees-Data-Structure-Part-1/)

We're going to continue talking about trees. And in particular, look at walking a tree, or visiting the elements of a tree, or traversing the elements of a tree. So often we want to go through the nodes of a tree in a particular order.  
We talked earlier, when we were looking at the syntax tree of an expression, how we could evaluate the expression by working our way up from the leaves. So that would be one way of walking through a tree in a particular order so we could evaluate. Another example might be printing the nodes of a tree. If we had a binary search tree, we might want to get the elements of a tree in sorted order. 

### There are two main ways to traverse a tree. 
* **Depth-first**: So there, we completely traverse one sub-tree before we go on to a sibling sub-tree.
* **Breadth-first**: We traverse all the nodes at one level before we go to the next level. So in that case, we would traverse all of our siblings before we visited any of the children of any of the siblings

***


#### Today, I am going to discuss DFS... DFS can be traversed in different ways (In Order, Pre Order and Post Order)

### 1 - In Order Traversal

**InOrderTraversal(tree) algorithm**
```
if tree = nil:
    return
InOrderTraversal(tree.left)
Print(tree.key)
InOrderTraversal(tree.right)
```
So, we're going to have a recursive implementation
1-where if we have a nil tree, we do nothing
2-otherwise,
* We traverse the left sub-tree, 
* And then do whatever we're going to do with the key, visit it, in this case, we're going to print it. But often there's just some operation you want to carry out
* And then traverse the right sub-tree.

So let's look at an example of this.  
![Alt Stack](https://i.imgur.com/OKQy6vI.png "in order")

**We've got our binary search tree. And we're going to look at how these nodes get printed out if we do an in-order traversal. So to begin with:**
* We go to the Les node. And from there, since it's not nil, we're going to do an in-order traversal of its left child, which is Cathy. Similarly now we're going to do an in-order traversal of its left child, which is Alex. Also we do an in-order traversal of its left child which is nil, so it does nothing. So we come back to Alex, and then print out Alex
* And then traverse its right sub-tree which is nil and does nothing. We come back to Alex. And then we're finished with Alex and we go back to Cathy. So, we have successfully completed Cathy's left sub-tree.
* So we did an in-order traversal of that, so now we're going to print Cathy
* And then do an in-order traversal of its right sub-tree, which is Frank. 
So we go to Frank, similarly now we're going to print out Frank.
* We've finished with Frank and go back to Cathy, and now we've completed Cathy totally, so we go back to Les.
* We completed Les' left sub-tree, so we're now going to print Les and then traverse Les' right sub-tree. 
* So that is Sam, traverse its left sub-tree which is Nancy. Print it out
* Go back to Sam, we've completed Sam's left sub-tree, so we print Sam
* And then go ahead and do Sam's right sub-tree which is Violet, which will end up printing Tony, Violet, and then Wendy. 
* We're completed with Wendy. We go back to Violet. We completed her right sub-tree, so we go back to Sam, completed his right sub-tree, go back to Les, completed his right sub-tree, and we're done. 


**So we see we get the elements out in sorted order.**  
And again, we do the left child. And then the node and then the right child. And by our definition of a binary search tree, that gives them to us in order because we know all the elements in the left child are in fact less than or equal to the node itself.

Here is the code in C++
```C++
void printInOrderTraversal(struct node* node)
{
     if (node == NULL)
          return;

     //Check the left, recur on left child
     printInOrderTraversal(node->left);

     //then print the data of node
     cout<<node->data<<" ";

     //then check the right, recur on right child
     printInOrderTraversal(node->right);
}
```
***
### 2 - Pre Order Traversal
**The next depth-first traversal is a pre-order traversal. But we have to know why we use pre-order and post-order traversal?**
* Now the in-order traversal really is only defined for a binary tree because we talk about doing the left child and then the node and then the right child. 
* And so it's not clear if you had let's say three children, where it is you'd actually put the node itself. So you might do the first child and then print the node, and then second and third child. Or first child and then second child and print the node, and then third child. It's kind of undefined then, so not well-defined. 
* However, these next two, the pre-order and post-order traversal are well defined. Not just for binary trees, but for general, arbitrary number of children trees. 

**PreOrderTraversal(tree)algorithm**
```
if tree = nil:
    return
Print(tree.key)
PreOrderTraversal(tree.left)
PreOrderTraversal(tree.right)
```
So let's look at an example of this. 
![Alt Stack](https://i.imgur.com/sMI7qai.png "pre order")

**So here the pre-order traversal says, we're going to go ahead first if it's nil we return. We print the key first, that is, we visit the node itself and then its children.** 
* So we're going to, in this case, go ahead and go to the Les tree and then print out its key and then go to its children. 
* So we're going to first go to its left child which is Cathy, and for Cathy, we then print Cathy
* and then go to its left child which is Alex, print Alex, we go back to Cathy. And we finished its left child
* so then we go do its right child, which is Frank. 
* We finished Frank. We finished Cathy. We go back up to Les. We've already printed Les. We've already visited or traversed Les' left child. 
* Now we can traverse Les' right child, so it'll be Sam, which we'll print out. 
* And then we'll go to Nancy, which we'll print out 
* we'll go back up to Sam and then to Violet, and we will print Violet, 
* and then print Violet's children, which will be Tony and Wendy and then return back.

Here is the code in C++
```C++
void printPreorderTraversal(struct node* node)
{
     if (node == NULL)
          return;

     //print data of node
     cout<<node->data<<" ";

     //then check the left, recur on left sutree
     printPreorderTraversal(node->left);

     //then check the right, recur on right subtree
     printPreorderTraversal(node->right);
}
```
***
### 3 - Post Order Traversal
A post-order traversal is like a pre-order traversal expect instead of printing the node itself first, which is a pre, we print it last, which is the post. 
So all we've really done is move where this print statement is. 

**PostOrderTraversal(tree)algorithm**
```
if tree = nil:
    return
PostOrderTraversal(tree.left)
PostOrderTraversal(tree.right)
Print(tree.key)
```
So let's look at an example of this. 
![Alt Stack](https://i.imgur.com/eVU2m7q.png "post order")

And here then, **what's the last of these notes that's going to be printed??**  
Well it's actually going to be **Les**, because we're not going to be able to print Les until we've finished 

* Completely dealing with Les' left sub-tree and right sub-tree. So we'll visit Les, and then visit Cathy, and then Alex, and then we'll actually print out Alex. 
* Once we're done with Alex, we'll go back up to Cathy and down to Frank, and then print out Frank
* and then once we're done with both Alex and Frank we can then print Cathy. 
* We go back up to Les, and we now need to go deal with Les' right child which is Sam. 
* In order to deal with Sam we go to Nancy, print Nancy
* then go back up to Sam and down to Violet, and deal with the Violet tree, which will print out Tony, and then Wendy, and then Violet. 
* And on our way back up, then, when we get up to Sam, we have finished its children, so we can print out Sam. 
* When we get up to Les, we've finished its children, so we can print out Les.

**One thing to note about the recursive traversal is we do have sort of under the covers, a stack that's being used. Because in a recursive call, every time we make a call back to a procedure, we are invoking another frame on the stack. So we are saving implicitly our information of where we are on the stack.**

Here is the code in C++
```C++
void printPostorderTraversal(struct node* node)
{
     if (node == NULL)
        return;

     // first check the left, recur on left sutree
     printPostorderTraversal(node->left);

     // then check the right,recur on right subtree
     printPostorderTraversal(node->right);

     //print data of node
     cout<<node->data<<" ";
}
```
### Finally … [Here](https://github.com/mohamedkhaledyousef/Crash-courses/blob/master/Trees/DFS.cpp) is full example in the repo, And you can find all source code in c++.

#### Next, I am going to discuss BFS.
