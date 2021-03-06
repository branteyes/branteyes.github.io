---
layout: post
title: "sorts"
date: 2017-03-18
categories: 阅读记录 《啊哈算法》
---
## 简单的三种排序

### 1.简化版桶排序
基本原理：创建初始化一个数组，然后循环输入比数组元素多一个的数字，对应数组下标，然后遍历输出

代码示例1:
  include <stdio.h>
  int main()
  {
  int book[1001],i,j,t,n;
  for(i=0;i<=1000;i++)
  book[i]=0;
  scanf("%d",&n);//输入一个数n，表示接下来有n个数
  for(i=1;i<=n;i++)//循环读入n个数，并进行桶排序
  {
  scanf("%d",&t); //把每一个数读到变量t中
  book[t]++; //进行计数，对编号为t的桶放一个小旗子
  }
  for(i=1000;i>=0;i--) //依次判断编号1000~0的桶
  for(j=1;j<=book[i];j++) //出现了几次就将桶的编号打印几次
  printf("%d ",i);
  getchar();getchar();
  return 0;
  }
该代码的算法复杂度为O(M+N)



###  2.冒泡排序
基本原理： 每次比较相邻的两个元素，左边的比右边的大则交换位置，一轮结束后，从第二个元素开始比较，一直到倒数第二个元素，最后一个不需要比较。使用双重循环，加上一个判断交换元素位置，最后输出数组

代码示例1:
  include <stdio.h>
  int main()
  {
  int a[100],i,j,t,n;
  scanf("%d",&n); //输入一个数n，表示接下来有n个数
  for(i=1;i<=n;i++) //循环读入n个数到数组a中
  scanf("%d",&a[i]);
  //冒泡排序的核心部分
  for(i=1;i<=n-1;i++) //n个数排序，只用进行n-1趟
  {
  for(j=1;j<=n-i;j++) //从第1位开始比较直到最后一个尚未归位的数，想一想为什
  么到n-i就可以了。
  {
  if(a[j]<a[j+1]) //比较大小并交换
  { t=a[j]; a[j]=a[j+1]; a[j+1]=t; }
  }
  }
  for(i=1;i<=n;i++) //输出结果
  printf("%d ",a[i]);
  getchar();getchar();
  return 0;
  }
该代码的算法复杂度为O（N^2）



### 3.快速排序
基本原理：每次排序的时候，设置一个基准点，将小于等于基准点的数全部放到基准点的左边，将大于等于基准点的数全部放到基准点的右边，

代码示例1:
  include <stdio.h>
  int a[101],n;//定义全局变量，这两个变量需要在子函数中使用
  void quicksort(int left,int right)
  {
  int i,j,t,temp;
  if(left>right)
  return;
  temp=a[left]; //temp中存的就是基准数
  i=left;
  j=right;
  while(i!=j)
  {
  //顺序很重要，要先从右往左找
  while(a[j]>=temp && i<j)
  j--;
  //再从左往右找
  while(a[i]<=temp && i<j)
  i++;
  //交换两个数在数组中的位置
  if(i<j)//当哨兵i和哨兵j没有相遇时
  {
  t=a[i];
  a[i]=a[j];
  a[j]=t;
  }
  }
  //最终将基准数归位
  a[left]=a[i];
  a[i]=temp;
  quicksort(left,i-1);//继续处理左边的，这里是一个递归的过程
  quicksort(i+1,right);//继续处理右边的，这里是一个递归的过程
  }

  int main()
  {
  int i,j,t;
  //读入数据
  scanf("%d",&n);
  for(i=1;i<=n;i++)
  scanf("%d",&a[i]);
  quicksort(1,n); //快速排序调用
  //输出排序后的结果
  for(i=1;i<=n;i++)
  printf("%d ",a[i]);
  getchar();getchar();
  return 0;
  }
