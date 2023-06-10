/* name:Dhadge Krushna Babasaheb
roll no:16 
Div:A
Experiment No5:
Beginning with an empty binary search tree, Construct binary search tree by inserting the values in the order given. After constructing a binary tree -
i.	Insert new node
ii.	Find number of nodes in longest path from root
iii.	Minimum data value found in the tree
iv.	Change a tree so that the roles of the left and right pointers are swapped at every node
v.	Search a value */

#include<iostream>
#define size 20
using namespace std;
class bintree
{
	typedef struct bst
	{
		int data;
		struct bst *left,*right;	
	} node;
	node *root,*New, *temp, *parent;
	public:
		node *que[20];
		int front,rear;
		bintree()
		{
			root=NULL;
			front=rear=-1;
		}
		void create();
		void display();
		void find();
		void insert(node *, node *);
		void inorder(node *);
		void search(node**, int, node **);
		void LongestPathNodes();
		int Depth(node *);
		void FindMinValue();
		void minValue(node *,int*);
		void Mirrorimg();
		void mirror(node *);
		void LevelWiseDisplay(node *root);
		void enque(node *temp);
		node *deque();
};

void bintree::create()
{
New = new node;
New->left = NULL;
New->right = NULL;
cout<<"\n Enter The Element : ";
cin>> New->data;
if (root == NULL)
      root = New;
else
		insert(root, New);
}


void bintree::insert(node *root, node *New)
{
	if (New->data < root-> data)
	{
		if (root->left == NULL)
			root->left = New;
		else
			insert(root->left, New);
	}
	if (New->data > root->data)
	{
		if (root->right == NULL)
			root->right = New;
		else
			insert(root->right, New);
    }     
}

void bintree::display()
{
	if (root == NULL)
		cout<<"Tree Is Not Created";
    else
    {
    	cout<<"\n The Tree is : ";
		inorder(root);
	}
}

void bintree::inorder(node *temp)
{
	if (temp != NULL)
	{
		inorder(temp->left);
		cout<<" "<<temp->data;
		inorder(temp->right);
	}
}

void bintree::FindMinValue()
{
	int min = root->data;
	minValue(root, &min);
	cout<<"\n The minimum value node within a tree is: "<< min;
}

void bintree::minValue(node *temp,int *min)
{
	if (temp != NULL)
	{
	minValue(temp->left,min);
	if (temp->data < *min)
	*min = temp->data;
	minValue(temp->right,min);
	}
}

void bintree::find()
{
int key;
cout << "\n Enter The Element Which You Want To Search : ";
cin >> key;
temp=root;
search(&temp, key, &parent);
if (temp== NULL)
cout<< "\n Element is not present ";
else
cout<< "\n parent of node "<<temp->data<<" is "<<parent->data;
}

void bintree::search(node **temp,int key,node **parent)
{
	if (*temp==NULL)
		cout<<endl<<"Tree is Not created";
		else
		{
			while(*temp !=NULL)
			{
				if ((*temp)->data==key)
				{
					cout<<"\n Element "<<(*temp)->data<<" is Present ";
					break;
				}
				*parent=*temp;
			    if ((*temp)->data > key)
                    *temp =(*temp)->left;
                    else
                    *temp =(*temp)->right;
			}
		}
		return;
}

void bintree::LongestPathNodes()
{
if (root==NULL)
   cout<<"\n Tree is Empty!!!"; 
else
{ /* compute the depth of each subtree */
int lDepth = Depth(root);
int rDepth = Depth(root);
/* use the larger one */
if (lDepth > rDepth)
cout << "\n The number of nodes on Longest Path = "<< lDepth + 1;
//retum(IDepth + 1),
else
cout << "\n The number of nodes on Longest Path = " << rDepth + 1;
}
}

int bintree::Depth(node *root)
{
if (root== NULL)
return 0;
else
{
/* compute the depth of each subtree */
int lDepth = Depth(root->left);
int rDepth = Depth(root->right);
/* Return the larger one */
if (lDepth > rDepth)
return lDepth;
else
return(rDepth + 1);
}
}

void bintree::enque(node *temp)
{
	if(rear==size-1)
	{
		cout<<"Queue is empty!!!";
		return;
	}
	rear=rear+1;
	que[rear]=temp;
}

bintree::node *bintree::deque()
{
node *temp;
if (front== rear)
{
cout << "Queue is empty";
return NULL;
}
front++;
temp= que[front];
return temp;
}


void bintree::LevelWiseDisplay(node *root)
{
node *temp,*dummy;
dummy = new node;
front = rear = -1;
if (dummy== NULL)
cout<< "Insufficient Memory\n";
dummy->left = root;
dummy->right = NULL;
dummy->data = -999;
temp = dummy->left;
enque(temp); //inserting the node in the queue
enque(dummy);
temp = deque();//deleting the node from the queue
cout << "\n";
while (front != rear)
{
if (temp != dummy)
{
cout<<" "<< temp->data;
if (temp->left != NULL)
enque(temp->left);
if (temp->right != NULL)
enque(temp-> right);
}
else
{
	enque(temp);
	cout<<"\n";
}
temp=deque();
}
}

void bintree::Mirrorimg()
{
cout << "\n Original Tree",
LevelWiseDisplay(root);
mirror(root);
cout << "\n Tree with Swapped Nodes";
LevelWiseDisplay(root);
mirror(root); //bringing back the tree to original state
}

void bintree::mirror(node *root)
{
	node *temp_node;
	if(root!=NULL)
	{
		mirror(root->left);
		mirror(root->right);//Swapping left and right child nodes
		temp_node=root->left;
		root->left=root->right;
		root->right=temp_node;
	}
}

int main()
{
	int choice;
char ans='N';
bintree tr;
	cout<<"\n\t****Program for Binary Search Tree *****";
	do
	{
		cout <<"\n1.Create";
		cout <<"\n2.Display";
		cout <<"\n3.Longest Path Nodes",
		cout <<"\n4.Find Minimum Value",
		cout <<"\n5.Change Tree by Swapping nodes";
		cout <<"\n6.Search";
		cout <<"\n\n Enter your choice :";
		cin >> choice;
		switch (choice)
		{
			case 1:do
					{	
	       				tr.create();
						cout <<"Do u Want To enter More elements?(y/n)" << endl;
						cin >> ans;
					} while (ans == 'y');
					break;
			case 2:tr.display();
					break;
			case 3:tr.LongestPathNodes();
					break;
			case 4:tr.FindMinValue();
					break;
			case 5:tr. Mirrorimg();
					break;
			case 6:tr. find();
			break;
		}
	}while(choice!=7);
	return 0;
}

/* ************ output ************


        ****Program for Binary Search Tree *****
1.Create
2.Display
3.Longest Path Nodes
4.Find Minimum Value
5.Change Tree by Swapping nodes
6.Search

 Enter your choice :1

 Enter The Element : 10
Do u Want To enter More elements?(y/n)
y

 Enter The Element : 8
Do u Want To enter More elements?(y/n)
y

 Enter The Element : 7
Do u Want To enter More elements?(y/n)
y

 Enter The Element : 9
Do u Want To enter More elements?(y/n)
y

 Enter The Element : 4
Do u Want To enter More elements?(y/n)
y

 Enter The Element : 12
Do u Want To enter More elements?(y/n)
y

 Enter The Element : 11
Do u Want To enter More elements?(y/n)
y

 Enter The Element : 13
Do u Want To enter More elements?(y/n)
n

1.Create
2.Display
3.Longest Path Nodes
4.Find Minimum Value
5.Change Tree by Swapping nodes
6.Search

 Enter your choice :2

 The Tree is :  4 7 8 9 10 11 12 13
1.Create
2.Display
3.Longest Path Nodes
4.Find Minimum Value
5.Change Tree by Swapping nodes
6.Search

 Enter your choice :3

 The number of nodes on Longest Path = 4
1.Create
2.Display
3.Longest Path Nodes
4.Find Minimum Value
5.Change Tree by Swapping nodes
6.Search

 Enter your choice :4

 The minimum value node within a tree is: 4
1.Create
2.Display
3.Longest Path Nodes
4.Find Minimum Value
5.Change Tree by Swapping nodes
6.Search

 Enter your choice :5

 Original Tree
 10
 8 12
 7 9 11 13
 4
 Tree with Swapped Nodes
 10
 12 8
 13 11 9 7
 4
1.Create
2.Display
3.Longest Path Nodes
4.Find Minimum Value
5.Change Tree by Swapping nodes
6.Search

 Enter your choice :6

 Enter The Element Which You Want To Search : 4

 Element 4 is Present
 parent of node 4 is 7
1.Create
2.Display
3.Longest Path Nodes
4.Find Minimum Value
5.Change Tree by Swapping nodes
6.Search

 Enter your choice : */
