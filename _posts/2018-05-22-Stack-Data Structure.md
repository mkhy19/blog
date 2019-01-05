![alt text](https://github.com/mohamedkhaledyousef/Crash-courses/blob/master/img/stack.jpeg?raw=true "Stack")
## A stack is a data structure that occasionally known as LIFO (Last In First Out), meaning that the last element added to the stack must be the first element removed from it.

The simplest way to understand stack, Box of books. We add the first one on bottom then the next on top and so on. If we want to choose any one, we should remove all books above it. for example if we want to get the last book in the box, we will remove all books on top of this book.

By stack we can:  
Push(Key) : adds key to collection  
Key Top() : returns the most recently added key  
Key Pop() : removes and returns most recently added key  
Boolean Empty() : are there any elements?????  


Here stack implementation using STL :
```c++
#include <iostream>
#include <stack>

using namespace std;

void printStack(stack <int> myStack)
{
    stack <int> s= myStack;
    while (!s.empty())
    {
        cout<< s.top()<<endl;
        s.pop();
    }
    cout <<endl;
}

int main ()
{
    stack <int> st;
    st.push(10);
    st.push(20);
    st.push(30);
    st.push(40);
    st.push(50);

    cout << "The stack st is : "<<endl;
    printStack(st);

    cout << "the stack size : " << st.size()<<endl;
    cout << "the stack top : " << st.top()<<endl;


    cout << "After pop element : "<<endl;
    st.pop();    
    printStack(st);

    return 0;
}
``` 

Last thing to say, One of the application of a stack is Balanced Brackets  
Here the problem:  
Input : A string str consisting of ‘(‘ , ‘)’ , ‘[‘ , ‘]’ characters  
Output: returns whether or not the string’s parentheses and square brackets balanced  

For examples:  
Balanced like this:  
“ ([]) “  
“ ((([([])]))()) “  
Unbalanced like this:  
“ ([]]() “  
“ ][ “  

Algorithm  
```
IsBalanced(str )
 Stack stack //create stack
 for char in str: //for every character in string
    if char in [‘(‘, ‘[‘]:
        stack.Push(char ) 
    else:
        if stack.Empty(): //means false ,not matches
            return False
        top <- stack.Pop()
        if (top = ‘[‘ and char != ‘]’) or (top = ‘(‘ and char != ‘)’):
            return False //dont match
 return stack.Empty()
```

Here the code :
```c++
#include <bits/stdc++.h>

using namespace std;

bool isBalanced(string s) 
{
    vector<char> openingBracketsStack; 
    
    for(int i=0; i<s.size() ;++i) 
    {
        if(s[i]=='{' || s[i]=='[' || s[i]=='(') 
        {
            openingBracketsStack.push_back(s[i]);
        } 
        
        else 
        {
            // Pop the top of the stack and make sure the brackets match
            if(openingBracketsStack.size()==0)    //empty stack
            {
                return false;
            }

            char top=openingBracketsStack.back();
            openingBracketsStack.pop_back();
            if(top=='{' && s[i]!='}') 
            {
                return false;
            }
            if(top=='(' && s[i]!=')') 
            {
                return false;
            }
            if(top=='[' && s[i]!=']') 
            {
                return false;
            }
        }
    }

    if(openingBracketsStack.size()==0) 
    {
        return true;
    } 
    else 
    {
        return false;
    }
}

int main()
{
    int t;
    cin >> t;
    for(int a= 0; a<t; ++a)
    {
        string s;
        cin>>s;

        bool result = isBalanced(s);
        
        if(result)
            cout << "YES"<<endl;
        else 
            cout << "NO"<<endl;
    }
    return 0;
}
```

You must know that:
1. Stacks are used for compilers and a lot of algorithms
2. We can also implement stack with linked list
  * One disadvantage is one limitation of the array is that we have maximum size base on the array that we initially allocated
  * The other potential problem is that we have potentially wasted space, So if we allocated a very large array to allow possibly large stack and we did not actually use much of it …. all the rest of it is wasted
  * We can keep pushing and the nice thing about this is there is no priority limit as to the number of elements you can add
  * As long as you have available memory ,you can keep adding
  * There is an overhead though like in the array ,we have each element size is just enough to store our key
  * There we have got the overhead of storing a pointer as well and on the other hand there is no wasted space in terms of allocated space that is not actually being used
  * You can see how to implement stack using linked list [here](https://github.com/mohamedkhaledyousef/Crash-courses/blob/master/Stack/StackAndLinkedList.cpp) 
3. Stacks are known as LIFO (Last In First Out) or GIGO (Garbage In Garbage Out)

Last thing to say, Thanks for reading and I hope it would help and don’t hesitate to tell me your feedback and suggestions :))
All source codes in c++ in this [repo](https://github.com/mohamedkhaledyousef/Crash-courses/tree/master/Stack) 






