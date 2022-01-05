# hashing-seperate-chaining

#include<stdio.h>
#include<malloc.h>
#include<stdlib.h>
struct hashtable
{
    int data;
    struct hashtable *next;
};
typedef struct hashtable node;
int hash(int x)
{
    return x%10;
}
void insert(node *t[10],int x)
{
    node *p=(node *)(malloc(sizeof(node)));
    p->data=x;
    p->next=NULL;
    int i=hash(x);
    if(t[i]->next==NULL)
    {
        t[i]->next=p;
    }
    else
    {
        p->next=t[i]->next;
        t[i]->next=p;
    }
   
}
void display(node *t[10])
{
    node *temp;
    for(int i=0;i<10;i++)
    {
        temp=t[i]->next;
        while(temp!=NULL)
        {
            printf("%d ",temp->dash);
            temp=temp->next;
        }
    }
}
void delete(node *t[10],int x)
{
    int i=hash(x),flag=0;
    node *temp=t[i]->next,*temp1=t[i];
    while(temp!=NULL)
    {
        if(temp->data==x)
        {
            flag=1;
            break;
        }
        else
        {
            temp1=temp;
            temp=temp->next;
        }
    }
    if(flag==1)
    {
        temp1->next=temp->next;
        free(temp);
        printf("%d element is deleted",x);
    }
    else
    {
        printf("element is not present");
    }
}
void search(node *t[10],int x)
{
    int i=hash(x),flag=0;
    node *temp=t[i]->next;
    while(temp!=NULL)
    {
        if(temp->data==x)
        {
            flag=1;
            break;
        }
        else
        {
            temp=temp->next;
        }
    }
    if(flag==1)
    {
        printf("%d element is present",x);
    }
    else
    {
        printf("Not Present");
    }
}
void main()
{
    node *t[10];
    for(int i=0;i<10;i++)
    {
        t[i]=(node *)(malloc(sizeof(node)));
        t[i]->next=NULL;
    }
    int c,x;
    while(1)
 {    printf("Enter choice 1.insert 2.delete 3.display 4.search 5.exit");
      scanf("%d",&c);
      switch(c)
      {
          case 1:
                 printf("enter ele to insert");
                 scanf("%d",&x);
                   insert(t,x);
                   break;
          case 2:
                printf("enter ele to delete");
                scanf("%d",&x);
                delete(t,x);
                break;
         case 3:
               display(t);
               break;
        case 4:
               printf("enter ele to search");
               scanf("%d",&x);
               search(t,x);
               break;
        case 5:
              exit(1);
        default :
              printf("enter correct choice");
      }
}
