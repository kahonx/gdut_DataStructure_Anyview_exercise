---
title: 数据结构习题
date: 2022/3/7
---



# 数据结构习题

## 第一章
### DC01PE06 将三个整数按升序重新排列
试写一算法，如果三个整数a，b和c的值不是依次非递增的，则通过交换，令其为非递增。
要求实现下列函数：
void Descend(int &a, int &b, int &c); 
/* 通过交换，令 a >= b >= c */

```c
#include "allinclude.h"  //DO NOT edit this line
void Descend(int &a, int &b, int &c) { // 通过交换，令 a >= b >= c
    // Add your code here
    int temp;
    if(a < c){
      temp = c;
      c = a;
      a = temp;
    }
    if(b < c){
      temp = b;
      b = c;
      c= temp;
    }
    if(b > a){
      temp = a;
      a = b;
      b = temp;
    }
}
```
### DC01PE08 求一元多项式的值
试编写算法求一元多项式
    P(x) = a0 + a1x + a2x^2 + ... + anx^n
的值P(x0)，并确定算法中每一语句的执行次数和整个算法的时间复杂度。
要求实现下列函数：
float Polynomial(int n, int a[], float x0);
/* 求一元多项式的值P(x0)。                    */
/* 数组a的元素a[i]为i次项的系数，i=0,1,...,n  */

```c
#include "allinclude.h"  //DO NOT edit this line
float Polynomial(int n, int a[], float x0){ 
    // Add your code here
    float ans = a[0],t = 1.0;
    int i = 1;
    while(i <= n){
      t *= x0;
      ans += (t * a[i]);
      i++;
    }
    return ans;
}
```
### DC01PE11 求k阶裴波那契序列的第m项的值
已知k阶裴波那契序列的定义为
    f(0)=0, f(1)=0, ..., f(k-2)=0, f(k-1)=1;
    f(n)=f(n-1)+f(n-2)+...+f(n-k), n=k,k+1,...
试编写求k阶裴波那契序列的第m项值的函数算法，k和m均以值调用的形式在函数参数表中出现。
要求实现下列函数：
Status Fibonacci(int k, int m, int &f);
/* 如果能求得k阶斐波那契序列的第m项的值f，则返回OK；*/
/* 否则（比如，参数k和m不合理）返回ERROR            */

```c
#include "allinclude.h"  //DO NOT edit this line
Status Fibonacci(int k, int m, int &f) { 
    // Add your code here
    int *a;     
    int i=1; 
    if(k < 2 || m < 0) return ERROR;     
    if(m < k) {
      if(m == k-1) f = 1;
      else f = 0;
      return OK;
    }
    a = (int*)malloc((m + 1)*sizeof(int));
    for (int i = 0; i < k - 1; i++) a[i] = 0;
      /* code */
      a[i] = 0;
      i = k + 1;
      a[k - 1] = 1;
      a[k] = 1;
      while(i <= m){
        a[i] = 2*a[i - 1] - a[i - k -1];
        i++;
      }
    f = a[m];
    return OK;
}
```
### DC01PE18 计算i!×2^i的值
试编写算法，计算i!×2^i的值并存入数组a[0..n-1]的第i-1个分量中 (i=1,2,…,n)。假设计算机中允许的整数最大值为MAXINT，则当对某个k(1≤k≤n)使k!×2^k>MAXINT时，应按出错处理。注意选择你认为较好的出错处理方法。
要求实现下列函数：
Status Series(int a[], int n);
/* 求i!*2^i序列的值并依次存入长度为n的数组a；若所有 */
/* 值均不超过MAXINT，则返回OK，否则返回EOVERFLOW     */

```c
#include "allinclude.h"  //DO NOT edit this line
Status Series(int a[], int n) { 
    // Add your code here
 int t;
 int s;
 if(0 == n){
  return ERROR;
 }
 for(int i=1; i<=n; ++i){
  t = 1; 
  s = 1;
  for(int j=1; j<=i; ++j){
   t*=j;
   s*=2;
  }
  a[i-1] = t * s;
  if(a[i-1] > MAXINT){
   return EOVERFLOW;
  }
 }
 return OK;
}
```
### DC01PE49  由一维数组构建一个序列
试写一算法，由长度为n的一维数组a构建一个序列S。
要求实现下列函数：
Status CreateSequence(Sequence &S, int n, ElemType *a); 
/* 由长度为n的一维数组a构建一个序列S，并返回OK。 */
/* 若构建失败，则返回ERROR                       */
序列的定义为：
typedef struct {
  ElemType  *elem;
  int  length;
} Sequence;

```c
#include "allinclude.h"  //DO NOT edit this line
Status CreateSequence(Sequence &S, int n, ElemType *a) { 
   if(n<1){
     return ERROR;
   }else{
     S.elem = (ElemType*)malloc(n*sizeof(ElemType));
     S.elem[0] = a[0];
     for (int i = 0; i < n; i++)
       /* code */
       S.elem[i] = a[i];
       S.length = n;
     }
     return OK;
}
```
### DC01PE61  构建一个值为x的结点
链表的结点和指针类型定义如下
    typedef struct LNode {
       ElemType  data;
       struct LNode *next;
    } LNode, *LinkList;
试写一函数，构建一个值为x的结点。
要求实现下列函数：
LinkList MakeNode(ElemType x); 
/* 构建一个值为x的结点，并返回其指针。 */
/* 若构建失败，则返回NULL。            */

```c
#include "allinclude.h"  //DO NOT edit this line
LinkList MakeNode(ElemType x) { 
    // Add your code here
  LNode*p;
  p=(LNode*)malloc(sizeof(LNode));
  if(p == NULL) return NULL;
  else 
  p->data = x;
  return p;
}
```
### DC01PE63   构建长度为2且两个结点的值依次为x和y的链表
链表的结点和指针类型定义如下
    typedef struct LNode {
       ElemType  data;
       struct LNode *next;
    } LNode, *LinkList;
试写一函数，构建长度为2且两个结点的值依次为x和y的链表。
要求实现下列函数：
LinkList CreateLinkList(ElemType x, ElemType y); 
/* 构建其两个结点的值依次为x和y的链表。*/
/* 若构建失败，则返回NULL。            */

```c
#include "allinclude.h"  //DO NOT edit this line
LinkList CreateLinkList(ElemType x, ElemType y) { 
    // Add your code here
  LNode*p;
  p = (LNode*)malloc(sizeof(LNode));
  if(NULL == p) return NULL;
  else{
    p->next = (LNode*)malloc(sizeof(LNode));
    if(NULL == p->next) return NULL;
    p->data = x;
    p->next->data = y;
    p->next->next = NULL;
  }
  return p;
}
```
### DC01PE65  构建长度为2的升序链表
链表的结点和指针类型定义如下
    typedef struct LNode {
       ElemType  data;
       struct LNode *next;
    } LNode, *LinkList;
试写一函数，构建长度为2的升序链表，两个结点的值
分别为x和y，但应小的在前，大的在后。
要求实现下列函数：
LinkList CreateOrdLList(ElemType x, ElemType y); 
/* 构建长度为2的升序链表。    */
/* 若构建失败，则返回NULL。   */

```c
#include "allinclude.h"  //DO NOT edit this line
LinkList CreateOrdLList(ElemType x, ElemType y) { 
    // Add your code here
    LNode*p;
    p=(LNode*)malloc(sizeof(LNode));
    if(NULL == p) return NULL;
    else{
      p->next=(LNode*)malloc(sizeof(LNode));
      if(NULL == p->next) {
        return NULL;
      }else{
        p->data = (x < y)? x : y;
        p->next->data = (x > y)? x : y;
        p->next->next = NULL;
      }
      return p;
    }
}
```

## 第二章
### DC02PE03 实现顺序栈的判空操作
试写一算法，实现顺序栈的判空操作
StackEmpty_Sq(SqStack S)。
要求实现下列函数：
Status StackEmpty_Sq(SqStack S); 
/* 对顺序栈S判空。                      */ 
/* 若S是空栈，则返回TRUE；否则返回FALSE */
顺序栈的类型定义为：
typedef struct {
  ElemType *elem;  // 存储空间的基址
  int top;         // 栈顶元素的下一个位置，简称栈顶位标
  int size;        // 当前分配的存储容量
  int increment;   // 扩容时，增加的存储容量
} SqStack;         // 顺序栈

```c
#include "allinclude.h"  //DO NOT edit this line
Status StackEmpty_Sq(SqStack S) { 
    // Add your code here
  if(S.top == 0){
    return TRUE;
  }else{
    return FALSE;
  }
}
```
### DC02PE05  实现顺序栈的取栈顶元素操作
试写一算法，实现顺序栈的取栈顶元素操作
GetTop_Sq(SqStack S, ElemType &e)。
要求实现下列函数：
Status GetTop_Sq(SqStack S, ElemType &e);
/* 取顺序栈S的栈顶元素到e，并返回OK； */ 
/* 若失败，则返回ERROR。              */
顺序栈的类型定义为：
typedef struct {
  ElemType *elem;  // 存储空间的基址
  int top;         // 栈顶元素的下一个位置，简称栈顶位标
  int size;        // 当前分配的存储容量
  int increment;   // 扩容时，增加的存储容量
} SqStack;         // 顺序栈

```c
#include "allinclude.h"  //DO NOT edit this line
Status GetTop_Sq(SqStack S, ElemType &e) { 
    // Add your code here
    if(S.top == 0){
      return ERROR;
    }else{
      e = S.elem[S.top-1];
      return OK;
    }
}
```
### DC02PE07  实现顺序栈的出栈操作
试写一算法，实现顺序栈的出栈操作
Pop_Sq(SqStack &S, ElemType &e)。
要求实现下列函数：
Status Pop_Sq(SqStack &S, ElemType &e); 
/* 顺序栈S的栈顶元素出栈到e，并返回OK；*/ 
/* 若失败，则返回ERROR。               */
顺序栈的类型定义为：
typedef struct {
  ElemType *elem;  // 存储空间的基址
  int top;         // 栈顶元素的下一个位置，简称栈顶位标
  int size;        // 当前分配的存储容量
  int increment;   // 扩容时，增加的存储容量
} SqStack;         // 顺序栈

```c
#include "allinclude.h"  //DO NOT edit this line
Status Pop_Sq(SqStack &S, ElemType &e) { 
    // Add your code here
  if(S.top == 0){
      return ERROR;
    }else{
      e = S.elem[--S.top];
      return OK;
    }
}
```
### DC02PE11  构建初始容量和扩容增量分别为size和inc的空顺序栈S
若顺序栈的类型重新定义如下。试编写算法，构建初始容量和扩容增量分别为size和inc的空顺序栈S。
typedef struct {
  ElemType *elem; // 存储空间的基址
  ElemType *top;  // 栈顶元素的下一个位置
  int size;       // 当前分配的存储容量
  int increment;  // 扩容时，增加的存储容量
} SqStack2;
要求实现下列函数：
Status InitStack_Sq2(SqStack2 &S, int size, int inc); 
/* 构建初始容量和扩容增量分别为size和inc的空顺序栈S。*/ 
/* 若成功，则返回OK；否则返回ERROR。                 */

```c
#include "allinclude.h"  //DO NOT edit this line
Status InitStack_Sq2(SqStack2 &S, int size, int inc) { 
    // Add your code here
  S.elem = (ElemType*)malloc(size*sizeof(ElemType));
  if(NULL == S.elem||size <= 0 || inc <=0) return ERROR;
    else{
      S.top = S.elem;
      S.size = size;
      S.increment = inc;
       return OK;
    }
}
```
### DC02PE13 实现顺序栈的判空操作
若顺序栈的类型重新定义如下。试编写算法，
实现顺序栈的判空操作。
typedef struct {
  ElemType *elem; // 存储空间的基址
  ElemType *top;  // 栈顶元素的下一个位置
  int size;       // 当前分配的存储容量
  int increment;  // 扩容时，增加的存储容量
} SqStack2;
要求实现下列函数：
Status StackEmpty_Sq2(SqStack2 S); 
/* 对顺序栈S判空。                      */ 
/* 若S是空栈，则返回TRUE；否则返回FALSE */

```c
#include "allinclude.h"  //DO NOT edit this line
Status StackEmpty_Sq2(SqStack2 S) { 
    // Add your code here
    if(S.top == S.elem){
      return TRUE;
    }else{
      return FALSE;
    }
}
```
### DC02PE15 实现顺序栈的入栈操作
若顺序栈的类型重新定义如下。试编写算法，实现顺序栈的入栈操作。
typedef struct {
  ElemType *elem; // 存储空间的基址
  ElemType *top;  // 栈顶元素的下一个位置
  int size;       // 当前分配的存储容量
  int increment;  // 扩容时，增加的存储容量
} SqStack2;
要求实现下列函数：
Status Push_Sq2(SqStack2 &S, ElemType e); 
/* 若顺序栈S是满的，则扩容，若失败则返回ERROR。*/
/* 将e压入S，返回OK。                          */

```c
#include "allinclude.h"  //DO NOT edit this line
Status Push_Sq2(SqStack2 &S, ElemType e) { 
    // Add your code here
    ElemType*newbase;
    if(*(S.top) >= S.size){
      newbase = (ElemType*)realloc(S.elem,(S.size+S.increment)*sizeof(ElemType));
      if(NULL == newbase) return ERROR;
      S.elem = newbase;
      S.size += S.increment;
    }
    *(S.top++) = e;
    return OK;
}
```
### DC02PE17 实现顺序栈的出栈操作
若顺序栈的类型重新定义如下。试编写算法，实现顺序栈的出栈操作。
typedef struct {
  ElemType *elem; // 存储空间的基址
  ElemType *top;  // 栈顶元素的下一个位置
  int size;       // 当前分配的存储容量
  int increment;  // 扩容时，增加的存储容量
} SqStack2;
要求实现下列函数：
Status Pop_Sq2(SqStack2 &S, ElemType &e); 
/* 若顺序栈S是空的，则返回ERROR；    */ 
/* 否则将S的栈顶元素出栈到e，返回OK。*/

```c
#include "allinclude.h"  //DO NOT edit this line
Status Pop_Sq2(SqStack2 &S, ElemType &e) { 
    // Add your code here
  if(S.top == S.elem){
    return ERROR;
  }else{
    e = *(--S.top);
  }
  return OK;
}
```
### DC02PE19 借助辅助栈，复制顺序栈S1得到S2
试写一算法，借助辅助栈，复制顺序栈S1得到S2。
Status CopyStack_Sq(SqStack S1, SqStack &S2)。
要求实现下列函数：
Status CopyStack_Sq(SqStack S1, SqStack &S2); 
/* 借助辅助栈，复制顺序栈S1得到S2。    */ 
/* 若复制成功，则返回TRUE；否则FALSE。 */
顺序栈的类型定义为：
typedef struct {
  ElemType *elem;  // 存储空间的基址
  int top;         // 栈顶元素的下一个位置，简称栈顶位标
  int size;        // 当前分配的存储容量
  int increment;   // 扩容时，增加的存储容量
} SqStack;         // 顺序栈
可调用顺序栈接口中下列函数：
Status InitStack_Sq(SqStack &S, int size, int inc); // 初始化顺序栈S
Status DestroyStack_Sq(SqStack &S); // 销毁顺序栈S
Status StackEmpty_Sq(SqStack S);    // 栈S判空，若空则返回TRUE，否则FALSE
Status Push_Sq(SqStack &S, ElemType e); // 将元素e压入栈S
Status Pop_Sq(SqStack &S, ElemType &e); // 栈S的栈顶元素出栈到e

```c
#include "allinclude.h"  //DO NOT edit this line
Status CopyStack_Sq(SqStack S1, SqStack &S2) { 
    // Add your code here
    if(StackEmpty_Sq(S1)){
      S2.top =0;
      return TRUE;
    }else{
      S2.elem = S1.elem;
      S2.top = S1.top;
      return TRUE;
    }
}
```
### DC02PE23 求循环队列的长度
试编写算法，求循环队列的长度。
循环队列的类型定义为：
typedef struct {
  ElemType *base;  // 存储空间的基址
  int front;       // 队头位标
  int rear;        // 队尾位标，指示队尾元素的下一位置
  int maxSize;     // 最大长度
} SqQueue;
要求实现下列函数：
int QueueLength_Sq(SqQueue Q); 
/* 返回队列Q中元素个数，即队列的长度。*/ 

```c
#include "allinclude.h"  //DO NOT edit this line
int QueueLength_Sq(SqQueue Q) { 
    // Add your code here
    return (Q.rear-Q.front+Q.maxSize)%Q.maxSize;
}
```
### DC02PE25 编写入队列和出队列的算法
如果希望循环队列中的元素都能得到利用，
则可设置一个标志域tag，并以tag值为0或1来区分尾
指针和头指针值相同时的队列状态是"空"还是"满"。
试编写与此结构相应的入队列和出队列的算法。
本题的循环队列CTagQueue的类型定义如下：
typedef struct {
  ElemType elem[MAXQSIZE];
  int tag;
  int front;
  int rear;
} CTagQueue;
实现下列函数：
Status EnCQueue(CTagQueue &Q, ElemType x);
  /* 将元素x加入队列Q，并返回OK；*/
  /* 若失败，则返回ERROR。       */
Status DeCQueue(CTagQueue &Q, ElemType &x);
  /* 将队列Q的队头元素退队到x，并返回OK；*/
  /* 若失败，则返回ERROR。               */


```c
#include "allinclude.h"  //DO NOT edit this line
Status EnCQueue(CTagQueue &Q, ElemType x) { 
    // Add your code here
    if(Q.front == Q.rear && Q.tag == 1)
      return ERROR;
      else{
        Q.elem[Q.rear] = x;
        Q.rear = (Q.rear+1)%MAXQSIZE;
      }
      if(Q.front==Q.rear)
      Q.tag=1;
      return OK;
}
Status DeCQueue(CTagQueue &Q, ElemType &x){
  if(Q.front == Q.rear && Q.tag == 0)
  return ERROR;
  else{
    x = Q.elem[Q.front];
    Q.front = (Q.front+1)%MAXQSIZE;
  }
  if(Q.front==Q.rear)
  Q.tag=0;
  return OK;
}
```
### DC02PE27 写出循环队列的入队列和出队列的算法
假设将循环队列定义为：以域变量rear和length分别指示循环队列中队尾元素的位置和内含元素的个数。试给出此循环队列的队满条件，并写出相应的入队列和出队列的算法（在出队列的算法中要返回队头元素）。

本题的循环队列CLenQueue的类型定义如下：
typedef struct {
  ElemType elem[MAXQSIZE];
  int length;
  int rear;
} CLenQueue;
实现下列函数：
Status EnCQueue(CLenQueue &Q, ElemType x);
  /* 将元素x加入队列Q，并返回OK；*/
  /* 若失败，则返回ERROR。       */
Status DeCQueue(CLenQueue &Q, ElemType &x);
  /* 将队列Q的队头元素退队到x，并返回OK；*/
  /* 若失败，则返回ERROR。               */


```c
#include "allinclude.h"  //DO NOT edit this line
Status EnCQueue(CLenQueue &Q, ElemType x) { 
    // Add your code here
    if(Q.length==MAXQSIZE) return ERROR;
    Q.rear=(Q.rear+1)%MAXQSIZE;
    Q.elem[Q.rear]=x;
    Q.length++;
    return OK;
}

Status DeCQueue(CLenQueue &Q, ElemType &x){
    // Add your code here
    if(Q.length==0) return ERROR;
    x=Q.elem[(Q.rear+MAXQSIZE-Q.length+1)%MAXQSIZE];
    Q.length--;
    return OK;
}
```
### DC02PE32 利用循环队列编写求k阶斐波那契序列中第n+1项fn的算法
已知k阶斐波那契序列的定义为:
    f0=0,  f1=0,  …,  fk-2=0,  fk-1=1;
    fn=fn-1+fn-2+…+fn-k,  n=k,k+1,…
试利用循环队列编写求k阶斐波那契序列中第n+1项fn的算法。

本题的循环队列的类型定义如下：
typedef struct {
  ElemType *base; // 存储空间的基址
  int front;      // 队头位标
  int rear;       // 队尾位标，指示队尾元素的下一位置
  int maxSize;    // 最大长度
} SqQueue;
要求实现下列函数：
long Fib(int k, int n);
/* 求k阶斐波那契序列的第n+1项fn */

```c
#include "allinclude.h"  //DO NOT edit this line
long Fib(int k, int n) { 
    // Add your code here
    if(k<2||n<0) return ERROR;
    if(n<k-1)  return 0;
    else if(n==k-1)  return 1;
    else{
      SqQueue S;
      S.base=(ElemType*)malloc((n+1)*sizeof(ElemType));
      S.base[k-1]=1;
      int i,j,sum;
      for(i = 0; i < k-1; i++){
        S.base[i]=0;
      }
      for (i = k; i < n+1; i++) {
        /* code */
        sum=0;
        for (j = i-k; j < i ; j++) {
          /* code */
          sum+=S.base[j];
        }
          S.base[i]=sum;
        }
        return S.base[n];
      }
}
```
### DC02PE33 试写一个比较A和B大小的算法
设A=(a1,…,am)和B=(b1,…,bn)均为有序顺序表，
A'和B'分别为A和B中除去最大共同前缀后的子表（例如，
A=(x,y,y,z,x,z)，B=(x,y,y,z,y,x,x,z)，则两者中最大
的共同前缀为(x,y,y,z)， 在两表中除去最大共同前缀后
的子表分别为A'=(x,z)和B'=(y,x,x,z)）。若A'=B'=空表，
则A=B；若A'=空表，而B'≠ 空表，或者两者均不为空表，
且A'的首元小于B'的首元，则A<B；否则A>B。试写一个比
较A和B大小的算法。（注意：在算法中，不要破坏原表A
和B，也不一定先求得A'和B'才进行比较）。
顺序表类型定义如下：
typedef struct {
  ElemType *elem;
  int       length;
  int       size;
  int       increment;
} SqList;
要求实现下列函数：
char Compare(SqList A, SqList B);
/* 比较顺序表A和B,      */
/*   返回'<', 若A<B;    */
/*       '=', 若A=B;    */
/*       '>', 若A>B     */

```c
#include "allinclude.h"  //DO NOT edit this line
char Compare(SqList A, SqList B) { 
    // Add your code here
    int i =  0;
    while((i <= A.length-1) && (i <= B.length-1) && (A.elem[i] == B.elem[i])){
      ++i;
    } if(i == A.length && i == B.length){
      return '=';
    }else if(i == A.length && i != B.length && A.elem[i] < B.elem[i]){
      return '<';
    }else if(i != A.length && i != B.length && A.elem[i] < B.elem[i]){
      return '<';
    }else{
      return '>';
    }
}
```
### DC02PE35 试写一算法，实现顺序表的就地逆置
试写一算法，实现顺序表的就地逆置，即利用原表的存储空间将线性表(a1,a2,…,an)逆置为(an,an-1,…,a1)。
顺序表类型定义如下：
typedef struct {
  ElemType *elem;
  int       length;
  int       size;
  int       increment;
} SqList;
实现下列函数：
void Inverse(SqList &L);

```c
#include "allinclude.h"  //DO NOT edit this line
void Inverse(SqList &L) { 
    // Add your code here
    ElemType temp;
    if(L.elem != 0 && L.length != 1){
      for (int i = 0; i < L.length/2; i++) {
        /* code */
        temp = L.elem[i];
        L.elem[i] = L.elem[L.length - 1 - i];
        L.elem[L.length - 1 - i] = temp;
      }
    }
}
```
### DC02PE45 试写一算法，求并集A＝A∪B
假设有两个集合A和B分别用两个线性表LA和LB
表示(即：线性表中的数据元素即为集合中的成员），
试写一算法，求并集A＝A∪B。
顺序表类型定义如下
typedef struct {
  ElemType *elem;  // 存储空间的基址
  int length;    // 当前长度
  int size;      // 存储容量 
  int increment; // 空间不够增加空间大小
} SqList;  // 顺序表
可调用顺序表的以下接口函数：   
Status InitList_Sq(SqList &L, int size, int inc); // 初始化顺序表L
int ListLength_Sq(SqList L);  // 返回顺序表L中元素个数
Status GetElem_Sq(SqList L, int i, ElemType &e); 
  // 用e返回顺序表L中第i个元素的值
int Search_Sq(SqList L, ElemType e); 
  // 在顺序表L顺序查找元素e，成功时返回该元素在表中第一次出现的位置，否则返回-1
Status Append_Sq(SqList &L, ElemType e);  // 在顺序表L表尾添加元素e
实现如下算法：
void Union(SqList &La, List Lb)。

```c
#include "allinclude.h"  //DO NOT edit this line
void Union(SqList &La, List Lb){ 
    // Add your code here
    int count = 0;
    int la = ListLength_Sq(La);
    int lb = ListLength_Sq(Lb);
    for (int i = 0; i < lb; i++) {
      /* code */
      if(Search_Sq(La , Lb.elem[i]) == -1){
        count++;
      }
      ElemType * p;
      p = (ElemType*)realloc(La.elem ,La.size + count*sizeof(ElemType));
      if(NULL == p){
        return ;
      }
      La.elem = p;
      for (int i = 0; i < lb; i++) {
        /* code */
        if(Search_Sq(La , Lb.elem[i]) == -1){
          Append_Sq(La , Lb.elem[i]);
        }
      }
    }
}
```
### DC02PE53 试写一算法，实现链栈的判空操作
试写一算法，实现链栈的判空操作。
链栈的类型定义为：
typedef struct LSNode {
  ElemType data;       // 数据域
  struct LSNode *next; // 指针域
} LSNode, *LStack; // 结点和链栈类型
要求实现下列函数：
Status StackEmpty_L(LStack S); 
/* 对链栈S判空。若S是空栈，则返回TRUE；否则返回FALSE */
```c
#include "allinclude.h"  //DO NOT edit this line
Status StackEmpty_L(LStack S){ 
    // Add your code here
    if(NULL == S){
      return true;
    } else{
      return FALSE;
    }   
}
```
### DC02PE55 试写一算法，实现链栈的取栈顶元素操作
试写一算法，实现链栈的取栈顶元素操作。
链栈的类型定义为：
typedef struct LSNode {
  ElemType data;       // 数据域
  struct LSNode *next; // 指针域
} LSNode, *LStack; // 结点和链栈类型
要求实现下列函数：
Status GetTop_L(LStack S, ElemType &e); 
/* 取链栈S的栈顶元素到e，并返回OK; */
/* 若S是空栈，则失败，返回ERROR。  */

```c
#include "allinclude.h"  //DO NOT edit this line
Status GetTop_L(LStack S, ElemType &e){ 
    // Add your code here
    if(NULL == S) return ERROR;
    e = S->data;
    return OK;
}
```
### DC02PE61 实现链队列的判空操作
试写一算法，实现链队列的判空操作。
链队列的类型定义为：
typedef struct LQNode {     
  ElemType  data;  
  struct LQNode  *next;  
} LQNode, *QueuePtr; // 结点和结点指针类型
typedef struct {     
  QueuePtr  front;  // 队头指针
  QueuePtr  rear;   // 队尾指针
} LQueue;  // 链队列类型
要求实现下列函数：
Status QueueEmpty_LQ(LQueue Q);
/* 判定链队列Q是否为空队列。           */
/* 若Q是空队列，则返回TRUE，否则FALSE。*/

```c
#include "allinclude.h"  //DO NOT edit this line
Status QueueEmpty_LQ(LQueue Q){ 
    // Add your code here
    if(Q.front == NULL) return TRUE;
    return FALSE;
}
```
### DC02PE63 实现链队列的求队列长度操作
试写一算法，实现链队列的求队列长度操作。
链队列的类型定义为：
typedef struct LQNode {     
  ElemType  data;  
  struct LQNode  *next;  
} LQNode, *QueuePtr; // 结点和结点指针类型
typedef struct {     
  QueuePtr  front;  // 队头指针
  QueuePtr  rear;   // 队尾指针
} LQueue;  // 链队列类型
要求实现下列函数：
int QueueLength_LQ(LQueue Q);
/* 求链队列Q的长度并返回其值 */

```c
#include "allinclude.h"  //DO NOT edit this line
int QueueLength_LQ(LQueue Q){ 
    // Add your code here
  if(Q.front == NULL){
      return 0;
    }
    int len = 0;
    LQNode * p = Q.front;
    while(p != NULL){
      p = p->next;
      len++;
    }
    return len;
}

```
### DC02PE68 编写队列初始化、入队列和出队列的算法
假设以带头结点的循环链表表示队列，并且
只设一个指针指向队尾元素结点(注意不设头指针)，
试编写相应的队列初始化、入队列和出队列的算法。
带头结点循环链队列CLQueue的类型定义为：
typedef struct LQNode {
  ElemType data;
  struct LQNode *next;
} LQNode, *CLQueue;
实现下列函数：
Status InitCLQueue(CLQueue &rear); // 初始化空队列
Status EnCLQueue(CLQueue &rear, ElemType x); // 入队
Status DeCLQueue(CLQueue &rear, ElemType &x); // 出队
```c
#include "allinclude.h"  //DO NOT edit this line
Status InitCLQueue(CLQueue &rear){ 
    // Add your code here
    rear = (CLQueue)malloc(sizeof(LQNode));
    if(NULL == rear) return FALSE;
    rear->next = rear;
    return TRUE;
} 

Status EnCLQueue(CLQueue &rear, ElemType x){ 
    // Add your code here
    CLQueue head,p;
    head = rear->next;
    p = (CLQueue)malloc(sizeof(LQNode));
    if(NULL == p){
      return FALSE;
    }
    p->data = x;
    p->next = head;
    rear->next = p;
    rear = p;
    return TRUE;
}

Status DeCLQueue(CLQueue &rear, ElemType &x){ 
    // Add your code here
    CLQueue head,p;
    head = rear->next;
    if(head == rear){
      return FALSE;
    }
    p = head->next;
    x = p->data;
    head->next = p->next;
    free(p);
    return TRUE;   
}
```
### DC02PE71 实现带头结点单链表的判空操作
试写一算法，实现带头结点单链表的判空操作。
单链表的类型定义为：
typedef struct LNode {     
  ElemType  data;  
  struct LNode  *next;  
} LNode, *LinkList; // 结点和结点指针类型
要求实现下列函数：
Status ListEmpty_L(LinkList L);
/* 判定带头结点单链表L是否为空链表。   */
/* 若L是空链表，则返回TRUE，否则FALSE。*/

```c
#include "allinclude.h"  //DO NOT edit this line
Status ListEmpty_L(LinkList L){ 
    // Add your code here
  if(L == NULL || L->next == NULL){
    return TRUE;
  }else{
    return FALSE;
  }
} 
```
### DC02PE73 实现带头结点单链表的销毁操作
试写一算法，实现带头结点单链表的销毁操作。
单链表的类型定义为：
typedef struct LNode {     
  ElemType  data;  
  struct LNode  *next;  
} LNode, *LinkList; // 结点和结点指针类型
要求实现下列函数：
Status DestroyList_L(LinkList &L);
/* 销毁带头结点单链表L，并返回OK。*/

```c
#include "allinclude.h"  //DO NOT edit this line
Status DestroyList_L(LinkList &L){ 
    // Add your code here
   LNode *q;
   while(L){
     q = L->next;
     free(L);
     L = q;
   }
   return OK;
}
```
### DC02PE75 实现带头结点单链表的清空操作
试写一算法，实现带头结点单链表的清空操作。
单链表的类型定义为：
typedef struct LNode {     
  ElemType  data;  
  struct LNode  *next;  
} LNode, *LinkList; // 结点和结点指针类型
要求实现下列函数：
Status ClearList_L(LinkList &L);
/* 将带头结点单链表L置为空表，并返回OK。*/
/* 若L不是带头结点单链表，则返回ERROR。 */

```c
#include "allinclude.h"  //DO NOT edit this line
Status ClearList_L(LinkList &L){ 
    // Add your code here
    if(L == NULL) return ERROR;
    LNode *p,*q;
    p = L->next;
    while(p){
      q = p->next;
      free(p);
      p = q;
    }
    L->next = NULL;
    return OK;
} 
```
### DC02PE77 实现带头结点单链表的求表长度操作
试写一算法，实现带头结点单链表的求表长度操作。
单链表的类型定义为：
typedef struct LNode {     
  ElemType  data;  
  struct LNode  *next;  
} LNode, *LinkList; // 结点和结点指针类型
要求实现下列函数：
int ListLength_L(LinkList L);
/* 求带头结点单链表L的长度，并返回长度值。*/
/* 若L不是带头结点单链表，则返回-1。      */

```c
#include "allinclude.h"  //DO NOT edit this line
int ListLength_L(LinkList L){ 
    // Add your code here
    if(L == NULL) return -1;
    int count = 0;
    while(L){
      count++;
      L = L->next;
    }
    count--;
    return count;
} 
```
### DC02PE82 在带头结点单链表L插入第i元素e
试写一算法，在带头结点单链表L插入第i元素e。
带头结点单链表的类型定义为：
typedef struct LNode {
  ElemType      data;
  struct LNode *next;
} LNode, *LinkList;
实现下列函数：
Status Insert_L(LinkList L, int i, ElemType e);
/* 在带头结点单链表L插入第i元素e，并返回OK。*/
/* 若参数不合理，则返回ERROR。              */

```c
#include "allinclude.h"  //DO NOT edit this line
Status Insert_L(LinkList L, int i, ElemType e){ 
    // Add your code here
    if(i < 0) return ERROR;
    int count = 0;
    LinkList p = L;
    while(p != NULL && count < i-1){
      p = p->next;
      count++;
    }
    if(!p || count > i-1) return ERROR;
    LinkList ptr;
    ptr = (LNode*)malloc(sizeof(LNode));
    ptr->data = e;
    ptr->next = p->next;
    p->next = ptr;
    return OK;
} 
```
### DC02PE84 在带头结点单链表删除第i元素到e
试写一算法，在带头结点单链表删除第i元素到e。

带头结点单链表的类型定义为：
typedef struct LNode {
  ElemType      data;
  struct LNode *next;
} LNode, *LinkList;
实现下列函数：
Status Delete_L(LinkList L, int i, ElemType &e);
/* 在带头结点单链表L删除第i元素到e，并返回OK。*/
/* 若参数不合理，则返回ERROR。                */

```c
#include "allinclude.h"  //DO NOT edit this line
Status Delete_L(LinkList L, int i, ElemType &e){ 
    // Add your code here
    LinkList p = L , pt;
    int count = 0;
    while( p->next && count < i-1){
      p = p->next;
      count++;
    }
    if(!(p->next) || count > i-1) return ERROR;
    pt = p->next;
    p->next = pt->next;
    e = pt->data;
    free(pt);
    return OK;
}
```
### DC02PE86 在带头结点单链表的第i元素起的所有元素从链表移除，并构成一个带头结点的新链表
试写一算法，在带头结点单链表的第i元素起的所有元素从链表移除，并构成一个带头结点的新链表。
带头结点单链表的类型定义为：
typedef struct LNode {
  ElemType      data;
  struct LNode *next;
} LNode, *LinkList;
实现下列函数：
Status Split_L(LinkList L, LinkList &Li, int i);
/* 在带头结点单链表L的第i元素起的所有元素 */
/* 移除，并构成带头结点链表Li，返回OK。   */
/* 若参数不合理，则Li为NULL，返回ERROR。  */

```c
#include "allinclude.h"  //DO NOT edit this line
Status Split_L(LinkList L, LinkList &Li, int i){ 
    // Add your code here
    int count = 0;
    LinkList p = L , pt;
    while(p != NULL && count < i-1){
      p = p->next;
      count++;
    }
    if(i < 0 || p == NULL || count > i-1 || p->next == NULL){
      Li = NULL;
      return ERROR;
    }pt = (LinkList)malloc(sizeof(LNode));
    if(pt == NULL) return ERROR;
    Li = pt;
    Li->next = p->next;
    p->next = NULL;
    return OK;
} 
```
### DC02PE88 试写一算法，在带头结点单链表删除第i元素起的所有元素
试写一算法，在带头结点单链表删除第i元素起的所有元素。
带头结点单链表的类型定义为：
typedef struct LNode {
  ElemType      data;
  struct LNode *next;
} LNode, *LinkList;
实现下列函数：
Status Cut_L(LinkList L, int i);
/* 在带头结点单链表L删除第i元素起的所有元素，并返回OK。*/
/* 若参数不合理，则返回ERROR。                         */

```c
#include "allinclude.h"  //DO NOT edit this line
Status Cut_L(LinkList L, int i){ 
    // Add your code here
    int count= 0; 
     LinkList p= L, pt;      
     while(p !=NULL && count < i-1){
       p = p->next;          
       count++;      
       
     } 
     if(i <= 0 || p == NULL || count > i-1 || p->next == NULL)      {      
     return ERROR;        
     } 
     if(i == 1){ 
     free(L->next);      
     L->next=NULL;      
     return OK;      
    } 
     pt = p->next;         
     p->next = NULL;      
     while(pt != NULL){ 
     p = pt->next;      
     free(pt);      
     pt = p;      
     }      
     return OK; 
} 
```
### DC02PE90 删除带头结点单链表中所有值为x的元素
试写一算法，删除带头结点单链表中所有值为x的元素，并释放被删结点空间。
单链表类型定义如下：
typedef struct LNode {
  ElemType      data;
  struct LNode *next;
} LNode, *LinkList;
实现下列函数：
Status DeleteX_L(LinkList L, ElemType x);
/* 删除带头结点单链表L中所有值为x的元素，      */
/* 并释放被删结点空间，返回实际删除的元素个数。*/

```c
#include "allinclude.h"  //DO NOT edit this line
Status DeleteX_L(LinkList L, ElemType x) { 
    // Add your code here
  int count = 0;
  LinkList p =L->next , pt = L , q;
  while(p != NULL){
    if(p->data == x){
      q = p;
      p = p->next;
      free(q);
      pt->next = p;
      count++;
    }else{
      pt = p;
      p = p->next;
    }
  }
  return count;
}
```
### DC02PE91 删除带头结点单链表中所有值小于x的元素
试写一算法，删除带头结点单链表中所有值小于x的元素，并释放被删结点空间。

单链表类型定义如下：
typedef struct LNode {
  ElemType      data;
  struct LNode *next;
} LNode, *LinkList;
实现下列函数：
Status DeleteSome_L(LinkList L, ElemType x);
/* 删除带头结点单链表L中所有值小于x的元素，    */
/* 并释放被删结点空间，返回实际删除的元素个数。*/

```c
#include "allinclude.h"  //DO NOT edit this line
Status DeleteSome_L(LinkList L, ElemType x) { 
    // Add your code here
    int count = 0;
  LinkList p =L->next , pt = L , q;
  while(p != NULL){
    if(p->data < x){
      q = p;
      p = p->next;
      free(q);
      pt->next = p;
      count++;
    }else{
      pt = p;
      p = p->next;
    }
  }
  return count;
}
```

## 第三章
### DC03PE03 改写直接插入排序算法
试以顺序表L的L.rcd[L.length+1]作为监视哨，改写教材3.2节中给出的升序直接插入排序算法。
顺序表的类型RcdSqList定义如下：
typedef struct {
   KeyType key; 
   ... 
} RcdType;
typedef struct {
   RcdType rcd[MAXSIZE+1]; // rcd[0]闲置
   int length;
} RcdSqList;
实现下列函数：
void InsertSort(RcdSqList &L);

```c
#include "allinclude.h"  //DO NOT edit this line
void InsertSort(RcdSqList &L)
{ 
  int i,j;
  for (i = 1; i < L.length ; i++) {
    /* code */
    if(L.rcd[i + 1].key < L.rcd[i].key){
      L.rcd[L.length + 1].key = L.rcd[i + 1].key;
      j = i + 1;
      do{
        j--;
        L.rcd[j + 1].key = L.rcd[j].key;
      }while(L.rcd[L.length + 1].key < L.rcd[j - 1].key);
      L.rcd[j].key = L.rcd[L.length + 1].key;
    }
  }
}
```
### DC03PE06 改进的冒泡排序
如下所述，改写教材1.5节的冒泡排序算法：
将算法中用以起控制作用的布尔变量change改为一个整型变量，指示每一趟排序中进行交换的最后一个记录的位置，并以它作为下一趟起泡排序循环终止的控制值。
顺序表的类型RcdSqList定义如下：
typedef struct {
   KeyType key; 
   ... 
} RcdType;
typedef struct {
   RcdType rcd[MAXSIZE+1]; // rcd[0]闲置
   int length;
} RcdSqList;
实现下列函数：
void BubbleSort(RcdSqList &L);
/* 元素比较和交换必须调用以下比较函数和交换函数：*/
/* Status LT(RedType a, RedType b);   比较："<"  */
/* Status GT(RedType a, RedType b);   比较：">"  */
/* void Swap(RedType &a, RedType &b); 交换       */
比较函数和交换函数:
Status LT(RedType a, RedType b);   // 比较函数："<"
Status GT(RedType a, RedType b);   // 比较函数：">"
void Swap(RedType &a, RedType &b); // 交换函数

```c
#include "allinclude.h"  //DO NOT edit this line
void BubbleSort(RcdSqList &L)
/* 元素比较和交换必须调用如下定义的比较函数和交换函数：*/
/* Status LT(RedType a, RedType b);   比较："<"        */
/* Status GT(RedType a, RedType b);   比较：">"        */
/* void Swap(RedType &a, RedType &b); 交换             */
{
    int i,j,change=1;
    for(i=L.length;i>1&&change;i=change){
        change=0;
        for(j=1;j<i;j++)
            if(GT(L.rcd[j],L.rcd[j+1])){
                Swap(L.rcd[j],L.rcd[j+1]);
                change=j;
            } 
    }                
}
```
### DC03PE23 计数排序
已知记录序列L.rcd[1..L.length]中的关键字各不相同，可按如下所述实现计数排序：另设数组c[1..n]，对每个记录a[i]， 统计序列中关键字比它小的记录个数存于c[i]，则c[i]=0的记录必为关键字最小的记录，然后依c[i]值的大小对序列中记录进行重新排列。试编写算法实现上述排序方法。
顺序表的类型RcdSqList定义如下：
typedef struct {
   KeyType key; 
   ... 
} RcdType;
typedef struct {
   RcdType rcd[MAXSIZE+1]; // rcd[0]闲置
   int     length;
} RcdSqList;
实现下列函数：
void CountSort(RcdSqList &L);
/* 采用顺序表存储结构，在函数内自行定义计数数组c */

```c
#include "allinclude.h"  //DO NOT edit this line
void CountSort(RcdSqList &L)
/* 采用顺序表存储结构，在函数内自行定义计数数组c */
{ 
  // Add your code here
  int *c;
  c = (int*)malloc((L.length+1)*sizeof(int));
  KeyType * temp;
  temp = (KeyType*)malloc((L.length+1)*sizeof(int));
  int i,j;
  for (i = 0; i < L.length+1; i++) {
    /* code */
    c[i] = 0;
  }
    for (i = 1; i < L.length+1; i++) {
      /* code */
      for (j = 1; j < L.length+1; j++) {
        /* code */
        if(L.rcd[i].key>L.rcd[j].key){
          c[i]++;
        }
      }
    }
    for (i = 1; i < L.length+1; i++) {
      /* code */
      temp[c[i]+1] = L.rcd[i].key; 
    }
    for (j = 1; j < L.length+1; j++) {
      /* code */
      L.rcd[j].key = temp[j];
    }

}
```

## 第四章
### DC04PE04 哈希表中关键字的有序输出
已知某哈希表的装载因子小于1，哈希函数H(key)为关键字(标识符)的第一个字母在字母表中的序号，处理冲突的方法为线性探测开放定址法。试编写一个按第一个字母的顺序输出哈希表中所有关键字的算法。
哈希表的类型HashTable定义如下：
#define SUCCESS    1
#define UNSUCCESS  0
#define DUPLICATE -1
typedef char StrKeyType[4];
typedef struct {
   StrKeyType key; // 关键字项
   int    tag;     // 标记 0:空；1:有效; -1:已删除
   void  *any;     // 其他信息
} RcdType;
typedef struct {
  RcdType *rcd;    // 存储空间基址
  int      size;   // 哈希表容量
  int      count;  // 表中当前记录个数
} HashTable;
实现下列函数：
void PrintKeys(HashTable ht, void(*print)(StrKeyType));
/* 依题意用print输出关键字 */

```c
#include "allinclude.h"  //DO NOT edit this line
void PrintKeys(HashTable ht, void(*print)(StrKeyType)){
/* 依题意用print输出关键字 */
  int n , i;
  for (char c = 'A' ; c <= 'Z'  ; c++) {
    /* code */
    n = (c - 'A') % ht.size;
    i = n;
    while((n + 1) % ht.size  != i){
      if(-1 != ht.rcd[n].tag && ht.rcd[n].key[0] == c)
      print(ht.rcd[n].key);
      n  = (n + 1) % ht.size;
    }
  }
}
```

### DC04PE15 链地址哈希表的构造
假设哈希表长为m，哈希函数为H(x)，用链地址法处理冲突。试编写输入一组关键字并建造哈希表的算法。

哈希表的类型ChainHashTab定义如下：
#define NUM         7
#define NULLKEY    -1
#define SUCCESS     1
#define UNSUCCESS   0
#define DUPLICATE  -1

typedef char HKeyType;

typedef struct HNode {
   HKeyType  data;
   struct HNode*  next;
}*HLink;

typedef struct {
   HLink  *rcd;   // 指针存储基址，动态分配数组
   int    count;  // 当前表中含有的记录个数
   int    size;  // 哈希表的当前容量
}ChainHashTab;    // 链地址哈希表
int Hash(ChainHashTab H, HKeyType k) { // 哈希函数
  return k % H.size;
}
Status Collision(ChainHashTab H, HLink &p) {
  // 求得下一个探查地址p 
  if (p && p->next) { 
    p = p->next;
    return SUCCESS;
  } else return UNSUCCESS;
}
实现下列函数：
int BuildHashTab(ChainHashTab &H, int n, HKeyType es[]);
/* 直接调用下列函数                             */
/* 哈希函数：                                   */
/*    int Hash(ChainHashTab H, HKeyType k);     */
/* 冲突处理函数：                               */
/*    int Collision(ChainHashTab H, HLink &p);  */

```c
#include "allinclude.h"  //DO NOT edit this line
int BuildHashTab(ChainHashTab &H, int n, HKeyType es[]) 
/* 直接调用下列函数                             */
/* 哈希函数：                                   */
/*    int Hash(ChainHashTab H, HKeyType k);     */
/* 冲突处理函数：                               */
/*    int Collision(ChainHashTab H, HLink &p);  */
{
    int i , j , k;
    HLink p , q , t;
    j = 0;
    H.size = NUM;
    H.count = 0;
    H.rcd = (HLink *)malloc(H.size*sizeof(HLink));
    if(H.rcd == NULL) return UNSUCCESS;
    for (i = 0 ; i < H.size ; i++) {
      /* code */
      H.rcd[i] = NULL;
    }
    for (i = 0; i < n; i++) {
      /* code */
      p = (HLink)malloc(sizeof(HNode));
      p->data = es[i];
      k = Hash(H , p->data);
      t = H.rcd[k];
      while(t != NULL){
        if(t->data == p->data){
          j = 1;
          break;
        }
        t = t->next;
      }
      if(j == 0){
        q = H.rcd[k];
        p->next = q;
        H.rcd[k] = p;
        H.count++;
      }else{
        H.count++;
        j = 0;
      }
    }
    return SUCCESS;
}
```
## 第五章
### DC05PE04 根据给定的递归函数编写递归算法
试编写如下定义的递归函数的递归算法:
    g(m,n) = 0             当m=0,n>=0
    g(m,n) = g(m-1,2n)+n   当m>0,n>=0
实现下列函数：
int G(int m, int n); 
/* 如果 m<0 或 n<0 则返回 -1 */

```c
#include "allinclude.h"  //DO NOT edit this line
int G(int m, int n) {
  int temp = 0;
  if(m<0||n<0) 
    return -1;
  else if(m==0&&n>=0) 
    return 0;
  else 
    {
      temp =G(m-1,2*n);
      return temp+n;
    }
}
```
### DC05PE05 根据给定的递归函数F(n)编写递归算法
试写出求递归函数F(n)的递归算法：
    F(n) = n+1      当n=0
    F(n) = nF(n/2)  当n>0
实现下列函数：
int F(int n);
/* 如果 n<0 则返回 -1 */

```c
#include "allinclude.h"  //DO NOT edit this line
int F(int n) {
  int temp = 0;
  if(n < 0){
    return -1;
  }else if(n == 0) {
    temp = n + 1;
  }else{
   temp = n * F(n / 2); 
  }
  return temp;
}
```
### DC05PE06 利用递归算法求解平方根
求解平方根 的迭代函数定义如下：
  sqrt(A,p,e) = p                   当|p*p-A|<e
  sqrt(A,p,e) = sqrt(A,(p+A/p)/2,e) 当|p*p-A|>=e
其中，p是A的近似平方根，e是结果允许误差。试写出相
应的递归算法。
实现下列函数：
float Sqrt(float A, float p, float e);

```c
#include "allinclude.h"  //DO NOT edit this line
float Sqrt(float A, float p, float e) {
    float temp = 0;
    if(pow(p*p-A , 2)<pow(e , 2)){
      temp = p;
    }else{
      temp = Sqrt(A,(p+A/p)/2,e);
    }
    return temp;
}
```
### DC05PE07 请写出Ackerman函数的递归算法
已知Ackerman函数的定义如下：
   akm(m,n) = n+1                 当m=0
   akm(m,n) = akm(m-1,1)          当m!=0,n=0
   akm(m,n) = akm(m-1,akm(m,n-1)) 当m!=0,n!=0
请写出递归算法。
实现下列函数：
int Akm(int m, int n);
/* 若 m<0 或 n<0 则返回-1  */
```c
#include "allinclude.h"  //DO NOT edit this line
int Akm(int m, int n) {
  int temp = 0;
  if(m < 0 || n < 0){
    return -1;
  }
  else if(m == 0){
    temp = n + 1;    
  }else if(m != 0 && n == 0){
    temp = Akm(m - 1 , 1); 
  }else if(m != 0 || n != 0){
    temp = Akm(m - 1 , Akm(m , n - 1));
  }
  return temp;
}
```
### DC05PE15 试写出求递归函数F(n)的非递归算法
试写出求递归函数F(n)的非递归算法：
    F(n) = n+1      当n=0
    F(n) = nF(n/2)  当n>0
实现下列函数：
int F(int n);

```c
#include "allinclude.h"  //DO NOT edit this line

int F(int n) {
  int temp = 0;
  if(n < 0){
    return -1;
  }else if(n == 0){
    temp = n + 1;
  }else{
    temp = n * F(n / 2);
  }
  return temp;
}
```
### DC05PE16 试写出求解平方根的非递归算法
求解平方根 的迭代函数定义如下：
  sqrt(A,p,e) = p                   当|p*p-A|<e
  sqrt(A,p,e) = sqrt(A,(p+A/p)/2,e) 当|p*p-A|>=e
其中，p是A的近似平方根，e是结果允许误差。试写出相应的非递归算法。
实现下列函数：
float Sqrt(float A, float p, float e);
```c
#include "allinclude.h"  //DO NOT edit this line

float Sqrt(float A, float p, float e) {
    double temp = 0;
    if(pow(p * p - A , 2) < pow(e , 2)){
      temp = p;
    }else{
      temp = Sqrt(A , (p + A/p) / 2 ,e);
    }
    return temp;
}
```
### DC05PE20 将给定点元素同色区域的颜色进行置换
假设以二维数组g[1..m][1..n]表示一个图像
区域，g[i][j]表示该区域中点(i,j)所具颜色，其值
为从0到k的整数。试编写递归算法，将点(i0,j0)所在
区域的颜色置换为颜色c。约定与(i0,j0)同色的上、
下、左、右的邻接点为同色区域的点。
表示图像区域的类型定义如下：
typedef char GTYPE[m+1][n+1];
实现下列函数：
void ChangeColor(GTYPE g, int m, int n, 
                 char c, int i0, int j0);
/* 在g[1..m][1..n]中，将元素g[i0][j0] */
/* 所在的同色区域的颜色置换为颜色c    */

```c
#include "allinclude.h"  //DO NOT edit this line
void ChangeColor(GTYPE g, int m, int n, 
                 char c, int i0, int j0) {
  char t = g[i0][j0];
  g[i0][j0] = c;
  if(i0-1 >= 1 && g[i0-1][j0] == t)
    ChangeColor(g,m,n,c,i0-1,j0);
  if(j0-1 >= 1 && g[i0][j0-1] == t)
    ChangeColor(g,m,n,c,i0,j0-1);
  if(i0+1 <= m && g[i0+1][j0] == t)
    ChangeColor(g,m,n,c,i0+1,j0);
  if(j0+1 <= n && g[i0][j0+1] == t)
    ChangeColor(g,m,n,c,i0,j0+1);
}
```
### DC05PE30 求广义表的深度
试按依次对每个元素递归分解的分析方法重写求广义表的深度的递归算法。

广义表类型GList的定义：
typedef enum {ATOM,LIST} ElemTag;
typedef struct GLNode{
     ElemTag tag;
     union {
       char atom;
       struct { 
         GLNode *hp, *tp;
       } ptr;
     }un;
} *GList;
要求实现以下函数：
int GListDepth(GList ls);
/* Return the depth of list */

```c
#include "allinclude.h"  //DO NOT edit this line
int GListDepth(GList ls) {
 int max,dep;
 GList pp;
 if(NULL == ls) return 1;
 if(ATOM == ls->tag) return 0;
  for(max = 0,pp = ls;pp;pp = pp->un.ptr.tp){
    dep = GListDepth(pp->un.ptr.hp)+1;
    if(dep > max)
     max = dep;
  }
  return max;
}
```
### DC05PE32 判别两个广义表是否相等
试编写判别两个广义表是否相等的递归算法。

广义表类型GList的定义：
typedef enum {ATOM,LIST} ElemTag;
typedef struct GLNode{
     ElemTag tag;
     union {
       char atom;
       struct { 
         GLNode *hp, *tp;
       } ptr;
     }un;
} *GList;
要求实现以下函数：
Status Equal(GList A, GList B);
/* 判断广义表A和B是否相等,是则返回TRUE,否则返回FALSE */

```c
#include "allinclude.h"  //DO NOT edit this line

Status Equal(GList A, GList B) {
  if(A == NULL && B == NULL) 
    return TRUE;
  else if(A == NULL || B == NULL || A->tag != B->tag) 
    return FALSE;
  else if(A->tag == ATOM && A->un.atom == B->un.atom) 
    return TRUE;
  if(Equal(A->un.ptr.hp , B->un.ptr.hp) && Equal(A->un.ptr.tp , B->un.ptr.tp))
    return TRUE;
   else return FALSE; 
}
```
### DC05PE33 输出广义表中所有原子项及其所在的层次
试编写递归算法，输出广义表中所有原子项
及其所在层次。
广义表类型GList的定义：
typedef enum {ATOM,LIST} ElemTag;
typedef struct GLNode{
    ElemTag tag;
    union {
       char atom;
       struct { 
          GLNode *hp, *tp;
       } ptr;
    }un;
} *GList;
要求实现以下函数：
void OutAtom(GList A, int layer, void(*Out2)(char, int));
/* 递归地用函数Out2输出广义表的原子及其所在层次,layer表示当前层次 */

```c
#include "allinclude.h"  //DO NOT edit this line
void OutAtom(GList A, int layer, void(*Out2)(char, int)) {
  GList p;
  p = A;
  if(NULL == A) return ;
  if(ATOM == p->tag){
    Out2(A->un.atom,layer);
    return;
  }
  // 表头不包括层次 表尾必定是一个广义表包括了层次
  OutAtom(p->un.ptr.hp,layer+1,Out2);
  OutAtom(p->un.ptr.tp,layer,Out2);
}
```

## 第六章
### DC06PE06 判别两棵二叉树是否相似
若两棵二叉树T1和T2皆为空，或者皆不空且T1的左、右子树和T2的左、右子树分别相似，则称二叉树T1和T2相似。试编写算法，判别给定的两棵二叉树是否相似。
二叉链表类型定义：
typedef struct BiTNode {
  TElemType  data;
  struct BiTNode  *lchild, *rchild;
} BiTNode, *BiTree;
要求实现下列函数：
// 如果T1和T2相似，则返回TRUE；否则返回FALSE
Status Similar(BiTree T1, BiTree T2);
```c
#include "allinclude.h"  //DO NOT edit this line
Status Similar(BiTree T1, BiTree T2){ 
    // Add your code here
    if(NULL == T1 && NULL == T2) return TRUE;
    if(NULL != T1 && NULL != T2){
      return Similar(T1->lchild , T2->lchild) && Similar(T1->rchild , T2->rchild);
    }
    return FALSE;
}
```

### DC06PE11 编写递归算法，求对二叉树T先序遍历时第k个访问的结点的值
编写递归算法，求对二叉树T先序遍历时第k个访问的结点的值。
二叉链表类型定义：
typedef struct BiTNode {
  TElemType data;
  struct BiTNode  *lchild, *rchild;
} BiTNode, *BiTree;
要求实现下列函数：
TElemType PreOrderK(BiTree T, int k);
/* 求对二叉树T先序遍历时第k个访问的结点的值。*/
/* 若失败，则返回'#'                         */
```c
#include "allinclude.h"  //DO NOT edit this line
TElemType PreOrderK(BiTree T, int k){ 
    // Add your code here
    TElemType PreOrder(BiTree T, int &k1);
    return PreOrder(T,k);
} 
TElemType PreOrder(BiTree T, int &k1){
  TElemType p = '#';
  if(T == NULL) return '#';
  if(k1 == 1) return T->data;
  k1--;
  if(T->lchild)
    p = PreOrder(T->lchild, k1);
  if(T->rchild && p == '#')
    p = PreOrder(T->rchild, k1);
  return p;
}
```
### DC06PE12 编写递归算法，计算二叉树T中叶子结点的数目
编写递归算法，计算二叉树T中叶子结点的数目。
二叉链表类型定义：
typedef struct BiTNode {
  TElemType  data;
  struct BiTNode  *lchild, *rchild;
} BiTNode, *BiTree;
要求实现下列函数：
int Leaves(BiTree T);
/* 计算二叉树T中叶子结点的数目 */

```c
#include "allinclude.h"  //DO NOT edit this line
int Leaves(BiTree T){ 
    // Add your code here
    if(NULL == T){
      return 0;
    }else{
      if(T->lchild == NULL && T->rchild == NULL){
        return 1;
      }else{
      return Leaves(T->lchild) + Leaves(T->rchild);
    }
 } 
}
```
### DC06PE21 试利用栈及其基本操作写出二叉树T的非递归的先序遍历算法
试利用栈及其基本操作写出二叉树T的非递归的先序遍历算法。
二叉链表类型定义：
typedef struct BiTNode {
  TElemType  data;
  struct BiTNode  *lchild,*rchild;
} BiTNode, *BiTree;
可用栈类型Stack的相关定义：
typedef BiTree SElemType;   // 栈的元素类型
Status InitStack(Stack &S); 
Status StackEmpty(Stack S); 
Status Push(Stack &S, SElemType e);
Status Pop(Stack &S, SElemType &e); 
Status GetTop(Stack S, SElemType &e); 
要求实现下列函数：
void PreOrder(BiTree T, void (*visit)(TElemType)); 
/* 使用栈，非递归先序遍历二叉树T，     */
/* 对每个结点的元素域data调用函数visit */
```c
#include "allinclude.h"  //DO NOT edit this line
void PreOrder(BiTree T, Status (*visit)(TElemType)){ 
    // Add your code here
    Stack S; 
    InitStack(S);
    BiTree p = T;
    while(p != NULL || !StackEmpty(S)){
      if(p != NULL){
          visit(p->data);
          Push(S , p);
          p = p->lchild;
      }
      else{
        Pop(S , p);
        p = p->rchild;
      }
    }
}
```

### DC06PE23 试利用栈及其基本操作写出二叉树T的非递归的后序遍历算法
试利用栈及其基本操作写出二叉树T的非递归的后序遍历算法(提示：为分辨后序遍历时两次进栈的不同返回点，需在指针进栈时同时将一个标志进栈）。
二叉链表类型定义：
typedef struct BiTNode {
  TElemType  data;
  struct BiTNode  *lchild,*rchild;
} BiTNode, *BiTree;
可用栈类型Stack的相关定义：
typedef struct {
  struct BiTNode *ptr; // 二叉树结点的指针类型
  int      tag; // 0..1
} SElemType;    // 栈的元素类型
Status InitStack(Stack &S); 
Status StackEmpty(Stack S); 
Status Push(Stack &S, SElemType e);
Status Pop(Stack &S, SElemType &e); 
Status GetTop(Stack S, SElemType &e); 
要求实现下列函数：
void PostOrder(BiTree T, void (*visit)(TElemType));
/* 使用栈，非递归后序遍历二叉树T，     */
/* 对每个结点的元素域data调用函数visit */

```c
#include "allinclude.h"  //DO NOT edit this line
void PostOrder(BiTree T, Status (*visit)(TElemType))
/* 使用栈，非递归后序遍历二叉树T，     */
/* 对每个结点的元素域data调用函数visit */
{
  Status right;
  Stack S;
  InitStack(S);
  SElemType w;
  w.ptr=T;
  w.tag=0;
  BiTree p;
  do {
    while (w.ptr!=NULL) { 
      Push(S,w);
      w.ptr=w.ptr->lchild; 
    }
    right=TRUE;
    while (!StackEmpty(S) && right) {
      Pop(S,w);
      if (w.tag==1) {
        visit(w.ptr->data);
      } else {
        w.tag=1; 
        Push(S,w);  
        w.ptr=w.ptr->rchild;  
        w.tag=0;
        right=FALSE;
      }
    }
  } while (!StackEmpty(S));
}
```

### DC06PE27 二叉树采用三叉链表的存储结构，试编写不借助栈的非递归中序遍历算法
二叉树采用三叉链表的存储结构，试编写不借助栈的非递归中序遍历算法。

三叉链表类型定义：
typedef struct TriTNode {
  TElemType data;
  struct TriTNode  *parent, *lchild, *rchild;
} TriTNode, *TriTree;

要求实现以下函数：
void InOrder(TriTree PT, void (*visit)(TElemType));
/* 不使用栈，非递归中序遍历二叉树PT，  */
/* 对每个结点的元素域data调用函数visit */

```c
#include "allinclude.h"  //DO NOT edit this line
void InOrder(TriTree PT, Status (*visit)(TElemType)){ 
    // Add your code here
    TriTree p = PT , pr;
      while(p != NULL){
        if(p->lchild != NULL) p = p->lchild;
        else{
          visit(p->data);
          if(p->rchild != NULL){
            p = p->rchild;
          } 
          else{
           pr = p;
           p = p->parent;
           while(p != NULL && (p->rchild == NULL || p->rchild == pr)){
            if(p->lchild == pr)
            visit(p->data);
            pr = p;
            p = p->parent;
          }
          if(p != NULL){
            visit(p->data);
          p = p->rchild;
          }
        }
      }
    }
}
```

### DC06PE29 编写不用栈辅助的二叉树非递归后序遍历算法
假设在三叉链表的结点中增设一个标志域(mark取值0,1或2)以区分在遍历过程中到达该结点时应继续向左或向右或访问该结点。试以此存储结构编写不用栈辅助的二叉树非递归后序遍历算法。
带标志域的三叉链表类型定义：
typedef struct TriTNode {
  TElemType  data;
  struct TriTNode  *lchild, *rchild, *parent;
  int       mark;  // 标志域
} TriTNode, *TriTree;

要求实现以下函数：
void PostOrder(TriTree T, Status (*visit)(TElemType));
/* 不使用栈，非递归后序遍历二叉树T，   */
/* 对每个结点的元素域data调用函数visit */

```c
#include "allinclude.h"  //DO NOT edit this line
void PostOrder(TriTree T, Status (*visit)(TElemType)){ 
    // Add your code here
    TriTree p = T;
    // visit(p->data);
     while(p){
        while(p->mark==0){  //先遍历左孩子
            p->mark=1;
            if(p->lchild)
                p=p->lchild;
        }
        while(p->mark==1){  //再遍历右孩子
            p->mark=2;
            if(p->rchild)
            p=p->rchild;
        }
        if(p->mark==2){ 
            visit(p->data);
            p=p->parent;
        }
    }
} 
```

### DC06PE33 编写递归算法，将二叉树中所有结点的左、右子树相互交换
编写递归算法，将二叉树中所有结点的左、右子树相互交换。

二叉链表类型定义：
typedef struct BiTNode {
  TElemType data;
  struct BiTNode  *lchild, *rchild;
} BiTNode, *BiTree;

要求实现下列函数：
void ExchangeSubTree(BiTree &T);
/* 将二叉树中所有结点的左、右子树相互交换 */

```c
#include "allinclude.h"  //DO NOT edit this line
void ExchangeSubTree(BiTree &T){ 
    // Add your code here
    BiTree temp;
    if(T){
      temp = T->lchild;
      T->lchild = T->rchild;
      T->rchild = temp;
      ExchangeSubTree(T->lchild);
      ExchangeSubTree(T->rchild);
    }
}
```

### DC06PE37 编写递归算法：求二叉树中以元素值为x的结点为根的子树的深度
编写递归算法：求二叉树中以元素值为x的结点为根的子树的深度。

二叉链表类型定义：
typedef struct BiTNode {
  TElemType data;
  struct BiTNode  *lchild, *rchild;
} BiTNode, *BiTree;

要求实现下列函数：
int Depthx(BiTree T, TElemType x);
/* 求二叉树中以值为x的结点为根的子树深度 */

```c
#include "allinclude.h"  //DO NOT edit this line
int Depthx(BiTree T, TElemType x){
    // Add your code here
    if(NULL==T) return 0;
    int leftdepth,rightdepth;
    if(T->data==x){
       if(T->lchild) leftdepth=Depthx(T->lchild,T->lchild->data);
       else leftdepth=Depthx(T->lchild,x);
       if(T->rchild) rightdepth=Depthx(T->rchild,T->rchild->data);
       else rightdepth=Depthx(T->rchild,x);
        return 1+(leftdepth>rightdepth?leftdepth:rightdepth);
    }else{
      leftdepth=Depthx(T->lchild,x);
      rightdepth=Depthx(T->rchild,x);
      return leftdepth>rightdepth?leftdepth:rightdepth;
    }
}
```

### DC06PE40 编写递归算法：对于二叉树中每一个元素值为x的结点，删去以它为根的子树，并释放相应的空间
编写递归算法：对于二叉树中每一个元素值为x的结点，删去以它为根的子树，并释放相应的空间。

二叉链表类型定义：
typedef struct BiTNode {
  TElemType data;
  struct BiTNode  *lchild, *rchild;
} BiTNode, *BiTree;

要求实现下列函数：
void ReleaseX(BiTree &T, char x);
/* 对于二叉树中每一个元素值为x的结点，  */
/* 删去以它为根的子树，并释放相应的空间 */

```c
#include "allinclude.h"  //DO NOT edit this line
void ReleaseX(BiTree &T, char x)
{
    void Destroy(BiTree &T);
    if(T){
      if(T->data == x){
        Destroy(T);
      }else{
        ReleaseX(T->lchild , x);
        ReleaseX(T->rchild , x);
      }
    }
}

void Destroy(BiTree &T){
  if(!T) return;
  else{
    Destroy(T->lchild);
    Destroy(T->rchild);
    free(T);
    T = NULL;
  }
}
```

### DC06PE43 编写复制一棵二叉树的递归算法
编写复制一棵二叉树的递归算法。
二叉链表类型定义：
typedef char TElemType;   // 设二叉树的元素为char类型
typedef struct BiTNode {
  TElemType data;
  struct BiTNode  *lchild, *rchild;
} BiTNode, *BiTree;
要求实现下列函数：
void CopyBiTree(BiTree T, BiTree &TT);
/* 递归复制二叉树T得到TT */

```c
#include "allinclude.h"  //DO NOT edit this line
void CopyBiTree(BiTree T, BiTree &TT){ 
    // Add your code here
    if(NULL == T){
      TT = NULL;
      return;
    }else{
      TT = (BiTree)malloc(sizeof(BiTree));
      TT->data = T->data;
      CopyBiTree(T->lchild , TT->lchild);
      CopyBiTree(T->rchild , TT->rchild);
    }
} 
```

### DC06PE47 编写算法判别给定二叉树是否为完全二叉树
编写算法判别给定二叉树是否为完全二叉树。

二叉链表类型定义：
typedef struct BiTNode {
  TElemType data;
  struct BiTNode  *lchild, *rchild;
} BiTNode, *BiTree;

可用队列类型Queue的相关定义：
typedef BiTree QElemType; // 设队列元素为二叉树的指针类型
Status InitQueue(Queue &Q);
Status EnQueue(Queue &Q, QElemType e);
Status DeQueue(Queue &Q, QElemType &e);
Status GetHead(Queue Q, QElemType &e);
Status QueueEmpty(Queue Q);

要求实现下列函数：
Status CompleteBiTree(BiTree T);
/* 判别二叉树T是否为完全二叉树 */

```c
#include "allinclude.h"  //DO NOT edit this line
Status CompleteBiTree(BiTree T){ 
    // Add your code here
    if(T==NULL)
        return TRUE;
    int F = 0;
    BiTree p =  T;
    Queue Q;
    InitQueue(Q);
    EnQueue(Q,p);
    while(DeQueue(Q,p)){
        if(p==NULL)
            F=1;
        else if(F)
            return false;
        else{
            EnQueue(Q,p->lchild);
            EnQueue(Q,p->rchild);            
        }
    }   
    return true;
}
```

### DC06PE50 试编写一个二叉排序树的判定算法
试编写一个二叉排序树的判定算法。

二叉排序树的类型BSTree定义如下：
typedef struct {
  KeyType key;  
  ... ...   // 其他数据域
} TElemType;

typedef struct BiTNode {
  TElemType data;
  struct BSTNode  *lchild, *rchild;
}BSTNode, *BSTree;

实现下列函数：
Status IsBSTree(BSTree T);
/* 判别二叉树T是否为二叉排序树。*/
/* 若是，则返回TRUE，否则FALSE  */

```c
#include "allinclude.h"  //DO NOT edit this line
Status BST(BSTree T,BSTree &pre){
  if(!T) return TRUE;
  if( FALSE == BST(T->lchild,pre)) return FALSE;
  if(pre != NULL && pre->data.key >T->data.key) return FALSE;
  pre=T;
  return BST(T->rchild,pre);
}
Status IsBSTree(BSTree T){ 
    // Add your code here
    BSTree p=NULL;
    return BST(T,p);
    
}
```

### DC06PE53 编写递归算法，从大到小输出给定二叉排序树中所有关键字不小于x的数据元素
编写递归算法，从大到小输出给定二叉排序树中所有关键字不小于x的数据元素。

二叉排序树的类型BSTree定义如下：
typedef struct {
    KeyType key;  
    ... ...   // 其他数据域
} TElemType;

typedef struct BSTNode {
  TElemType  data;
  struct BSTNode  *lchild,*rchild;
}BSTNode, *BSTree;

实现下列函数：
void OrderOut(BSTree T, KeyType k, void(*visit)(TElemType));
/* 调用visit(T->data)输出  */

```c
#include "allinclude.h"  //DO NOT edit this line
void OrderOut(BSTree T, KeyType k, void(*visit)(TElemType)){ 
    // Add your code here
    if(!T)
        return ;
    OrderOut(T->rchild,k,visit);
    if(T->data.key>=k){
        visit(T->data);
        OrderOut(T->lchild,k,visit);
    }
} 
```

### DC06PE60 试写一非递归算法，在二叉查找树T中插入元素e
二叉查找树的类型BSTree定义如下：
typedef struct {
  KeyType key;  
    ... ...   // 其他数据域
} TElemType;

typedef struct BSTNode {
  TElemType data;
  struct BSTNode  *lchild,*rchild;
} BSTNode, *BSTree;
实现下列函数：
Status InsertBST_I(BSTree &T, TElemType k);
/* 在二叉查找树T中插入元素e的非递归算法 */

```c
#include "allinclude.h"  //DO NOT edit this line
Status InsertBST_I(BSTree &T, TElemType k)
{  
    BSTree s,p = T;
    s = (BSTree)malloc(sizeof(BSTNode));
    if(!s)  return OVERFLOW;
    s->data = k;    s->lchild = NULL;   s->rchild = NULL;
    while(T){
        if(p->data.key==k.key)
            return OVERFLOW;
        if(p->data.key>k.key){
            if(p->lchild)
                p = p->lchild;
            else
                p->lchild = s;
        }        
        if(p->data.key<k.key){
            if(p->rchild)
                p = p->rchild;
            else
                p->rchild = s;
        }     
    }    
}
```

### DC06PE68 试编写算法，求二叉树T中结点a和b的最近共同祖先
二叉链表类型定义：
typedef struct BiTNode {
  TElemType data;
  struct BiTNode  *lchild,*rchild;
} BiTNode, *BiTree;

可用栈类型Stack的相关定义：
typedef struct {
  BiTNode *ptr; // 二叉树结点的指针类型
  int      tag; // 0..1
} SElemType;      // 栈的元素类型

Status InitStack(Stack &S); 
Status StackEmpty(Stack S); 
int StackLength(SqStack S);
Status Push(Stack &S, SElemType e);
Status Pop(Stack &S, SElemType &e); 
Status GetTop(Stack S, SElemType &e); 

要求实现下列函数：
BiTree CommAncestor(BiTree T, TElemType a, TElemType b);
/* 求二叉树T中结点a和b的最近共同祖先 */

```c
#include "allinclude.h"  //DO NOT edit this line
Status getPathStack(Stack &s,BiTree t,TElemType v)
{
    if(t == NULL) return ERROR;
    SElemType e;
    e.ptr = t;
    if (t->data == v) {
        Push(s,e);
        return OK;
    }
    if (OK == getPathStack(s,t->lchild,v)) {
        Push(s,e);
        return OK;
    }
    if (OK == getPathStack(s,t->rchild,v)) {
        Push(s,e);
        return OK;
    }
    Pop(s,e);
    return ERROR;
}    
 
BiTree CommAncestor(BiTree T, TElemType a, TElemType b)

{
    if (T == NULL) return NULL;
    Stack sa,sb;    
    InitStack(sa);
    InitStack(sb);
    if (ERROR == getPathStack(sa,T,a)) return NULL;
    if (ERROR == getPathStack(sb,T,b)) return NULL;
    SElemType E1,E2,e1,e2;
    Pop(sa,E1);
    Pop(sb,E2);
    while (!StackEmpty(sa) && !StackEmpty(sb)) {
        e1 = E1;
        e2 = E2; 
        if (ERROR == Pop(sa,E1) || ERROR == Pop(sb,E2) || E1.ptr->data != E2.ptr->data || E1.ptr->data == a || E2.ptr->data == b)
            return e1.ptr;
    }
    return NULL;
}
```


### DC06PE75 在二叉排序树的每个结点中增设一个lsize域，其值为该结点的左子树中的结点数加1。试编写时间复杂度为O(logn)的算法，求树中第k小的结点的位置

二叉排序树的类型BSTree定义如下：
typedef char KeyType;

typedef struct BSTNode {
  KeyType key;
  struct BSTNode  *lchild,*rchild;
  int lsize; // 新增域，值为左子树的结点数+1
} BSTNode, *BSTree;

实现下列函数：
BSTNode *Ranking(BSTree T, int k);
/* 在含lsize域的二叉排序树T中，*/
/* 求指向T中第k小的结点的指针  */

```c
#include "allinclude.h"  //DO NOT edit this line
BSTNode *Ranking(BSTree T, int k){ 
    // Add your code here
    if(!T)
        return NULL;
    if(T->lsize == k)
        return T;
    else if(T->lsize > k)
        return Ranking(T->lchild,k);
    else
        return Ranking(T->rchild,k-T->lsize); 
} 
```


### DC06PE77  假设二叉排序树T的每个结点的平衡因子域bf当前均为0。试编写算法，求二叉排序树T的深度，并为每个结点的bf域赋予正确的平衡因子值

平衡二叉排序树的类型BBSTree定义如下：
typedef char KeyType;
typedef struct BBSTNode {
  KeyType key;
  int bf;    // 平衡因子
  struct BBSTNode  *lchild,*rchild;
} BBSTNode, *BBSTree;

实现下列函数：
int Depth_BF(BBSTree T);
/* 求二叉排序树T的深度，并为每个结点 */
/* 的bf域赋予正确的平衡因子值。      */

```c
#include "allinclude.h"  //DO NOT edit this line
int Depth_BF(BBSTree T){ 
    // Add your code here
    int lf,rf;
    if(!T)
        return 0;
    lf = Depth_BF(T->lchild);
    rf = Depth_BF(T->rchild);
    T->bf = lf-rf;
    return 1 + (lf > rf ? lf : rf);
} 
```

### DC06PE82 编写平衡二叉排序树的右平衡处理算法

平衡二叉排序树的类型BBSTree定义如下：
typedef char KeyType;  
typedef struct BBSTNode {
  KeyType key;
  int  bf;    // 平衡因子
  struct BBSTNode  *lchild,*rchild;
} BBSTNode, *BBSTree;

可调用下列旋转调整操作：
void L_Rotate(BBSTree &p); // 对最小失衡子树p做左旋调整
void R_Rotate(BBSTree &p); // 对最小失衡子树p做右旋调整

实现下列函数：
void RightBalance(BBSTree &T);
/* 实现对二叉树T的右平衡处理 */

```c
#include "allinclude.h"  //DO NOT edit this line
#define LH +1
#define EH 0
#define RH -1
void RightBalance(BBSTree &T){ 
    // Add your code here
    BBSTree lc,rd;
    lc = T->rchild;
    switch(lc->bf){
      case RH:
        T->bf = lc->bf = EH; 
        L_Rotate(T);
        break;
      case LH:
        rd = lc->lchild;
        switch(rd->bf){
          case RH:T->bf = RH;lc->bf = EH;break;
          case EH:T->bf = lc->bf = EH;break;
          case LH:T->bf = EH;lc->bf = LH;break;
        }
        rd->bf = EH;
        R_Rotate(T->rchild);
        L_Rotate(T);
        break;
    }
}
```


## 第七章

### DC07PE15  试编写算法，对一棵以孩子兄弟链表表示的树统计叶子的个数

孩子兄弟链表类型定义：
typedef struct CSTNode {
  TElemType  data;
  struct CSTNode  *firstChild, *nextSibling;
} CSTNode, *CSTree;

要求实现下列函数：
int Leave(CSTree T); /* 统计树T的叶子数 */

```c
#include "allinclude.h"  //DO NOT edit this line
int Leave(CSTree T){ 
    // Add your code here
    void Count(CSTree T , int &n);
    int n = 0;
    Count(T,n);
    return n;
} 
void Count(CSTree T , int &n){
 if(T){
      if(!T->firstChild) n++;
      Count(T->firstChild, n);
      Count(T->nextSibling, n);
   }
}
```

### DC07PE17  试编写算法，求一棵以孩子兄弟链表表示的树的度

孩子兄弟链表类型定义：
typedef struct CSTNode {
  TElemType  data;
  struct CSTNode  *firstChild, *nextSibling;
} CSTNode, *CSTree;

要求实现下列函数：
int Degree(CSTree T); /* 求树T的度 */

```c
#include "allinclude.h"  //DO NOT edit this line
int Degree(CSTree T){ 
    // Add your code here
   int ds,dt,d;
   CSTree p;
   if(!T) return 0;
   else { ds=0;dt=0;
       for( p = T->firstChild; p ; p= p->nextSibling){
          dt++;
          d= Degree(p);
          if(d>ds) ds =d;
       }
       return ds>dt?ds:dt;
   }
}
```

### DC07PE22  试编写算法，对以双亲表示法存储的树计算深度

树的双亲表示法的类型定义如下：
typedef struct {
  TElemType data;
  int     parent;  // 双亲位置
} PTNode; // 结点类型
typedef struct {
  PTNode nodes[MAX_TREE_SIZE]; // 结点存储空间
  int  n, r; // 结点数和根的位置
} PTree;

要求实现以下函数：
int PTreeDepth(PTree T); /* 求树T的深度 */

```c
#include "allinclude.h"  //DO NOT edit this line
int PTreeDepth(PTree T){ 
    // Add your code here
    int maxdep = 0 , dep , i , j;
    for (i = 0 ; i < T.n ; i++) {
      /* code */
      dep = 0;
      for (j = i ; j > 0 ; j = T.nodes[j].parent) {
        /* code */dep++;
      }
      if(dep > maxdep) maxdep = dep;
    }
    return maxdep + 1;
} 
```

### DC07PE24  试编写算法，对以双亲孩子表示法存储的树计算深度

孩子链表类型定义：
typedef struct ChildNode {  // 孩子结点
  int childIndex;
  struct ChildNode *nextChild;
} ChildNode; // 孩子结点类型
typedef struct  {
  TElemType data;
  int     parent;  // 双亲位置
  struct ChildNode *firstChild; // 孩子链表头指针
} PCTreeNode; // 结点类型
typedef struct {
  PCTreeNode *nodes; // 结点存储空间
  int  n, r; // 结点数和根的位置
} PCTree;

要求实现下列函数：
int PCTreeDepth(PCTree T); /* 求树T的深度 */

```c
#include "allinclude.h"  //DO NOT edit this line
int PCTreeDepth(PCTree T){ 
    // Add your code here
    int depth;
    int count(PCTree T,int pos);
    depth = count(T,T.r);
    return depth;
}
int count(PCTree T, int pos){
  if(T.nodes[pos].firstChild == NULL)
    return 1;
  ChildNode *temp = T.nodes[pos].firstChild;
  int depth = 1,max =1;
  while(temp != NULL){
    if(T.nodes[temp->childIndex].firstChild != NULL){
      depth = count(T,temp->childIndex);
      if(depth > max)
        max = depth;
    }
    temp = temp->nextChild;
  }
  return max+1;
}
```

### DC07PE26  试编写算法，对以孩子-兄弟链表表示的树计算深度

孩子兄弟链表类型定义：
typedef struct CSTNode {
  TElemType  data;
  struct CSTNode  *firstChild, *nextSibling;
} CSTNode, *CSTree;

要求实现下列函数：
int TreeDepth(CSTree T);
/* 求树T的深度 */

```c
#include "allinclude.h"  //DO NOT edit this line
int TreeDepth(CSTree T){ 
    // Add your code here
    int dep1,dep2,dep;
    if(T == NULL){
      dep = 0;
    }
    else{
      dep1 = TreeDepth(T->firstChild);
      dep2 = TreeDepth(T->nextSibling);
      dep = dep1 + 1 > dep2 ? dep1 + 1 : dep2;
    }
      return dep;
}
```

### DC07PE63  试编写非递归算法，实现并查集带路径压缩的查找操作

并查集的类型定义如下：
typedef struct {
  int *parent;
  int  n;
} MFSet;

实现下列函数：
int find(MFSet S, int i);
/* 并查集带路径压缩的查找的非递归实现 */

```c
#include "allinclude.h"  //DO NOT edit this line
int find(MFSet S, int i){ 
    // Add your code here
    int k,temp,r;
    r = i;
    while(S.parent[r] >= 0)
      r = S.parent[r];
    k = i;
    while(k != r){
      temp = S.parent[k];
      S.parent[k] = r;
      k = temp;
    }
    return r;
}
```
## 第八章
### DC08PE12  编写算法，创建有向图的邻接数组存储结构
编写算法，创建有向图的邻接数组存储结构。
图的邻接数组存储结构的类型定义如下：
#define UNVISITED  0
#define VISITED    1  
#define MAX_VEX_NUM  4
#define INFINITY MAXINT // 计算机允许的整数最大值，即∞
typedef int VRType;
typedef char InfoType;
typedef char VexType;
typedef enum {DG,DN,UDG,UDN} GraphKind; // 有向图,有向网,无向图,无向网
typedef struct {
    VRType adj; // 顶点关系类型。对无权图，用1(是)或0(否)表示相邻否；
                // 对带权图，则为权值类型
    InfoType *info; // 该弧相关信息的指针(可无)
}ArcCell;//,AdjMatrix[MAX_VERTEX_NUM][MAX_VERTEX_NUM];
typedef struct {
  ArcCell arcs[MAX_VEX_NUM][MAX_VEX_NUM]; // 关系数组
  VexType vexs[MAX_VEX_NUM]; // 顶点数组
  int n, e;   // 顶点数和边（弧）数
  GraphKind kind; // 图的类型
} MGraph; // 邻接数组类型
typedef struct {
  VexType v, w;
  int inf;
} ArcInfo;

可调用以下基本操作：
Status InitGraph(MGraph &G, GraphKind kind, int n);
  // 初始化含n个顶点空间的kind类的空图G
int LocateVex(MGraph G, VexType v); // 查找顶点v在图G中的位序

要求实现以下函数：
Status CreateDG(MGraph &G, VexType *vexs, int n,
                           ArcInfo *arcs, int e);
/* 创建含n个顶点和e条边的有向图G，vexs为顶点信息，arcs为边信息 */

```c
#include "allinclude.h"  //DO NOT edit this line
Status CreateDG(MGraph &G, VexType *vexs, int n,
                           ArcInfo *arcs, int e){ 
    // Add your code here
    InitGraph(G,DG,n);
    int i,j,k;
    VexType v, w;
    G.e = e; G.n = n;
    for(int m = 0 ; m < n ; m++)
        G.vexs[m] = vexs[m];
    for(k = 0;k < G.e ; k++){
        v = arcs[k].v; 
        w = arcs[k].w;
        i = LocateVex(G,v);
        j = LocateVex(G,w);
        if(i<0||j<0) 
            return ERROR;
        G.arcs[i][j].adj = 1;
      }
    return OK;
}
```
### DC08PE15   编写算法，在图G中，相对于k顶点的当前邻接顶点m顶点，求下一个邻接顶点
编写算法，在图G中，相对于k顶点的当前邻接顶点m顶点，求下一个邻接顶点。

图的邻接数组存储结构的类型定义如下：
#define UNVISITED  0
#define VISITED    1  
#define MAX_VEX_NUM  4
#define INFINITY MAXINT // 计算机允许的整数最大值，即∞
typedef int VRType;
typedef char InfoType;
typedef char VexType;
typedef enum {DG,DN,UDG,UDN} GraphKind; // 有向图,有向网,无向图,无向网
typedef struct {
    VRType adj; // 顶点关系类型。对无权图，用1(是)或0(否)表示相邻否；
                // 对带权图，则为权值类型
    InfoType *info; // 该弧相关信息的指针(可无)
}ArcCell;//,AdjMatrix[MAX_VERTEX_NUM][MAX_VERTEX_NUM];
typedef struct {
  ArcCell arcs[MAX_VEX_NUM][MAX_VEX_NUM]; // 关系数组
  VexType vexs[MAX_VEX_NUM]; // 顶点数组
  int n, e;   // 顶点数和边（弧）数
  GraphKind kind; // 图的类型
} MGraph; // 邻接数组类型

要求实现以下函数：
int NextAdjVex(MGraph G, int k, int m);
/* 在图G中，相对于k顶点的当前邻接顶点m顶点，求下一个邻接顶点 */

```c
#include "allinclude.h"  //DO NOT edit this line
int NextAdjVex(MGraph G, int k, int m){ 
    // Add your code here
    int i = 0;
    if(G.n == 0 && k == 0 && m == 0) return 0;
    for (i = m + 1 ; i < G.n ; i++) {
      /* code */
      if(G.arcs[k][i].adj != 0)
        return i;
    }return -1;
}
```

### DC08PE17  编写算法，在图G中置顶点v到顶点w的弧或边
编写算法，在图G中置顶点v到顶点w的弧或边。

图的邻接数组存储结构的类型定义如下：
#define UNVISITED  0
#define VISITED    1  
#define MAX_VEX_NUM  4
#define INFINITY MAXINT // 计算机允许的整数最大值，即∞
typedef int VRType;
typedef char InfoType;
typedef char VexType;
typedef enum {DG,DN,UDG,UDN} GraphKind; // 有向图,有向网,无向图,无向网
typedef struct {
    VRType adj; // 顶点关系类型。对无权图，用1(是)或0(否)表示相邻否；
                // 对带权图，则为权值类型
    InfoType *info; // 该弧相关信息的指针(可无)
}ArcCell;//,AdjMatrix[MAX_VERTEX_NUM][MAX_VERTEX_NUM];
typedef struct {
  ArcCell arcs[MAX_VEX_NUM][MAX_VEX_NUM]; // 关系数组
  VexType vexs[MAX_VEX_NUM]; // 顶点数组
  int n, e;   // 顶点数和边（弧）数
  GraphKind kind; // 图的类型
} MGraph; // 邻接数组类型

可调用以下基本操作：
int LocateVex(MGraph G, VexType v); // 查找顶点v在图G中的位序

要求实现以下函数：
Status SetArc(MGraph &G, VexType v, VexType w, ArcCell info);
/* 在图G中置顶点v到顶点w的弧或边 */

```c
#include "allinclude.h"  //DO NOT edit this line
Status SetArc(MGraph &G, VexType v, VexType w, ArcCell info){ 
    // Add your code here
    int i , j , k;
    VRType *p;
    i = LocateVex(G , v);
    j = LocateVex(G , w);
    if(i < 0 || j < 0 || v == w) return ERROR;
    else if(G.arcs[i][j].adj != info.adj){
        G.e++;
        G.arcs[i][j] = info;
    } 
    return OK;
}
```

### DC08PE21  编写算法，计算以邻接表方式存储的有向图G中k顶点的出度
编写算法，计算以邻接表方式存储的有向图G中k顶点的出度。 
图的邻接表存储结构的类型定义如下：
#define UNVISITED  0
#define VISITED    1  
#define INFINITY MAXINT // 计算机允许的整数最大值，即∞
typedef char VexType;
typedef enum {DG,DN,UDG,UDN} GraphKind; // 有向图,有向网,无向图,无向网
typedef struct AdjVexNode {
  int adjvex;  // 邻接顶点在顶点数组中的位序
  struct AdjVexNode *next; // 指向下一个邻接顶点（下一条边或弧）
  int info;    // 存储边（弧）相关信息，对于非带权图可不用
} AdjVexNode, *AdjVexNodeP; // 邻接链表的结点类型
typedef struct VexNode {
  VexType data;    // 顶点值，VexType是顶点类型，由用户定义
  struct AdjVexNode *firstArc; // 邻接链表的头指针
} VexNode; // 顶点数组的元素类型
typedef struct {
  VexNode *vexs;  // 顶点数组，用于存储顶点信息
  int n, e;       // 顶点数和边（弧）数
  GraphKind kind; // 图的类型
  int *tags;      // 标志数组
} ALGraph;  // 邻接表类型

要求实现下列函数：
int outDegree(ALGraph G, int k); 
/* 求有向图G中k顶点的出度。若k顶点不存在，则返回-1 */

```c
#include "allinclude.h"  //DO NOT edit this line
int outDegree(ALGraph G, int k){ 
    // Add your code here
    int i , count = 0;
    AdjVexNodeP p;
    if(k < 0 || k >= G.n) return -1;
    if(G.vexs[k].firstArc != NULL)
      p = G.vexs[k].firstArc;
    for(; p != NULL ; p = p->next){
      count++;
    }
    return count;
}
```
### DC08PE22  编写算法，计算以邻接表方式存储的有向图G中k顶点的入度
编写算法，计算以邻接表方式存储的有向图G中k顶点的入度。 
图的邻接表存储结构的类型定义如下：
#define UNVISITED  0
#define VISITED    1  
#define INFINITY MAXINT // 计算机允许的整数最大值，即∞
typedef char VexType;
typedef enum {DG,DN,UDG,UDN} GraphKind; // 有向图,有向网,无向图,无向网
typedef struct AdjVexNode {
  int adjvex;  // 邻接顶点在顶点数组中的位序
  struct AdjVexNode *next; // 指向下一个邻接顶点（下一条边或弧）
  int info;    // 存储边（弧）相关信息，对于非带权图可不用
} AdjVexNode, *AdjVexNodeP; // 邻接链表的结点类型
typedef struct VexNode {
  VexType data;    // 顶点值，VexType是顶点类型，由用户定义
  struct AdjVexNode *firstArc; // 邻接链表的头指针
} VexNode; // 顶点数组的元素类型
typedef struct {
  VexNode *vexs;  // 顶点数组，用于存储顶点信息
  int n, e;       // 顶点数和边（弧）数
  GraphKind kind; // 图的类型
  int *tags;      // 标志数组
} ALGraph;  // 邻接表类型

要求实现下列函数：
int inDegree(ALGraph G, int k);
/* 求有向图G中k顶点的入度。若k顶点不存在，则返回-1 */

```c
#include "allinclude.h"  //DO NOT edit this line
int inDegree(ALGraph G, int k){ 
    // Add your code here
    int count = 0;
    AdjVexNode *p;
    if(G.e == 0 || G.n == 0 || k > G.n) return -1;
    for (int i = 0; i < G.n; i++) {
      /* code */
      p = G.vexs[i].firstArc;
      while(p){
        if(p->adjvex == k) count++;
        p = p->next;
      }
    }
    return count;
}
```

### DC08PE32  编写算法，创建有向图的邻接表存储结构
编写算法，创建有向图的邻接表存储结构。 
图的邻接表存储结构的类型定义如下：
#define UNVISITED  0
#define VISITED    1  
#define MAX_VEX_NUM  4
#define INFINITY MAXINT // 计算机允许的整数最大值，即∞
typedef char VexType;
typedef enum {DG,DN,UDG,UDN} GraphKind; // 有向图,有向网,无向图,无向网
typedef struct AdjVexNode {
  int adjvex;  // 邻接顶点在顶点数组中的位序
  struct AdjVexNode *next; // 指向下一个邻接顶点（下一条边或弧）
  int info;    // 存储边（弧）相关信息，对于非带权图可不用
} AdjVexNode, *AdjVexNodeP; // 邻接链表的结点类型
typedef struct VexNode {
  VexType data;    // 顶点值，VexType是顶点类型，由用户定义
  struct AdjVexNode *firstArc; // 邻接链表的头指针
} VexNode; // 顶点数组的元素类型
typedef struct {
  VexNode vexs[MAX_VEX_NUM];  // 顶点数组，用于存储顶点信息
  int n, e;       // 顶点数和边（弧）数
  GraphKind kind; // 图的类型
  int *tags;      // 标志数组
} ALGraph;  // 邻接表类型

可调用以下基本操作：
int LocateVex(ALGraph G, VexType v); // 查找顶点v在图G中的位序

要求实现下列函数：
Status CreateDG(ALGraph &G, VexType *vexs, int n,
                            ArcInfo *arcs, int e);
/* 创建含n个顶点和e条边的有向图G，vexs为顶点信息，arcs为边信息 */

```c
#include "allinclude.h"  //DO NOT edit this line
Status CreateDG(ALGraph &G, VexType *vexs, int n,
                            ArcInfo *arcs, int e){ 
    // Add your code here
    int i , j , k;
    VexType v , w;
    AdjVexNodeP p;
    G.n = n; G.e = e;
    // G.vexs = (VexNode *)malloc(n * sizeof(VexNode));
    G.tags = (int *)malloc(n * sizeof(int));
    for (i = 0 ; i < G.n ; i++) {
      /* code */
      G.tags[i] = UNVISITED;
      G.vexs[i].data = vexs[i];
      G.vexs[i].firstArc = NULL;
    }
    for (k = 0 ; k < G.e ; k++) {
      /* code */
      v = arcs[k].v;
      w = arcs[k].w;
      i = LocateVex(G , v);
      j = LocateVex(G , w);
      if(i < 0 ||j < 0) return ERROR;
      p = (AdjVexNode *)malloc(sizeof(AdjVexNode));
      if(NULL == p) return OVERFLOW;
      p->adjvex = j;
      p->next = G.vexs[i].firstArc;
      G.vexs[i].firstArc = p;
    }
    return OK;
}
```
### DC08PE34  编写算法，创建无向图的邻接表存储结构
编写算法，创建无向图的邻接表存储结构。
图的邻接表存储结构的类型定义如下：
#define UNVISITED  0
#define VISITED    1  
#define MAX_VEX_NUM  4
#define INFINITY MAXINT // 计算机允许的整数最大值，即∞
typedef char VexType;
typedef enum {DG,DN,UDG,UDN} GraphKind; // 有向图,有向网,无向图,无向网
typedef struct AdjVexNode {
  int adjvex;  // 邻接顶点在顶点数组中的位序
  struct AdjVexNode *next; // 指向下一个邻接顶点（下一条边或弧）
  int info;    // 存储边（弧）相关信息，对于非带权图可不用
} AdjVexNode, *AdjVexNodeP; // 邻接链表的结点类型
typedef struct VexNode {
  VexType data;    // 顶点值，VexType是顶点类型，由用户定义
  struct AdjVexNode *firstArc; // 邻接链表的头指针
} VexNode; // 顶点数组的元素类型
typedef struct {
  VexNode vexs[MAX_VEX_NUM]; //*vexs; 顶点数组，用于存储顶点信息
  int n, e;       // 顶点数和边（弧）数
  GraphKind kind; // 图的类型
  int *tags;      // 标志数组
} ALGraph;  // 邻接表类型

可调用以下基本操作：
int LocateVex(ALGraph G, VexType v); // 查找顶点v在图G中的位序

要求实现下列函数：
Status CreateUDG(ALGraph &G, VexType *vexs, int n,
                             ArcInfo *arcs, int e);
/* 创建含n个顶点和e条边的无向图G，vexs为顶点信息，arcs为边信息 */

```c
#include "allinclude.h"  //DO NOT edit this line
Status CreateUDG(ALGraph &G, VexType *vexs, int n,
                            ArcInfo *arcs, int e)
{
    int i,j,k;
    VexType v,w;
    AdjVexNodeP p,q;
    G.n = n;G.e = e;
    //G.vexs = (VexNode *)malloc(n*sizeof(VexNode)); 
    G.tags = (int*)malloc(n*sizeof(int));
    for(i = 0 ; i < G.n ; i++){
        G.tags[i] = UNVISITED;
        G.vexs[i].data = vexs[i];
        G.vexs[i].firstArc = NULL;
    }
    for(k = 0 ; k < G.e ; k++){
        v = arcs[k].v; 
        w = arcs[k].w;
        i = LocateVex(G,v);
        j = LocateVex(G,w);
        if(i < 0 || j < 0) return ERROR;
        p = (AdjVexNode *)malloc(sizeof(AdjVexNode));
        if(NULL == p) return OVERFLOW;
        p->adjvex = j;
        p->next = G.vexs[i].firstArc;
        G.vexs[i].firstArc = p; 
        q = (AdjVexNode*)malloc(sizeof(AdjVexNode));
        if(NULL == q) return OVERFLOW;
        q->adjvex = i;
        q->next = G.vexs[j].firstArc;
        G.vexs[j].firstArc = q;
    }
    return OK;
}
```

***大家都是来借鉴的吧（doge）***