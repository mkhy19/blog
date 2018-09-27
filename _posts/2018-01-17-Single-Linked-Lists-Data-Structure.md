![alt text](https://i.imgur.com/4lnxYxI.jpg "Linked List")
## linked list is a data structure that having a list of elements and each element has a reference pointing to the next element in the list.

**First thing we have to know about linked list is we have a head pointer that points to a node that then has some date and points to another node and so on till a node that dose not point to any farther.
And node contains 2 elements ,the value or the key (number like 7) and a pointer that points to the next node that contain (another number like 10 for example)**

7 →10

## There are operations that can be done on linked list called List API  
**1. On the front of the list:**  
* PushFront(key): add to front  
* Key TopFront(): return the front element  
* PopFront(): remove the front element  

**2. On the end of the list**  
* PushBack(key): add to back … also known a Append  
* Key TopBack(): return the back element  
* PopBack(): remove the back element  
There is difference between the front and back operation in run time  

**3. We can also do:**  
* Boolean Find(Key): is key in a list?  
* Erase(Key): remove key from list  
* Boolean Empty(): empty list?  
* AddBefore(Node,Key): adds key before Node  
* AddAfter(Node,Key): adds key after Node  

## Example:
**We have an empty list ,do this following operations:**  
PushBack(a);  
PushFront(b);  
PushBack(d);  
PushFront(c);  
PopBack();  

**Solution:**  
PushBack(a); a  
PushFront(b); b a  
PushBack(d); b a d  
PushFront(c); c b a d  
PopBack(); c b a  
so,the final result is => c b a  

**The run time for some operations**  
PushFront(key): add to front in O(1)  
Key TopFront(): return the front element in O(1)  
PopFront(): remove the front element O(1)  
PushBack(key): add to back in O(n) without no tail  
PushBack(key): add to back in O(1) with tail  
Key TopBack(): return the back element in O(n) without tail  
Key TopBack(): return the back element in O(1) with tail  
PopBack(): remove the back element in O(n)  

## NOTEs::
**WHEN we want to push at the back?**  
1. If We don’t have a tail pointer, So this going to be expensive operation. **WHY?**  
Because we start at the head and walk our way down the list untill we get to the end and in the end we add a node so its going to be O(n). Similarly if we want to TopBack or PopBack  
2. If we had a tail pointer, some of this will become simpler. WHY? because we are going to have both a head pointer that points to the head element ,and tail pointer that points to the tail element. So the first element and the last element became cheap operations.  
**For example:**  
*When we have tail pointer and we want to insert element*  
* We first allocate a node and put in our new key  
* Then update the next pointer of the current tail to point to this new tail  
* Then update the tail pointer itself  
* And the run time will be O(1)  

**WHEN we have tail pointer and we want to delete or PopBack element:**  
* Here we don’t have pointer that points from the last element to the previous last (the element before)  
* We only have a pointer from the previous to the last element and that pointer does not help us going back  
* So what we have got to do is:  
  1. We start from the head and walk our way down until we find the previous last element or node that points to the current tail (last element)  
  2. Then update our tail pointer to point to that (previous last element)  
  3. Then update the tail pointer to be null, this means tail pointer points to the previous last element which it became the tail element  
  4. Then we can remove the last element  
  5. And the final run time will be O(n) Because we have got to walk all the way down  

___

## Single Linked list algorithm
**PushFront**
```
node <- new node 
node.next <- head 
head <- node 
if tail = nil: //an empty list 
    tail <- head
```

**PopFront**
```
if head = nil:
    ERROR: empty list
head <- head.next
if head = nil:
    tail <- nil
```

**PushBack**
```
node <- new node 
node.key <- key 
node.next = nil 
if tail = nil; 
    head <- tail <- node
else: 
    tail.next <- node, 
    tail <- node
```

**PopBack**
```
if head = nil : 
    ERROR: empty list
if head = tail
    head <- tail <- nil
else 
    p <- head
    while p.next.next != nil:
         p <- p.next
    p.next <- nil;
    tail <- p
```

**Add after a node: AddAfter(node,key)**
```
node <- new node
node.key <- key
node.next = node.next
node.next = node
if tail = node: //one element in list and this is the same node that we want to add key after that
    tail <- node
```

**Adding before have the same problem we had with Pop back that we don’t have a link back to the previous element so AddBefore would be an O(n)**

## Here you can find all main operations that we can do on single linked list:
```c++
#include<iostream>
using namespace std;

//built node .... node = (data and pointer)
struct node     
{
    int data;   //data item
    node* next; //pointer to next node
};

//built linked list
class linkedlist
{
    private:
        node* head;
    public:
        linkedlist()    //constructor
        {
            head=NULL;  //head pointer points to null 
        }
        void addElementFirst(int d);           
        void addElementEnd(int d);         
        void addElementAfter(int d,int b);    
        void deleteElement(int d);
        void display();                    
};

//Push front code
void linkedlist::addElementFirst(int d)
{
    node* newNode=new node;        
    newNode->data=d;               
    newNode->next=head;            
    head=newNode;                   
}

//Push back code
void linkedlist::addElementEnd(int x)
{
    node* newNode=new node;    
    node* temp=new node;        
    temp=head;                 
    newNode->data=x;     
    if(temp==NULL)             
    {
        newNode->next=NULL;
        head=newNode;
        return;             
    }

    while(temp->next!=NULL)
    {
        temp=temp->next;      
    }

    newNode->next=NULL;       
    temp->next=newNode;        
}

//head->10->5->8->NULL
//if d=5,key=2
//head->10->5->2->8->NULL
void linkedlist::addElementAfter(int d,int key)    
{
    node* search=new node;   
    search=head;              
    while(search!=NULL)      
    {
        if(search->data==d)  
        {
            node* newNode=new node; 
            newNode->data=key;      
            newNode->next=search->next;   
            search->next=newNode;         
            return;
        }
        search=search->next;
    }

    if(search==NULL)  
        cout<<"The link not inserted because there is not found the node "<<d<<" in the LinkedList. "<<endl;
}

void linkedlist::deleteElement(int d)
{
    node* del;  
    del=head;  
    if(del==NULL)  
    {
        cout<<"Linked list is empty"<<endl;
        return;   
    }
    
    if(del->data==d)    
    {
        head=del->next; 
        return;
    }
    
    if(del->next==NULL) 
    {
        cout<<"Is not here, So not deleted."<<endl;
        return;
    }
    
    //if here more one nodes...one node points to another node ... bigger than 2 nodes .. at least 2 nodes
    while(del->next!=NULL)
    {
        if(del->next->data==d)
        {
            del->next=del->next->next;
            return;
        }

        del=del->next;
     }

     cout<<"Is not here, So not deleted."<<endl;
}

//void linkedlist::display(node *head)
void linkedlist::display()
{
    int n=0;             //counter for number of node
    node* current=head;  //current is pointer points to where head point
    if (current==NULL)
        cout<<"This is empty linked list."<<endl;
        
    while(current!=NULL) //until current reach to null(last element)
    {
        cout<<"The node data number "<<++n<<" is "<<current->data<<endl;  
        current=current->next;
    }
    
    cout<<endl;
}

int main()
{
    linkedlist li;      //li is object from linkedlist class
    li.display();       //empty list
    li.addElementFirst(25);  //head->25->NULL
    li.addElementFirst(36);  //head->36->25->NULL
    li.addElementFirst(49);  //head->49->36->25->NULL
    li.addElementFirst(64);  //head->64->49->36->25->NULL
    cout<<"After adding in the first of linked list"<<endl;
    li.display();
        //64
        //49
        //36
        //25
    cout<<endl;
    //head->64->49->36->25->NULL //current linked list from prev addElementFirst method

    cout<<"After adding in the end of linked list"<<endl;
    li.addElementEnd(25);  //head->25->NULL
    li.addElementEnd(36);  //head->25->36->NULL
    li.addElementEnd(49);  //head->25->36->49->NULL
    li.addElementEnd(64);  //head->25->36->49->64->NULL
    li.display();
    //head->64->49->36->25->25->36->49->64->NULL
    cout<<endl;
    
    //head->64->49->36->25->25->36->49->64->NULL
    cout<<"linked list after adding 10 after node that has data = 49"<<endl;
    li.addElementAfter(49,10);
    li.display();
    //head->64->49->10->36->25->25->36->49->64->NULL
    //head->64->49->10->36->25->25->36->49->64->NULL
    cout<<"linked list after adding deleting 49"<<endl;
    li.deleteElement(49);
    li.display();
    //head->64->10->36->25->25->36->49->64->NULL
    //Notice :delete the first 49 ... not permission for duplicates
    return 0;
}
```

### Last thing to say, Thanks for reading and I hope it would help and don’t hesitate to send your feedback and suggestions :))
## Source code in C++ [here](https://github.com/mohamedkhaledyousef/Crash-courses/blob/master/LinkedLists/Single%20Linked%20Lists/main.cpp)










