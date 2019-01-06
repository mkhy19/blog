![Alt Stack](https://i.imgur.com/MyTJYiN.png "trees 3")
## Before you start reading it, We have discussed intro about tree and binary search tree [here](https://mohamedkhaledyousef.github.io/Trees-Data-Structure-Part-1/) and also there is a blog about Depth-first-Search (DFS) [here](https://mohamedkhaledyousef.github.io/Depth-First-Search-(DFS)-Part-2/)

We're going to continue talking about trees. And in particular, look at walking a tree, or visiting the elements of a tree, or traversing the elements of a tree. So often we want to go through the nodes of a tree in a particular order.  
But here, We are going to talk about Breadth-first-Search (BFS)

## Breadth-first-Search (BFS)
* Here, we're going to actually use a queue instead of a stack. So in the breadth-first, we are going to call it level traversal here, we're going to go ahead and instantiate a queue.
* On the queue first put the root of the tree. So we put that in the queue 
* Then while the queue is not empty, we're going to dequeue, so pull a node off, deal with that by printing it.
* Then if it's got a left child, enqueue the left child.
* If it's got a right child, enqueue the right child. 
* And so this will have the effect of going through and processing the elements in level order.

**Breadth-first-Search (BFS) algorithm**
```
LevelTraversal(tree)
    if tree = nil: 
        return
    Queue q
    q.Enqueue(tree)
    while not q.Empty() :
        node ← q.Dequeue()
        Print(node)
        if node.left ̸= nil:
            q.Enqueue(node.left)
        if node.right ̸= nil:
            q.Enqueue(node.right)
```

So let's look at an example of this. 
![Alt Stack](https://i.imgur.com/FrHLqeU.png "Breadth First Search (BFS)")
 
We see the example here, and we're going to show the queue. 
* So here let's say we're just before the while loop, the queue contains Les. And we're going to now dequeue Les from the queue, output it by printing it.
* Then enqueue Les' children which are Cathy and Sam. 
* Now, we visit those in order, so first we're going to dequeue Cathy, print it out and then enqueue its children.
* **Remember when we're enqueuing we go at the end of the line, so Alex and Frank go after Sam.**
* So now we're going to dequeue Sam, print it, and then enqueue its children Nancy and Violet. 
* So we can see what we've done then is, we first printed Les, that's level one and then we printed the elements of level two, which are Cathy and Sam, and now we're going to go on to the elements at level three. 
* So notice, all the elements in level three, Alex, Frank, Nancy, and Violet are in the queue already. 
* And they're all going to be processed before any of the level four nodes are processed. So even though they'll be pushed in the queue, since the level three nodes got there first that they're all going to be processed before we process the level four ones. 
* So here, we dequeue Alex, print it out, and we're done. Dequeue Frank, print it out, we're done with Frank. Dequeue Nancy, print it out, we're done with Nancy. And Violet, we print it out, 
* But then also enqueue Tony and Wendy, and then dequeue those and print them out. 
* So this is a breadth-first search, with an explicit queue. 
* **NOTE:: You can do depth-first searches rather than recursively, iteratively, but you will need an additional data structure which is a stack to keep track of the work still to be done.** 

## Here is full example:
```C++
#include <bits/stdc++.h>

using namespace std;

struct node
{
    int data;
    struct node *left;
    struct node *right;
};

struct node* newNode(int data)
{
    node *temp = new node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

void printLevelTraversal(node *root)
{
    if (root==NULL)
        return;

    queue<node *> q;

    //Push Root
    q.push(root);

    while (q.empty()==false)
    {
        //Print the front of queue and remove it from the queue
        node *currNode = q.front();
        cout<<currNode->data<<" ";
        q.pop();

        //If this element have left child, Enqueue left child
        if (currNode->left!=NULL)
        {
            q.push(currNode->left);
        }

        //If this element have right child, Enqueue right child
        if (currNode->right!=NULL)
        {
            q.push(currNode->right);
        }
    }
}


int main()
{
    /*
        1
       / \
      2   3
     / \
    4   5
    //1 2 3 4 5
    */

    node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);

    cout<<"Breadth-first-Search (BFS): Level Order traversal of binary tree is "<<endl;
    printLevelTraversal(root);

    return 0;
}
```
### Finally … [Here](https://github.com/mohamedkhaledyousef/Crash-courses/blob/master/Trees/BFS.cpp) is the repo, You can find all source code in C++.

