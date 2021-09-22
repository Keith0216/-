# include <iostream>
using namespace std;

typedef struct LNode 
{
	int data; 
	struct LNode *prior,*next; 
	
}LNode, *LinkList; 


class LinkList_class//归并排序
{
public:
	LinkList sortList(LinkList head)
	{
		if(head == NULL||head->next ==NULL) return head;
		LinkList slow = head;
		LinkList fast = head->next;
		while(fast!=NULL&&fast->next!=NULL)
		{
			slow = slow->next;
			fast = fast->next->next;
		}

		LinkList head2 = slow->next;
		slow->next->prior = NULL;
		slow->next = NULL;
		return mergeList(sortList(head), sortList(head2));
	}

	LinkList mergeList(LinkList head, LinkList head2)
	{
		LinkList dum = new LNode;
		LinkList res = dum;
		while(head!=NULL&&head2!=NULL)
		{
			if(head->data<head2->data)
			{
				res->next = head;
				head->prior = res;
				head = head->next;
			}
			else
			{
				res->next = head2;
				head2->prior = res;
				head2 = head2->next;
			}
			res = res->next;
		}
		res->next=(head==NULL?head2:head);
		return dum->next;
		
	}

}Lclass;



void CreateList_H(LinkList &L, int n)
{
	 LinkList s; 
	 L=new LNode;
	 L->prior=L->next=NULL;
	 cout <<"请依次输入n个元素：" <<endl;
	 
	 while(n--)
	 {
		s=new LNode; 
		cin>>s->data; 
		if(L->next)
		{
			L->next->prior=s;
		}
		s->next=L->next;
		s->prior=L;
		L->next=s; 
	 }
}
void Listprint_L(LinkList L) 
{
    LinkList p;
    p=L->next;
    while(p)
    {
		cout <<p->data <<"\t";
		p=p->next;
    }
    cout<<endl;
}
bool deletnum_L(LinkList &L, int x, int num)
{
	int j = 1;
	LinkList p;
	p = L->next;
	while((p->data != x) && (j<num))
	{
		p = p->next;
		j++;

	}
	if (j>=num)
		 return 0;
	else if (j<num)
	{
		p->prior->next = p->next;
		p->next->prior = p->prior;
		return 1;

	}
	else 
	{
		p->prior->next = NULL;
		p->prior = NULL;
		return 1;
	}
	delete p;

}

int main()
{
	LinkList L;
	LinkList_class Lclass;
	cout <<"请输入元素个数n：" <<endl;
	int n, x;
	bool y;
	cin>>n;
	CreateList_H(L, n);
	cout<<"您输入的是:"<<endl;
	Listprint_L(L);
	//排序
	cout<<"排序后"<<endl;
	Listprint_L(Lclass.sortList(L));
	cout<<"输入你要删除的结点的值:"<<endl;
	cin>>x;
	y = deletnum_L(L, x, n);
	if (y == true)Listprint_L(L);
	else 
		cout<<"未查询到此数"<<endl;
	return 0;

}
