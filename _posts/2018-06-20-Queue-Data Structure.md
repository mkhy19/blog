
![Alt Stack](https://github.com/mohamedkhaledyousef/Crash-courses/blob/master/img/queue.jpeg?raw=true "queue")
## Queue is data structure like array and stack. But here the first element added to the queue, will be the first element removed from the queue. So queue called first in first out (FIFO) or first come first serve


We can in queue:  
**Enqueue(Key):** To add key to collection  
**Key Dequeue():** To remove and return least recently-added key  
**Boolean Empty():** Means, Are there any elements?  

Queue implementation:  
**We can implement queue in several way (Linked list, Array, 2 Stack).**

Queue implementation with linked list: There two things we must to know,   
**The first** : When we enqueue, we are going to push to the back of the linked list  
**The second** : To make sure the the queue list is empty , we make sure if the head is null or not  

Here the code using linked list:
```c++
//QUEUE USING LINKED LIST

#include <bits/stdc++.h>
#include<conio.h>

using namespace std;

//Create a NODE
struct node
{
   int data;
   struct node *next;
};

//Create a class 
class myQueue
{
   struct node *front,*tail;

   public:
       // constructure
        myQueue()
        {
            front=tail=NULL;
        }

        //declaration
        void Enqueue(int x);     // to insert an element
        void Dequeue();     // to delete an element
        void Display();     // to show the stack
};

//Definition

//Enqueue
void myQueue::Enqueue(int x)
{
   int value;
   struct node *newNode;

   cout<<"Enter a number to enqueue in queue: ";
   cin>>value;

   newNode=new node;
   newNode->data=value;
   newNode->next=NULL;
   if(front==NULL)
      front=newNode;
   else
      tail->next=newNode;
   tail=newNode;
}

// Dequeue
void myQueue::Dequeue()
{
   if(front==NULL)
   {
      cout<<"Queue is empty"<<endl;
      return;
   }

   struct node *temp;
   temp=front;
   front=front->next;
   cout<<temp->data<<" removed from the queue "<<endl;
   delete temp;
}

// Show Queue
void myQueue::Display()
{
   struct node *ptr1=front;
   if(front==NULL)
   {
      cout<<"The Queue is empty!!";
      return;
   }

   cout<<endl;
   cout<<"The Queue is : "<<endl;
   cout<<"front->";
   while(ptr1!=NULL)
   {
      cout<<ptr1->data<<" ->";
      ptr1=ptr1->next;
   }
   cout<<"tail"<<endl;

}

// Main function
int main()
{
    myQueue q;

		//take care, we can ignore those numbers in function and make it as you want.
		//if you want to print the same output, ignore value variable fron enqueue method and only use x
		
    q.Enqueue(5);   //5
    q.Enqueue(6);   //5 6
    q.Enqueue(8);   //5 6 8
    q.Enqueue(10);  //5 6 8 10
    q.Display();    //5 6 8 10
    q.Dequeue();    //6 8 10
    q.Display();    //6 8 10
    q.Dequeue();    //8 10
    q.Display();    //8 10
    q.Enqueue(7);   //8 10 7
    q.Display();    //8 10 7

   return 0;

}

``` 

Queue implementation with array:
**It’s easy to implement queue using array but pay attention in this case.**  
When we want to enqueue(g) maybe causes error!! WHY??  
This case occurred when we have array say with size (5) but this array have (4) occupied by values

**Here example:**
![Alt Stack](https://github.com/mohamedkhaledyousef/Crash-courses/blob/master/img/enqueue.png?raw=true "enqueue") 

if we did enqueue(g), The read and write would be both 2  
* And it would be hard to distinguish read and write index 2 because the queue is full
* Or read and write index both 2 because the queue is empty
* So we have a buffer of at least one that can’t be written to make sure read and write are separate and and distinct if the queue isn’t empty

**Notice:**
one distinction between the array and linked list implementation is that in the array implementation we have a maximum size that the queue can grow to so it is bounded

Here the code using array:
```c++
//Using Array

#include <iostream>

using namespace std;

// Constants
#define max 20

// Functions
int menu();

// Stack functions
void enqueue();
void dequeue();
int front();
bool isFull();
bool isEmpty();

// Variables
int queue[max];
int frontElement = 0;
int rearElement = 0;

int main()
{

    int choice;

    do
    {
        choice = menu();

        switch(choice)
        {
            case 1:
                enqueue();
                break;
            case 2:
                dequeue();
                break;
            case 3:
                front();
                break;
            case 4:
                isFull();
                break;
            case 5:
                isEmpty();
                break;
            case -1:
                choice = -1;
                break;

            default:
                cout<<"\nEnter a valid choice!!"<<endl;
        }
    }
    while(choice != -1);
}

int menu()
{
    int ch;

    cout<<"\nQueue using Array"<<endl;
    cout<<"\n1.Enqueue\n2.Dequeue\n3.Front element\n4.Is Full\n5.Is Empty\n6.Exit"<<endl;
    cout<<"\nEnter your Choice:"<<endl;
    cin>>ch;

    return ch;
}

void enqueue()
{
    if(rearElement == max)
    {
        cout<<"\nOverflow"<<endl;

    }
    else
    {
        int element;
        cout<<"\nEnter Element:"<<endl;
        cin>>element;
        cout<<"\nElement "<<element<<" has been pushed at : "<<rearElement<<endl;
        queue[rearElement] = element;
        rearElement++;
    }
}

void dequeue()
{
    if(rearElement == 0)
    {
        cout<<"Queue is empty."<<endl;

    }
    else
    {
        if(frontElement == rearElement) //empty queue or error
        {
            frontElement = 0;
            rearElement = 0;
        }

        cout<<"Dequeued element is "<<queue[frontElement]<<endl;
        frontElement ++;
    }
}

int front()
{
    cout<<"\nTop number is "<<queue[frontElement]<<endl;

    return queue[frontElement];
}

bool isFull()
{
    if(rearElement == max -1)
    {
        cout<<"true"<<endl;
        return true;

    }
    else
    {
        cout<<"false"<<endl;
        return false;
    }
}

bool isEmpty()
{
    if(rearElement == 0)
    {
        cout<<"true"<<endl;
        return true;

    }
    else
        {
        cout<<"false"<<endl;
        return false;
    }
}
``` 
 
Queue time complexity:  
Cost for doing a dequeue and enqueue , all are O(1). And there is no “worst case”

Finally … [Here](https://github.com/mohamedkhaledyousef/Crash-courses/tree/master/Queue) you can find how to implement queue using 2 stack and all source code in c++ 



