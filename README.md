\\Hashing With Chaining

#include<iostream>
#include<cstdlib>
#include<string>
#include<cstdio>
using namespace std;

class node
{
    public:
int data;
node *next;
node( int val)
 {
  data = val;
  next = NULL;
 }
};
class linklist
{
  node *head;
  public:
 linklist()
  {
   head = NULL;
  }
  void InsertAtTail(int val)
 {
     node *mynode=new node(val);
     if(head==NULL)
     {
         head=mynode;
     }
   else{
        node *temp=head;
     while(temp->next!=NULL)
     {
       temp= temp->next;
     }
   temp->next=mynode;
 }
 }
 void searching(int val)
{
    if(head==NULL)
    {
        cout<<"No node exists";
    }
    else
    {
        node *temp=head;
        while(temp!=NULL)
        {
            if(temp->data==val)
            {
                cout<<val<<" exists\n";
            }

        temp=temp->next;
        }
    }
}
void deletion(int val)
{
    if(head==NULL)
    {
        cout<<"No node exist";
    }
    else
    {
        node *temp=head,*temp1=head;
        while(temp->data!=val)
        {
            temp1=temp;
            temp=temp->next;
        }
if(temp==head)
{
    head=temp->next;
    delete temp;
}
else{
temp1->next=temp->next;
       delete temp;
    }
}
}
};
class HashMap
{
 public:
     linklist hasharray[10];

     HashMap()
     {

     }

     int hashindex(int key)
     {
         return key%10;
     }
     void Insertion(int val)
     {
        hasharray[hashindex(val)].InsertAtTail(val);

     }
    int Search(int val)
    {
        hasharray[hashindex(val)].searching(val);

    }
void Remove(int val)
{
        hasharray[hashindex(val)].deletion(val);

}
};

int main()
{
    HashMap hash;
    int value=0;
    int choice;
    while (1)
    {
        cout<<endl;
        cout<<"1.Insert element into the table"<<endl;
        cout<<"2.Search element from the key"<<endl;
        cout<<"3.Delete element at a key"<<endl;
        cout<<"4.Exit"<<endl;
        cout<<"Enter your choice: ";
        cin>>choice;
        switch(choice)
        {
        case 1:
            cout<<"Enter value to be inserted: ";
            cin>>value;
            hash.Insertion(value);
            break;
        case 2:
            cout<<"Enter value to be searched: ";
            cin>>value;
            if (hash.Search(value) == -1)
            {
	        cout<<"No value found \n";
	        continue;
	        }
            break;
        case 3:
            cout<<"Enter value to be deleted: ";
            cin>>value;
            hash.Remove(value);
            break;
        case 4:
            exit(1);
        default:
           cout<<"\nEnter correct option\n";
       }
    }
    return 0;
}
