/*
NAME:-Dhadge Krushna Babasaheb
Class:-SE
DIV:-A
Roll No.:-16
*C++ Program To read details of a book consists of chapters,
 *chapters consist of sections and sections consist of
 *subsections. Construct a tree and print the nodes.
 *Find the time and space requirements of your method.
 **/
# include <iostream>
# include <cstdlib>
# include <string.h>
using namespace std;
/*
 * Node Declaration
 */
struct node
{
    char label[10];
    int ch_count;
    struct node *child[10];
}*root;

/*
 * Class Declaration
 */
class GT
{
    public:
        void create_tree();  
 void display(node * r1);
     
        GT()
        {
            root = NULL;
        }
};

void GT::create_tree()
{
 int tbooks,tchapters,i,j,k;
 root = new node;
 cout<<"\n\tEnter name of book : ";
 cin>>root->label;
 cout<<"\n\tEnter no. of chapters in book : ";
 cin>>tchapters; 
 root->ch_count = tchapters;
 for(i=0;i<tchapters;i++)
 {
  root->child[i] = new node;
  cout<<"\n\tEnter Chapter name : ";
  cin>>root->child[i]->label;   
  cout<<"\n\tEnter no. of sections in  Chapter: "<<root->child[i]->label<<" : ";
  cin>>root->child[i]->ch_count;
  for(j=0;j<root->child[i]->ch_count;j++)
  {
   root->child[i]->child[j] = new node;
   cout<<"\n\tEnter Section "<<j+1<<" name : ";
   cin>>root->child[i]->child[j]->label;   
   cout<<"\n\tEnter no. of subsections in "<<root->child[i]->child[j]->label<<" : ";
   cin>>root->child[i]->child[j]->ch_count;
    for(k=0;k<root->child[i]->child[j]->ch_count;k++)
  	{
   root->child[i]->child[j]->child[k] = new node;
   cout<<"\n\tEnter subSection "<<k+1<<" name : ";
   cin>>root->child[i]->child[j]->child[k]->label; 
 	}  
  }

}
}


void GT::display(node * r1)
{
 int i,j,k,tchapters;
 if(r1 != NULL)
 { 
  cout<<"\n\n-----Book Hierarchy---";

  cout<<"\n\n Book title : "<<r1->label;
  tchapters = r1->ch_count;
  for(i=0;i<tchapters;i++)
  {
  
   cout<<"\n Chapter "<<i+1<<" : ";
   cout<<" "<<r1->child[i]->label;   
   
   for(j=0;j<r1->child[i]->ch_count;j++)
   {
   	 cout<<"\n Sections ";
    //cin>>r1->child[i]->child[j]->label;   
    cout<<j+1<<" :"<<r1->child[i]->child[j]->label<<"\n";
    
    for(k=0;k<r1->child[i]->child[j]->ch_count;k++)
   {
   	cout<<"SubSections ";
   	cout<<j+1<<"."<<k+1<<" "<<root->child[i]->child[j]->child[k]->label <<"\n\t";
   }  

  }
 }
}
}


/*
 * Main Contains Menu
 */
int main()
{
    int choice;
   GT gt;
    while (1)
    {
        cout<<"\n -----------------"<<endl;
        cout<<"Book Tree Creation"<<endl;
        cout<<"-----------------"<<endl;
        cout<<"1.Create"<<endl;
        cout<<"2.Display"<<endl;
        cout<<"3.Quit"<<endl;
        cout<<"Enter your choice : ";
        cin>>choice;
        switch(choice)
        {
        case 1:
              gt.create_tree();
        case 2:
              gt.display(root);
            break;
        case 3:
            exit(1);
        default:
            cout<<"Wrong choice"<<endl;
        }
    }
}





**********OUTPUT*********

-----------------
Book Tree Creation
-----------------
1.Create
2.Display
3.Quit
Enter your choice : 1

        Enter name of book : DSA

        Enter no. of chapters in book : 2

        Enter Chapter name : HASHING

        Enter no. of sections in  Chapter: HASHING : 2

        Enter Section 1 name : CHAINIING

        Enter no. of subsections in CHAINIING : 2

        Enter subSection 1 name : WITH

        Enter subSection 2 name : WITHOUT

        Enter Section 2 name : CLODEDHASHING

        Enter no. of subsections in CLODEDHASHING : 2

        Enter subSection 1 name : LINEAR

        Enter subSection 2 name : QUADRATIC

        Enter Chapter name : TREE

        Enter no. of sections in  Chapter: TREE : 2

        Enter Section 1 name : REPRESENTATION

        Enter no. of subsections in REPRESENTATION : 2

        Enter subSection 1 name : ARRAY

        Enter subSection 2 name : LINKEDLIST

        Enter Section 2 name : TRAVERSAL

        Enter no. of subsections in TRAVERSAL : 3

        Enter subSection 1 name : PREORDER

        Enter subSection 2 name : INORDER

        Enter subSection 3 name : POSTORDER


-----Book Hierarchy---

 Book title : DSA
 Chapter 1 :  HASHING
 Sections 1 :CHAINIING
SubSections 1.1 WITH
        SubSections 1.2 WITHOUT

 Sections 2 :CLODEDHASHIN?
SubSections 2.1 LINEAR
        SubSections 2.2 QUADRATIC

 Chapter 2 :  TREE
 Sections 1 :REPRESENTATI?
SubSections 1.1 ARRAY
        SubSections 1.2 LINKEDLIST

 Sections 2 :TRAVERSAL
SubSections 2.1 PREORDER
        SubSections 2.2 INORDER
        SubSections 2.3 POSTORDER

 -----------------
Book Tree Creation
-----------------
1.Create
2.Display
3.Quit
Enter your choice :


