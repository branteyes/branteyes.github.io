---
layout: post
title: stack,queue,linked list
date:  2017-03-19
categories: 阅读记录 《啊哈算法》
---

## 基本的stack，queue，linked list


### 栈的运用
基本原理：只允许在一端进行插入或删除操作的线性表。首先栈是一种线性表，但是限定这种线性表只能在某一端进行插入和删除操作

栈是先进后出原则，例如浏览网页前进后退和手枪上子弹打子弹

代码示例1:
  #include <string.h>
  int main()
  {
  char a[101],s[101];
  int i,len,mid,next,top;
  gets(a); //读入一行字符串
  len=strlen(a); //求字符串的长度
  mid=len/2-1; //求字符串的中点
  top=0;//栈的初始化
  //将mid前的字符依次入栈
  for(i=0;i<=mid;i++)
  s[++top]=a[i];
  //判断字符串的长度是奇数还是偶数，并找出需要进行字符匹配的起始下标
  if(len%2==0)
  next=mid+1;
  else
  next=mid+2;
  //开始匹配
  for(i=next;i<=len-1;i++)
  {
    if(a[i]!=s[top])
    break;
    top--;
  }
  //如果top的值为0，则说明栈内所有的字符都被一一匹配了
  if(top==0)
  printf("YES");
  else
  printf("NO");
  getchar();getchar();
  return 0;
  }

代码示例2:
  #include <stdio.h>
  struct queue
  {
  int data[1000];
  int head;
  int tail;
  };
  struct stack
  {
  int data[10];
  int top;
  };
  int main()
  {
  struct queue q1,q2;
  struct stack s;
  int book[10];
  int i,t;
  //初始化队列
  q1.head=1; q1.tail=1;
  q2.head=1; q2.tail=1;
  //初始化栈
  s.top=0;
  //初始化用来标记的数组，用来标记哪些牌已经在桌上
  for(i=1;i<=9;i++)
  book[i]=0;
  //依次向队列插入6个数
  //小哼手上的6张牌
  for(i=1;i<=6;i++)
  {
  scanf("%d",&q1.data[q1.tail]);
  q1.tail++;
  }
  //小哈手上的6张牌
  for(i=1;i<=6;i++)
  {
  scanf("%d",&q2.data[q2.tail]);
  q2.tail++;
  }
  while(q1.head<q1.tail && q2.head<q2.tail ) //当队列不为空的时候执行循环
  {
  t=q1.data[q1.head];//小哼出一张牌
  //判断小哼当前打出的牌是否能赢牌
  if(book[t]==0) //表明桌上没有牌面为t的牌
  {
  //小哼此轮没有赢牌
  q1.head++; //小哼已经打出一张牌，所以要把打出的牌出队
  s.top++;
  s.data[s.top]=t; //再把打出的牌放到桌上，即入栈
  book[t]=1; //标记桌上现在已经有牌面为t的牌
  }
  else
  {
  //小哼此轮可以赢牌
  q1.head++;//小哼已经打出一张牌，所以要把打出的牌出队
  q1.data[q1.tail]=t;//紧接着把打出的牌放到手中牌的末尾
  q1.tail++;
  while(s.data[s.top]!=t) //把桌上可以赢得的牌依次放到手中牌的末尾
  {
  book[s.data[s.top]]=0;//取消标记
  q1.data[q1.tail]=s.data[s.top];//依次放入队尾
  q1.tail++;
  s.top--; //栈中少了一张牌，所以栈顶要减1
  }
  }
  t=q2.data[q2.head]; //小哈出一张牌
  //判断小哈当前打出的牌是否能赢牌
  if(book[t]==0) //表明桌上没有牌面为t的牌
  {
  //小哈此轮没有赢牌
  q2.head++; //小哈已经打出一张牌，所以要把打出的牌出队
  s.top++;
  s.data[s.top]=t; //再把打出的牌放到桌上，即入栈
  book[t]=1; //标记桌上现在已经有牌面为t的牌
  }
  else
  {
  //小哈此轮可以赢牌
  q2.head++;//小哈已经打出一张牌，所以要把打出的牌出队
  q2.data[q2.tail]=t;//紧接着把打出的牌放到手中牌的末尾
  q2.tail++;
  while(s.data[s.top]!=t) //把桌上可以赢得的牌依次放到手中牌的末尾
  {
  book[s.data[s.top]]=0;//取消标记
  q2.data[q2.tail]=s.data[s.top];//依次放入队尾
  q2.tail++;
  s.top--;
  }
  }
  }
  if(q2.head==q2.tail)
  {
  printf("小哼win\n");
  printf("小哼当前手中的牌是");
  for(i=q1.head;i<=q1.tail-1;i++)
  printf(" %d",q1.data[i]);
  if(s.top>0) //如果桌上有牌则依次输出桌上的牌
  {
  printf("\n桌上的牌是");
  for(i=1;i<=s.top;i++)
  printf(" %d",s.data[i]);
  }
  else
  printf("\n桌上已经没有牌了");
  }
  else
  {
  printf("小哈win\n");
  printf("小哈当前手中的牌是");
  for(i=q2.head;i<=q2.tail-1;i++)
  printf(" %d",q2.data[i]);
  if(s.top>0) //如果桌上有牌则依次输出桌上的牌
  {
  printf("\n桌上的牌是");
  for(i=1;i<=s.top;i++)
  printf(" %d",s.data[i]);
  }
  else
  printf("\n桌上已经没有牌了");
  }
  getchar();getchar();
  return 0;
  }


### 队列
基本原理：队列是一种特殊的线性结构，它只允许在队列的首部（head）进行删除操作，这称为“出队”，而在队列的尾部（tail）进行插入操作，这称为“入队”。

当队列中没有元素时（即head==tail），称为空队列。队列是先进先出原则，例如排队结账

代码示例1:
  include <stdio.h>
  int main()
  {
  int q[102]={0,6,3,1,7,5,8,9,2,4};
  int head;
  int tail;
  int i;
  //初始化队列
  head=1;
  tail=10; //队列中已经有9个元素了，tail指向队尾的后一个位置
  while(head<tail) //当队列不为空的时候执行循环
  {
  //打印队首并将队首出队
  printf("%d ",q[head]);
  head++;
  //先将新队首的数添加到队尾
  q[tail]=q[head];
  tail++;
  //再将队首出队
  head++;
  }
  getchar();
  getchar();

  return 0;
  }

代码示例2:
  include <stdio.h>
  struct queue
  {
  int data[100];//队列的主体，用来存储内容
  int head;//队首
  int tail;//队尾
  };
  int main()
  {
  struct queue q;
  int i;
  //初始化队列
  q.head=1;
  q.tail=1;
  for(i=1;i<=9;i++)
  {
  //依次向队列插入9个数
  scanf("%d",&q.data[q.tail]);
  q.tail++;
  }
  while(q.head<q.tail) //当队列不为空的时候执行循环
  {
  //打印队首并将队首出队
  printf("%d ",q.data[q.head]);
  q.head++;
  //先将新队首的数添加到队尾
  q.data[q.tail]=q.data[q.head];
  q.tail++;
  //再将队首出队
  q.head++;
  }
  getchar();
  getchar();
  return 0;
  }


### 链表
基本原理：单链表是链式存储线性表，不需要使用地址连续的存储单元，不要求逻辑上相邻的两个元素在物理位置上也相邻，它是通过“链”建立起数据元素之间的逻辑关系，对线性表的插入、删除不需要移动元素，只需要修改指针。

线性表的链式存储又称为单链表，它是指通过一组任意的存储单元来存储线性表中的数据元素。为了建立起数据元素之间的线性关系，对每个链表结点，除了存放元素自身的信息之外，还需要存放一个指向其后继的指针

代码示例1:
  #include <stdio.h>
  #include <stdlib.h>
  int main()
  {
  int *p; //定义一个指针p
  p=(int *)malloc(sizeof(int)); //指针p获取动态分配的内存空间地址
  *p=10; //向指针p所指向的内存空间中存入10
  printf("%d",*p); //输出指针p所指向的内存中的值
  getchar();getchar();
  return 0;
  }

代码示例2:
  #include <stdio.h>
  #include <stdlib.h>
  //这里创建一个结构体用来表示链表的结点类型
  struct node
  {
  int data;
  struct node *next;
  };
  int main()
  {
  struct node *head,*p,*q,*t;
  int i,n,a;
  scanf("%d",&n);
  head = NULL;//头指针初始为空
  for(i=1;i<=n;i++)//循环读入n个数
  {
  scanf("%d",&a);
  //动态申请一个空间，用来存放一个结点，并用临时指针p指向这个结点
  p=(struct node *)malloc(sizeof(struct node));
  p->data=a;//将数据存储到当前结点的data域中
  p->next=NULL;//设置当前结点的后继指针指向空，也就是当前结点的下一个结点为空
  if(head==NULL)
  head=p;//如果这是第一个创建的结点，则将头指针指向这个结点
  else
  q->next=p;//如果不是第一个创建的结点，则将上一个结点的后继指针指向当前结点
  q=p;//指针q也指向当前结点
  }
  //输出链表中的所有数
  t=head;
  while(t!=NULL)
  {
    printf("%d ",t->data);
  t=t->next;//继续下一个结点
  }
  getchar();getchar();
  return 0;
  }

  代码示例3:
    #include <stdio.h>
  #include <stdlib.h>
  //这里创建一个结构体用来表示链表的结点类型
  struct node
  {
  int data;
  struct node *next;
  };
  int main()
  {
  struct node *head,*p,*q,*t;
  int i,n,a;
  scanf("%d",&n);
  head = NULL;//头指针初始为空
  for(i=1;i<=n;i++)//循环读入n个数
  {
  scanf("%d",&a);
  //动态申请一个空间，用来存放一个结点，并用临时指针p指向这个结点
  p=(struct node *)malloc(sizeof(struct node));
  p->data=a;//将数据存储到当前结点的data域中
  p->next=NULL;//设置当前结点的后继指针指向空，也就是当前结点的下一个结点为空
  if(head==NULL)
  head=p;//如果这是第一个创建的结点，则将头指针指向这个结点
  else
  q->next=p;//如果不是第一个创建的结点，则将上一个结点的后继指针指向当前结点
  q=p;//指针q也指向当前结点
  }
  scanf("%d",&a);//读入待插入的数
  t=head;//从链表头部开始遍历
  while(t!=NULL)//当没有到达链表尾部的时候循环
  {
  if(t->next->data > a)//如果当前结点下一个结点的值大于待插入数，将数插入到中间
  {
  p=(struct node *)malloc(sizeof(struct node));//动态申请一个空间，
  用来存放新增结点
  p->data=a;
  p->next=t->next;//新增结点的后继指针指向当前结点的后继指针所指向的结点
  t->next=p;//当前结点的后继指针指向新增结点
  break;//插入完毕退出循环
  }
  t=t->next;//继续下一个结点
  }
  //输出链表中的所有数
  t=head;
  while(t!=NULL)
  {
  printf("%d ",t->data);
  t=t->next;//继续下一个结点
  }
  getchar();getchar();
  return 0;
  }

  代码示例4:
  #include <stdio.h>
  int main()
  {
  int data[101],right[101];
  int i,n,t,len;
  //读入已有的数
  scanf("%d",&n);
  for(i=1;i<=n;i++)
  scanf("%d",&data[i]);
  len=n;
  //初始化数组right
  for(i=1;i<=n;i++)
  {
  if(i!=n)
  right[i]=i+1;
  else
  right[i]=0;
  }
  //直接在数组data的末尾增加一个数
  len++;
  scanf("%d",&data[len]);
  //从链表的头部开始遍历
  t=1;
  while(t!=0)
  {
  if(data[right[t]]>data[len])//如果当前结点下一个结点的值大于待插入数，将
  数插入到中间
  {
  right[len]=right[t];//新插入数的下一个结点标号等于当前结点的下一个结
  点编号
  right[t]=len;//当前结点的下一个结点编号就是新插入数的编号
  break;//插入完成跳出循环
  }
  t=right[t];
  }
  //输出链表中所有的数
  t=1;
  while(t!=0)
  {
  printf("%d ",data[t]);
  t=right[t];
  }
  getchar();
  getchar();
  return 0;
  }
