/*
Name:
Div:-
Roll No:-
Experiment No 09:-A Dictionary stores keywords & its meanings. Provide facility for adding new keywords,
	 , updating values of any entry. Provide facility to display whole data
	  sorted in ascending/ Descending order. Use Height balance tree and find the complexity for finding a keyword.
*/
#include <iostream>
using namespace std;
class node
{
	public:
	string word;
	string meaning;
	node* left=NULL;
	node* right=NULL;

	node(string x, string y)
	{
		word = x;
		meaning = y;
		left = NULL;
		right = NULL;
	}
	friend class Dictionary;
};

class Dictionary
{
public:
	node* root, *q;	//q is parent here
	Dictionary()
	{
		root = NULL;
		q=NULL;
	}

	void insert(node*, string, string);
	void display_asc(node *);
	void display_desc(node *);
	void comparisons(node*, string);
	void updateWord(node*, string);
	void deleteWord(node*, string);
	node* min_node(node *);
};

void Dictionary::insert(node* p, string key, string keyMeaning)
{
	if(key < p->word)
	{
		if(p->left != NULL)
			insert(p->left, key, keyMeaning);
		else
			p->left = new node(key, keyMeaning);
	}
	else if(key > p->word)
	{
		if(p->right != NULL)
			insert(p->right, key, keyMeaning);
		else
			p->right = new node(key, keyMeaning);
	}
}

void Dictionary::display_asc(node *p)		//inorder
{
	if(p->left!=NULL)
		display_asc(p->left);
	cout<<"\n" << p->word<<" \t" << p->meaning;
	if(p->right!=NULL)
		display_asc(p->right);
}

void Dictionary::display_desc(node *p)
{
	if(p->right!=NULL)
			display_desc(p->right);
	cout<<"\n" << p->word<<" \t" << p->meaning;
	if(p->left!=NULL)
		display_desc(p->left);
}

void Dictionary::updateWord(node* p, string key)
{
	while(p!=NULL)
	{
		if(key < p->word)
			p = p->left;

		else if(key > p->word)
			p = p->right;

		else if(key == p->word)
		{
			cout<<"\nEnter its new meaning: ";
			cin>>p->meaning;
			return;
		}
	}
	cout<<"\nWord not found!";
}


int main()
{
	int choice, n;
	string newWord, searchWord, newMeaning;
	Dictionary d1;
	menu:
	cout<<"\n\nDICTIONARY: ";
	cout<<"\n\n1. Insert new words";
	cout<<"\n2. Display the dictionary in ascending order";
	cout<<"\n3. Display the dictionary in descending order";
	cout<<"\n4. Search and update a word";
	cout<<"\n\nEnter your choice: ";
	cin>>choice;
	switch(choice)
	{
	case 1:
		cout<<"\nEnter the number of words to insert: ";
		cin >> n;
		for(int i=0 ; i<n ; i++)
		{
			cout<<"\nEnter the word to be inserted: ";
			cin >> newWord;
			cout<<"\nEnter its meaning: ";
			cin >> newMeaning;
			if(d1.root == NULL)
				d1. root = new node(newWord, newMeaning);
			else
				d1.insert(d1.root, newWord, newMeaning);
		}
		break;

	case 2:
		d1.display_asc(d1.root);
		break;

	case 3:
		d1.display_desc(d1.root);
		break;

	case 4:
		cout<<"\nEnter the word to search: ";
		cin >> searchWord;
		d1.updateWord(d1.root, searchWord);
		break;

	

	default:
		cout<<"\nInvalid input!";
	}
	if(choice!=7)
		goto menu;
	return 0;
}

