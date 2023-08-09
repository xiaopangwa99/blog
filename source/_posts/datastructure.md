---
title: 数据结构整理
categories: data structure
date: 2023-08-09 10:00:00
desciption: 对数据结构知识点的整理
---
# 基本定义

## 数据

### 1.数据

能输入计算机且能被计算机处理的各种符号的集合

1）数值型数据：整数、实数等

2）非数值型数据：文字、图像、声音等

### 2.数据元素

数据的基本单位

也称为元素、记录或结点

例：  学号    姓名     专业      性别

​           123    张三     电子      男

### 3.数据项

构成数据元素的不可分割的最小单位

例：学号

### 三者关系

数据>数据元素>数据项

### 4.数据对象

性质相同的数据元素的集合，是数据的一个子集

## **数据结构

数据元素相互之间的关系称为结构

### 1.逻辑结构

#### 1.集合结构

#### 2.线性结构

#### 3.树形结构

#### 4.图形结构

### 2.物理结构或存储结构

数据元素及其关系在计算机内存中的表示

#### 1.顺序存储结构

#### 2.链式存储结构

****











## 算法

### 1.时间复杂度

==O(1) < O(log n) < O(n) < O(n*log n) < O(n²) < O(n³) < O(2<sup>n</sup>) < O(n!) < O(n<sup>n</sup>)==







# 线性表

零个或者多个数据元素的有限序列



线性表中，一个数据元素可以由若干个数据项组成

## 1.顺序存储结构

### 1.顺序存储定义

线性表的顺序存储结构，指的是用一段地址连续的存储单元依次存储线性表数据的元素。

### 2.顺序存储方式

```c
typedef struct{
	ElemType data[MAXSIZE];
	int length;
}Sqlist;
```

需要三个属性：  1.存储空间的起始位置 ： 数据data ,他的存储位置就是存储空间的存储位置

​							 2.线性表的最大存储容量：数组长度MAXSIZE

​							 3.线性表的当前长度：length

### 3.线性表顺序存储结构的优缺点

优点：无需为表中元素之间的逻辑关系而增加额外的存储空间

​			可以快速地存取表中的任一位置的元素



缺点：插入和删除操作需要移动大量元素

​		    当线性表长度变化较大时，难以确定存储空间的容量

​			造成存储空间的“碎片”



## 2.链式存储结构

### 1.定义

n个结点（a<sub>i</sub>的存储映像）链结成一个链表，即为线性表（a<sub>1</sub>,a<sub>2</sub>,a<sub>3</sub>,…,a<sub>n</sub>）的链式存储结构



**a<sub>i</sub>的存储映像**：1.数据域 

​						   2.指针域



**头指针**：链表中第一个结点的存储位置

~~最后一个结点指向空结点NULL~~



### 2.头指针、头结点的异同

**头指针**：1.头指针是指链表指向第一个结点的指针，若链表有头结点，则是指向头结点的指针

​				2.头指针具有标志作用，所以常用头指针冠以链表的名字

​				3.无论链表是否为空，头指针均不为空。头指针是链表的必要元素



**头结点**：1.头结点是为了操作的统一和方标而设立的，放在第一元素的结点之前，其数据域一般无意义（也可存放链表的长度）

​				2.有了头结点，对在第一元素结点之前插入结点和删除第一节点，其操作与其他结点的操作就统一了

​				3.头节点不一定就是链表的必需要素



### 3.链表存储方式

```c
/*线性表的单链表存储结构*/
typedef struct Node{
	ElemType data;
	struct Node *next;
}Node;
typedef struct Node *LinkList;
```



 对于插入或者删除数据越频繁的操作，单链表的效率优势就越明显 



### 4.单链表结构与顺序存储结构的优缺点

|              | 顺序存储方式                               | 单链表结构                                             |
| ------------ | ------------------------------------------ | ------------------------------------------------------ |
| 存储分配方式 | 用一段连续存储单元依次存储线性表的数据元素 | 采用链式存储结构，用一组任意的存储单元存放线性表的元素 |
| 时间性能     | 查找：O（1）                               | 查找：O（n）                                           |
|              | 插入和删除：O（n）                         | 插入和删除：O（1）                                     |
| 空间性能     | 需要预分配存储空间                         | 不需要分配存储空间                                     |

**线性表需要频繁查找，很少进行插入和删除操作时，宜采用顺序存储结构**

**线性表中的元素个数变化较大或者不知道有多大时，最好用单链表结构**



### 5.循环链表

### 6.双向链表

双向链表是在单链表的每个结点中，再设置一个指向其前驱节点的指针域

{% mermaid %}
graph TD
 A((线性表)) --- B1 & C1
 B1(顺序存储结构)
 C1(链式存储结构) --- D1(单链表) & D2(静态链表) & D3(循环链表) & D4(双向链表)
{% endmermaid %}












# 栈与队列

## 栈

#### 1.栈的定义

**栈(stack)是限定仅在表尾进行插入和删除操作的线性表**



允许插入和删除的一端称为栈顶(top)，另一端称为栈底(bottom)，不含任何数据元素的栈称为空栈。

栈又称为后进后出(Last In First Out)的线性表，简称LIFO结构



#### 2.栈的顺序存储结构及实现

顺序栈

```C
typedef struct{
	ElemType data[MAXSIZE]；
	int top;   /* 用于栈顶指针*/
}SqStack;
```



#### 3.两栈共享空间

```C
typedef struct{
	ElemType data[MAXSIZE]；
	int top1;   /* 用于栈1栈顶指针*/
	int top2;   /* 用于栈2栈顶指针*/
}SqDoubleStack;
```



使用这样的数据结构通常是两个栈的空间需求有相反关系，比如股票，买入时，一定是有人在卖出

如果是不相同数据类型的栈，这种方法不但不能更好的处理问题，反而会使问题变得更复杂。



#### 4.栈的链式存储结构及实现

链栈

```C
typedef struct StackNode{
	SElemType data;
	struct StackNode *next;
}StackNode, *LinkStackPtr;

typedef struct{
	LinkStackPtr top;
	int count;
}LinkStack;
```



#### 5.栈的应用

##### 1.递归

###### 1.递归的定义

一个直接调用自己或者通过一系列的调用语句间接调用自己的函数



每个递归定义必须至少又一个条件，满足时递归不再进行，即不再引用自身而是返回值退出



简单地说，在前行阶段，对于每一层递归，函数的局部变量、参数值以及返回地址都被压入栈中。

在退回阶段，位于栈顶的局部变量、参数值和返回地址被弹出，用于返回调用层次中执行代码的其余部分，也就是回复了调用的状态



##### 2.四则运算

## 队列

### 1.队列的定义

队列(queue)是只允许在一段进行插入操作，而在另一端进行删除操作的线性表



队列是一种先进先出(First In First Out)的线性表，简称FIFO。允许插入的一段为队尾，允许删除的一端称为队头



### 2.队列顺序存储

问题：“假溢出”

解决办法：循环队列

**队列头尾相连的顺序存储结构称为循环队列**



```C
typedef struct {
	QElemType data[MAXSIZE];
	int front;				/*头指针*/
	int rear;				/*尾指针，若队列不空，指向队列尾元素的下一个位置*/
}SqQueue;
```



### 3.队列链式存储

队列的链式存储，就是线性表的单链表，只不过它只能尾进头出而已，简称为链队列。



```C
typedef struct QNode{     /*结点结构*/
    QElemtype data;
    struct QNode *next;
}QNode,*QueuePtr;

typedef struct{           /*队列链表结构*/
    QueuePtr front, rear; /*队头、队尾指针*/
}LinkQueue;
```





















# 串

## 1.串的定义

串(string)是由零个或多个字符组成的有限序列，又叫字符串



## 2.串的存储结构

### 2.1顺序存储结构

### 2.2链式存储结构

总的来说不如顺序存储灵活，也不如顺序存储结构好



## 3.模式匹配算法

**字串的定位操作通常称做串的模式匹配**

n为主串长度、m为要匹配的子串长度

最好情况：一开始就匹配成功，比如"googlegood"中找"google"，时间复杂度为O(m)

稍差一些：每次首字母不匹配，比如"abcdefgoogle"中找"google"，时间复杂度为O(n+m)

最坏情况：每次匹配不成功都发生在最后一个位置，比如"0000000000000000000000000001"中找"0000001"，时间复杂度为O((n-m+1)*m)

**低效**



#### 3.1 KMP模式匹配算法

思想：



代码实现：1.初始化

​					2.前后缀相同情况

​					3.前后缀不同情况

​					4.更新next值

```C
void get_Next(*next, s){
	/*i 后缀末尾 、 j 前缀末尾【也指i之前（包括i）最长相等前后缀长度】*/
    
    //初始化
    j = 0;		/*前缀从最开始的位置开始*/
    next[0] = 0;
    
    for(i = 1; i < s.size(); i++){	/*i要从位置1开始*/
        
        //前后缀不同情况
        while(j > 0 && s[i] != s[j])  /*不能写成if*/
            j = next[j - 1];
        
        //前后缀相同情况
        if (s[i] == s[j])
            j++;
        
        //更新next值
        next[i] = j;
    }
}
```



#### 3.2 改进的KMP算法



代码实现

```C
void get_nextval(*nextval, s){
    while (i < T[0]){
        if(j == 0 || T[i] = T[k]){
             ++i;
             ++j;
            //区别如下
            if (T[i] != T[k])   nextval[i] = j;		/*若当前字符与前缀字符不同，则nextval与next无异*/
            else   nextval[i] = nextval[j];			/*若相同，则将nextval值赋值给nextval在i的位置的值*/
        }
        else k = nextval[k];
    }
}
```













# 树

## 1.树的定义

树(Tree)是n(n>=0)个结点的有限集。n=0时称为空树。

任意一颗非空树中：1）有且仅有一个特定的根(Root)结点

​								   2）当n>1时，其余结点可分为m(m>0)个互不相交的有限集，其中每个集合本身又是一棵树，并且称为根的子树(Sub Tree)



### 1.1结点的分类

结点拥有的子树数称为结点的**度(Degree)**

度为0的结点称为**叶结点(Leaf)**或终端结点

度不为0的结点称为非终端结点或分支结点

树的度是树内各结点的度的最大值



### 1.2结点间的关系

结点的子树的根称为该结点的**孩子(Child)**，相应的，该结点称为孩子的**双亲(Parent)**

同一个双亲的孩子之间互称**兄弟(Sibling)**

结点的祖先是从根到该结点所经分支上的所有结点

以某结点为根的子树中的任一结点都称为该节点的子孙



### 1.3其他相关概念

**层次(Level)**：从根开始定义起，根为第一层，根的孩子为第二层

双亲在同一层的结点互为**堂兄弟**

树中结点最大层次称为树的**深度(Depth)**

如果将树中结点的各子树看成是从左到右有次序的，不能互换的则称为**有序树**，否则称为**无序树**



### 1.4线性表与树

|                           线性结构                           |                            树结构                            |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| 第一个数据元素：无前驱<br />最后一个数据元素：无后继<br />中间元素：一个前驱，一个后继 | 根结点：无双亲，唯一<br />叶结点：无孩子，可以多个<br />中间结点：一个双亲，多个孩子 |







## 2.树的存储结构

### 2.1双亲表示法

在每个结点中，附设一个指示器指示其双亲结点在数组中的位置

| data | parent |
| :--: | :----: |

其中，data为数据域，parent为指针域，存储该结点的双亲在数组中的下标



代码实现

```C
//结点结构
typedef struct PTNode{	
    TElemType data;			/*结点数据*/
    int parent;				/*双亲位置*/
}PTNode;

//树结构
typedef struct{
    PTNode nodes[MAX_TREE_SIZE];	/*结点数组*/
    int r,n;						/*根的位置和结点数*/
}PTREE;
```



这样的存储结构可以很快找到他的双亲结点，所用时间复杂度为O(1)

但若要知道结点的孩子是什么，就只能遍历整个结构

所以可以增加一个长子域

我们又关注结点的孩子、有关注结点的兄弟、对时间遍历的要求比较高，那么我们可以把此结构扩展为双亲域、长子域、右兄弟域

**存储结构设计是一个非常灵活的过程**

**一个存储结构设计的是否合理，取决于基于该存储结构的运算是否适合、是否方便，时间复杂度好不好等**



### 2.2孩子表示法

****

**每个结点有多个指针域，其中每个指针指向一颗子树的根结点，我们把这种方法叫做多重链表表示法**



1. 方案1

   指针域的个数等于树的度

   | data | child1 | child2 |  ……  | childd |
   | :--: | :----: | :----: | :--: | :----: |

   若树中各结点的度相差很大时，浪费空间

   若相差较小，开辟的空间被充分利用了，则缺点变优点

2. 方案2

   指针域的个数等于该结点的度，专门取一个位置来存储结点指针域的个数

   | data | degree | child1 | child2 |  ……  | childd |
   | :--: | :----: | :----: | :----: | :--: | :----: |

   克服了浪费空间的缺点，提高了空间利用率

   但由于各结点的链表结构不同，加上要维护结点的度和数值，在运算上就会带来时间上的损耗



所以采用孩子表示法

具体办法是：

**把每个结点的孩子排列起来，以单链表作为存储结构，则n个节点有n个孩子链表**

**如果是叶子结点则此单链表为空。**

**然后n个头指针又组成一个线性表，采用顺序存储结构，存放进一堆数组中**



为此，设计了两种结点结构

1.孩子链表的孩子结点

| child | next |
| :---: | :--: |

其中，child是数据域，用来存储某个结点在表头数组中的下标；next是指针域，用来存储指向某结点的下一个孩子结点的指针

2.表头数组的表头结点

| data | firstchild |
| :--: | :--------: |

其中，data是数据域，存储某结点的数据信息；firstchild是头指针域，存储该结点的孩子链表的头指针



代码实现

```C
//孩子结点
typedef struct CTNode{
    int child;
    struct CTNode *next;
}*ChildPtr;

//表头结构
typedef struct{
    TElemType data;
    ChildPtr firstchild;
}CTBox;

//树结构
typedef struct{
    CTBOX nodes[MAX_TREE_SIZE]; 	/*结点数组*/
    int r,nl						/*根的位置和结点数*/
}CTree;
```



### 2.3孩子兄弟表示法

任何一棵树，它的结点的第一个孩子如果存在就是唯一的，它的右兄弟如果存在也是唯一的。

因此，我们设置两个指针，分别指向该结点的第一个孩子和此结点的右兄弟

| data | firstchild | rightsib |
| :--: | :--------: | :------: |

data为数据域；firstchild为指针域，存储长子结点的存储地址；rightsib是指针域，存储该结点的右兄弟结点的存储地址；

**将复杂的树变为二叉树**





## 3.二叉树

二叉树(Binary Tree)是n(n>=0)个结点的有限集合，该集合或者为空集(称为空二叉树),或者由一个根节点和两棵互不相交、分别称为根结点的左子树和右子树的二叉树组成



### 3.1二叉树特点

1. 每个结点最多有两棵子树
2. 左子树和右子树是有顺序的
3. 即使树中某结点只有一颗子树，也要区分它是左子树还是右子树



### 3.2特殊二叉树

1. 斜树

   所有结点都只有左子树的二叉树叫左斜树，所有结点都只有右子树的二叉树叫右斜树

2. 满二叉树

   所有分支点都存在左子树和右子树，且所有叶子结点都在同一层

3. 完全二叉树

   对一棵具有n个结点的二叉树按层序编号，如果编号为i的结点与同样深度的满二叉树中编号为i的结点在二叉树中位置相同，称为完全二叉树





### 3.3二叉树性质

性质1：在二叉树的第i层最多有2<sup>i-1</sup>个结点(i>=1)

性质2：深度为k的二叉树至多有2<sup>k</sup>-1个结点(k>=1)

性质3：对任何一棵二叉树T，如果其终端节点为n<sub>0</sub>，度为2的结点数为n<sub>2</sub>，则n<sub>0</sub> = n<sub>2</sub> +1

性质4：具有n个结点的完全二叉树的深度为[log<sub>2</sub>n]+1

性质5：如果一棵有n个结点的完全二叉树的结点按层序编号(从第1层到第[log<sub>2</sub>n]+1层，每层从左到右)，对任一结点i(1<=i<=n)有：

1. 如果i=1，则结点i是二叉树的根，无双亲；如果i>1，则其双亲是结点[i/2]
2. 如果2i>n，则结点无左孩子(结点i为叶子结点);否则其左孩子为结点2i
3. 如果2i+1>n，则结点i无右孩子；否则其右孩子为结点2i+1





## 4.二叉树的存储结构

### 4.1顺序存储结构

一般只用于完全二叉树



### 4.2二叉链表

二叉树每个结点最多有两个孩子，所以为它设计一个数据域和两个指针域



| lchild | data | rchild |
| :----: | :--: | :----: |



```c
//二叉树的二叉链表结点结构定义
typedef struct BiTNode{
    TElemType data;			/*结点结构*/
    struct BiTNode *lchild, *rchild;	/*左右孩子指针*/
}BiTNode, *BiTree
```





## 5.遍历二叉树

**二叉树的遍历时指从根节点出发，按照某种次序依次访问二叉树中所有结点，使得每个结点被访问一次且仅被访问一次**



两个关键词：**访问**和**次序**





### 5.1前序遍历

规则是若二叉树为空，则空操作返回，否则先访问根结点，然后前序遍历左子树，再前序遍历右子树



算法

```c
void PreOrderTraverse(BiTree T){
    if(T == NULL) return;
    printf("%c", T->data);			/*显示结点数据，可改为其他操作*/
    PreOrderTraverse(T -> lchild);	/*先序遍历左子树*/
    PreOrderTraverse(T -> rchild);	/*先序遍历右子树*/
}
```





### 5.2中序遍历

规则是若二叉树为空，则空操作返回，否则从根结点开始(注意不是先访问根结点)，中序遍历根结点的左子树，然后访问根结点，最后中序遍历右子树



算法

```C
void InOrderTraverse(BiTree T){
    if(T == NULL) return;
    InOrderTraverse(T -> lchild);	/*中序遍历左子树*/
    printf("%c", T->data);			/*显示结点数据，可改为其他操作*/
    InOrderTraverse(T -> rchild);	/*中序遍历右子树*/
}
```



### 5.3后序遍历

规则是若二叉树为空，则空操作返回，否则从左到右先叶子后结点的方式遍历访问左右子树，最后访问根结点



算法

```c
void PostOrderTraverse(BiTree T){
    if(T == NULL) return;
    PostOrderTraverse(T -> lchild);	/*后序遍历左子树*/
    PostOrderTraverse(T -> rchild);	/*后序遍历右子树*/
    printf("%c", T->data);			/*显示结点数据，可改为其他操作*/
}
```



### 5.4层次遍历

规则是若二叉树为空，则空操作返回，否则从树的第一层开始访问，从上而下逐层遍历，在同一层中，按从左到右的顺序对结点逐个访问







## 6.二叉树的建立

普通二叉树

{% mermaid %}
graph TD
	A((A)) --- B((B)) & C((C))
    B ---X(( )) & D((D))
    style X fill:#f100,stroke-width:0px
    linkStyle 2 stroke:#off, stroke-width:0px;
{% endmermaid %}

扩展二叉树

{% mermaid %}
graph TD
	A((A)) --- B((B)) & C((C))
    B ---X1((#)) & D((D))
    D ---X2((#)) & X3((#))
    C ---X4((#)) & X5((#))
    classDef X fill:#4169E1
    class X1,X2,X3,X4,X5 X;
{% endmermaid %}



代码实现

```c++
//按前序输入二叉树中结点值（一个字符）
void CreatBiTree(BiTree *T){
    TElemType ch;
    
    cin >> ch;
    
    if(ch == "#") T = NULL;
    else{
        if(!T = new BiTNode) exit(OVERFLOW);
       	
        T->data = ch;			/*生成结点*/
        CreatBiTree(T->lchild); /*构造左子树*/
        CreatBiTree(T->rchild); /*构造右子树*/
    }
}
```





## 7.线索二叉树

指针域未充分利用

将指向前驱和后继的指针称为线索，加上线索的二叉链表称为线索链表，相应的二叉树就称为线索二叉树

| lchild | ltag | data | rtag | rchild |
| :----: | :--: | :--: | :--: | :----: |

其中

- ltag为0时指向该结点的左孩子，为1时指向该结点的前驱
- rtag为0时指向该结点的右孩子，为1时指向该结点的后继



代码实现

```c
typedef enum {Link, Thread} PointTag; 	/*Link==0表示指向左右孩子指针*/
										/*Thread==1表示指向前驱或后继的线索*/
typedef struct BiThrNode{
    TElemType data;						/*结点数据*/
    struct BiThrNode *lchild, *rchild;	/*左右孩子指针*/
    PointerTag LTag,RTagj;				/*左右标志*/
}BiThrNode, *BiThrTree;
```

线索化的过程就是在遍历的过程中修改空指针的过程

中序遍历线索化的递归函数如下

```c
BiThrTree pre;					/*全局变量，始终指向刚刚访问过的结点*/
void InThreading(BiThrTree p){
    if(p){
        InThreading(p->lchild);
        ///////////////////////
        if(!p->lchild){			/*没有左孩子*/
            p—>LTag = Thread;	/*前驱线索*/
            p->lchild = pre;	/*左孩子指针指向前驱*/
        }
        if(!pre->rchild){		/*前驱没有右孩子*/
            pre->RTag = Thread; /*后继线索*/
            pre->rchild = p;	/*前驱右孩子指针指向后继(当前结点p)*/
        }
        pre = p;				/*保持pre指向p的前驱*/
        ///////////////////////
        InThreading(p->rchild);
    }
}
```

遍历代码如下

```c
//T指向头结点，头结点左链lchild指向根结点，头结点右链rchild指向中序遍历的最后一个结点
Status InOrderTraverse_Thr(BiThrTree T){
    BiThrTree p;
    p = T->lchild;
    while(p!=T){					/*空树或者遍历结束时，p == T*/
        while(p->LTag == Link)	p = p->lchild;
        cout << p->data;			/*显示结点数据或其他操作*/
        while(p->RTag == Thread && p->rchild != T){
            p = p->rchild;			/*访问后继结点*/
            cout << p->data;
        }
        p = p->rchild;				/*p进至其右子树根*/
    }					
}
```

**如果所用的二叉树需要经常遍历或查找结点时需要某种遍历序列中的前驱和后继，那么采用线索二叉树链表的存储结构就是非常不错的选择**





## 8.树、森林、二叉树的转换

**树 --> 二叉树**：

1.将所有兄弟结点间增加连线

2.只保留和第一个孩子结点的连线，删除与其他孩子结点连线

3.本身孩子结点为左孩子结点，兄弟结点为右孩子结点



**森林 --> 二叉树**

1.把每棵树转化为二叉树

2.第一棵二叉树不懂，从第二棵二叉树开始依次将后一棵二叉树的根节点作为前一棵的根节点的右孩子



## 9.哈夫曼树及其应用

### 9.1哈夫曼树的定义及原理

最基本的压缩编码方法-------哈夫曼编码



带权路径长度WPL最小的二叉树称作哈夫曼树



1. 先把有权值的叶子结点按照从小到大的顺序排列成有序序列，即A5,E10, B15, D30, C40
2. 取头两个最小权值结点形成新结点N<sub>1</sub>，相对较小的为左孩子
3. N<sub>1</sub>替换A、E，插入有序序列中重复2



### 9.2哈夫曼编码















# 图

## 1.图的定义及术语

## 2.图的存储结构

### 2.1邻接矩阵

图的邻接矩阵存储方式是用两个数组来表示图。

一个一维数组存储图中顶点信息，一个二维数组（称为邻接矩阵）存储图中的边的信息

{% mermaid %}
graph TD
V0 --- V1 & V2 & V3
V2 --- V1 &  V3
{% endmermaid %}

顶点数组： 

|  V0  |  V1  |  V2  |  V3  |
| :--: | :--: | :--: | :--: |

邻接矩阵：

|  0   |  1   |  1   |  1   |
| :--: | :--: | :--: | :--: |
|  1   |  0   |  1   |  0   |
|  1   |  1   |  0   |  1   |
|  1   |  0   |  1   |  0   |

**邻接矩阵存储结构**

```c
typedef struct{
    VertexType vexs[MAXVEX];		/*顶点表*/
    EdgeType arc[MAXVEX][MAXVEX];	/*邻接矩阵，可看作边表*/
    int numNodes, numEdges;			/*图中的定点数和边数*/
}MGraph;
```



**无向网图创建代码**

```c
void CreatMGraph(MGraph *G){
    int i, j, k, w;
    cout << "请输入顶点数和边数";
    cin >> G->numNodes >> G->numEdges;						/*输入顶点数和边数*/
    for(i = 0; i < G->numNodes; i++)	cin >> G->vexs[i];	/*读入顶点信息，建立顶点表*/
    for(i = 0; i < G->numNodes; i++)
        for(j = 0; j < G->numNodes; j++)
            G->arc[i][j] = INFINITY;						/*初始化邻接矩阵*/
    for(k = 0; k < G->numEdges; k++){
        cout << "输入边(vi,vj)的下标i,j和权w：\n";
        cin >> i >> j >> w;
        G->arc[i][j] = w;
        G->arc[j][i] = G->arc[i][j];						/*无向图，所以矩阵对称*/
    }
}
```





### 2.2邻接表

数组与链表相结合的存储方式称为邻接表

1.用数组存储顶点

| data | firstedge |
| :--: | :-------: |

2.用链表存储临界点

| adjvex | next |
| :----: | :--: |

有向图中，邻接表可以算出度

逆邻接表可以算入度

```c
typedef struct EdgeNode{					/*边表结点*/
    int adjvex;								/*邻接点域，存储该顶点对应下标*/
    EdgeType info;							/*用于存储权值，对非网图可以不要*/
    struct EdgeNode *next;					/*链域，指向下一个邻接点*/
}EdgeNode；
    
typedef struct VertexNode{					/*顶点表结点*/
    VertexType data;						/*顶点域，存储顶点信息*/
    EdgeNode *firstedge;					/*边表头指针*/
}VertexNode,AdjList[MAXVEX];

typedef struct{
    AdjList adjlist;
    int numNodes, numEdges;					/*图中当前顶点数和边数*/
}GraphAdjList;
```

**邻接表的创建**

```c
//建立图的邻接表结构
void CreatALGraph(GraphAdjList *G){
    int i, j, k;
    EdgeNode *e;
    cout << "请输入顶点数和边数";
    cin >> G->numNodes >> G->numEdges;
    for(i = 0; i < G->numNodes; i++){		/*读入顶点信息，建立顶点表*/
        cin >> G->adjList[i].data;			/*输入顶点信息*/
        G->adjList[i].firstedge = NULL;		/*边表置为空表*/
    }
    
    for(k = 0; k < G->numEdges; k++){		/*读入顶点信息，建立边表*/
        cout << "输入边(vi,vj)上的顶点序号:";
        cin >> i >> j;
        ////////////////////////////////////////////////////////////
        e = new EdgeNode;
        e->adjvex = j;
        e->next = G->adjList[i].firstedge;
        G->adjList[i].firstedge = e;		/////头插法
        e = new EdgeNode;
        e->adjvex = i;
        e->next = G->adjList[j].firstedge;
        G->adjList[j].firstedge = e;
        ////////////////////////////////////////////////////////////
    }
}
```



### 2.3十字链表

将邻接表与逆邻接表结合起来

顶点表结点结构如下

| data | firstin | firstout |
| :--: | :-----: | :------: |

边表结点如下

| tailvex | headvex | headlink | taillink |
| :-----: | :-----: | :------: | :------: |

tailvex：边起点在顶点表中下标

headvex：边终点在定点表中下标

headlink：入边表指针域，指向终点相同的下一条边

taillink：出边表指针域，指向起点相同的下一条边





### 2.4邻接多重表



### 2.5边集数组

边集数组是由两个一维数组构成。

一个存储顶点信息，一个存储边的信息

顶点数组

|  V0  |  V1  |  V2  |  V3  |  V4  |
| :--: | :--: | :--: | :--: | :--: |

边数组

| begin | end  | weight |
| :---: | :--: | :----: |





## 3.图的遍历

从图中某一顶点出发访遍图中其余顶点，且使每一个顶点仅被访问一次，这一过程就叫做图的遍历

**遍历实质**：图的邻接点



### 3.1深度优先遍历

深度优先遍历(Depth First Search) **DFS**

**类似树的前序遍历**



从图中某个顶点V出发，访问此顶点，然后从V的未被访问的邻接点出发深度优先遍历图，直至图中所有和v有路径相通的顶点都被访问到

若图中尚有顶点未被访问，则另选图中一个未曾被访问的顶点作为起始点，重复上述过程，直至图中所有顶点都被访问到为止

```c
//邻接矩阵的深度优先递归算法
void DFS(MGraph G, int i){
    int j;
    visitet[i] = TRUE;
    cout << G.vexs[i];							/*访问顶点，也可做其他操作*/
    for(j = 0; j < G.numVertexes; j++)			
        if(G.arc[i][j] == 1 && !visited[j])		/*G.arc[i][j]为1代表邻接，visited[i] = 0代表未被访问*/
            DFS(G, j);							/*对未访问的顶点做递归调用*/
}
```

用**邻接矩阵**表示图，遍历图中每个顶点都要从头扫描该顶点所在行，时间复杂度O(n<sup>2</sup>)

------



```c
//邻接表的深度优先递归算法
void DFS(GraphAdjList GL, int i){
    EdgeNode *p;
    visit[i] = TRUE;
    cout << GL.adjList[i].data;					/*打印顶点，也可做其他操作*/
    p = GL->adjList[i].firstedge;
    while(p){
        if(!visited[p->adjvex])
            DFS(GL, p->adjvex);
        p = p->next;
    }
}
```

用**邻接表**来表示图，有2e个表结点，但只需扫描e个结点即可完成遍历，加上访问n个头结点，时间复杂度为O(n+e)





### 3.2广度优先遍历

广度优先遍历(Breadth First Search) **BFS**

**类似树的层序遍历**

```c
//邻接矩阵的广度遍历
void BFS(Graph G){
    int i, j;
    InitQueue(Q);								/*辅助队列初始化,置空*/
    for(i = 0; i < G.numVertexes; i++){			/*对每个顶点做循环*/
        if(!visited[i]){						/*若是未被访问过就处理*/
            visited[i] = TRUE;					/*标记为已访问*/
            cout << G.vexs[i];					/*访问顶点*/
            EnQueue(Q,i);						/*当前顶点入队*/
            while(!QueueEmpty(Q)){				/*若当前队列不为空*/
                DeQueue(Q,i);					/*将队首元素出队列，赋值给i*/
                for(j = 0; j < G.numVertexes; j++){				
                    if(G.arc[i][j] == 1 && !visited[j]){		/*判断其他顶点，若与当前顶点存在边且未访问过*/
                        visited[j] == TRUE;						
                        cout << G.vexs[j];						/*访问顶点*/
                        EnQueue(Q,j);							/*将找到的顶点入队列*/
                    }
                }
            }
        }
    }
    
}
```



```c
//邻接表的广度遍历
void BFS(GraphAdjList GL){
    int i;
    EdgeNode *p;
    Queue Q;
    InitQueue(Q);
    for(i = 0; i < GL->numVertexes; i++){
        if(!visited[i]){
            visit[i] = TRUE;
            cout << G.vexs[i];					/*访问顶点*/
            EnQueue(Q,i);						/*当前顶点入队*/
            while(!QueueEmpty(Q)){
                DeQueue(Q,i);
                p = GL->adjustList[i].firstedge;/*找到当前顶点的边表链的表头指针*/
                while(p){
                    if(!visited[p->adjvex]){	/*若顶点未被访问*/
                        visited[p->adjvex] = TRUE;
                        cout << GL->adjList[p->adjvex].data;/*访问顶点*/
                        EnQueue(Q,p->adjvex);   /*将此顶点入队列*/
                    }
                    p = p->next;				/*指针指向下一个邻接点*/
                }
            }
        }
    }
}
```







## 4.最小生成树

构造连通网的最小代价生成树称为最小生成树



### 4.1Prim算法

```c
//Prim算法生成最小生成树
void MiniSpanTress_Prim(MGraph G){
    int min, i, j, k;
    int adjvex[MAXVEX];						/*邻接点下标*/
    int lowcost[MAXVEX];					/*保存权值*/
    for(i = 1; i < G.numVertexes; i++){
        lowcost[i] = G.arc[0][i];			/*将V0顶点与其他所有点连接的权值存入数组*/
        adjvex[i] = 0;						/*初始化为V0下标*/
    }
    for(i = 1; i < G.numVertexes; i++){
     	min = INFINITY;						/*初始化最小权值为∞,可设为较大数字*/
        j = 1; k = 0;
        //找到最小权值边，并将最小权值边的邻接点存入k
        while(j < G.numVertexes){				
            if(lowcost[j] != 0 && lowcost[j] < min){
                min = lowcost[j];
                k = j;
            }
        }
        
        cout << "(" + adjvex[k] + "," + k + ")";
        lowcost[k] = 0;						/*当前点已完成任务*/
        //将与k相接的边的权值更新至lowcost数组，并将其邻接点adjvex更新为k
        for(j = 1; j < G.numVertexes; j++){
            if(lowcost[j] != 0 && G.arc[k][j] < lowcost[j]){
                lowcost[j] = G.arc[k][j];
                adjvex[j] = k;
            }
        }
    }
}
```



### 4.2Kruskal算法

```c
//定义边集数组
typedef struct{
    int begin;
    int end;
    int weight;
}Edge;
```

```c
//Kruskal算法生成最小生成树
void MiniSpanTree_Kruskal(MGraph G){
    int i, n, m;
    Edge edges[MAXEDGE];
    int parent[MAXEDGE];					/*判断边是否形成回路*/
    
    /*省略按权值排序*/
    
    //初始化
    for(i = 0; i < G.numVertexes; i++){
        parent[i] = 0
    }
    
    for(i = 0; i < G.numEdges; i++){
        n = Find(parent, edges[i].begin);
        m = Find(parent, edges[i].end);
        if(n != m){							/*m若与n不相等，即未形成环路*/
            parent[n] = m;					/*将此边的结尾顶点放入下标为起点的parent中，表示此顶点已在生成树集合中*/
            printf("(%d, %d) %d", edges[i].begin, edges[i].end, edges[i].weight)
        }
    }
    //查找连接顶点的尾部下标
    int Find(int *parent, int f){
        while(parent[f] > 0){
            f = parent[f];
        }
        return f;
    }
}
```



### 4.3比较

|   算法名   |            Prim算法            |    Kruskal算法     |
| :--------: | :----------------------------: | :----------------: |
|  算法思想  |             选择点             |       选择边       |
| 时间复杂度 | O(n<sup>2</sup>)     n为顶点数 | O(eloge)   e为边数 |
|  适应范围  |             稠密图             |       稀疏图       |





## 5.最短路径

### 5.1Dijkstra算法

数据结构

```c
typedef struct{
    int vexs[MAXVEX];
    int arc[MAXVEX][MAXVEX];
    int numVertexes, numEdges;
}MGraph;

int Patharc[MAXVEX];			/*用于存储最短路径下标的数组*/
int ShortPathTable[MAXVEX];		/*用于存储到各点最短路径的权值和*/
```

算法代码

```c
//Dijkstra算法 求V0到其余顶点的最短路径P[v]及带权长度D[v]
void ShorttestPath_Dijkstra(MGraph G, int v0, Pathace *P, ShortPathTable *D){
    int v, w, k, min;
    int final[MAXVEX];						/*final[k] = 1 表示已求得*/
    //初始化数据
    for(v = 0; v < G.arc[v0][v]; v++){
        final[v] = 0;
        *D[v] = G.arc[v0][v];
        *P[v] = -1;
    }
    *D[v0] = 0;
    final[v0] = 1;
    //开始主循环
    for(v = 1; v < G.numVertexes; v++){
        min = INFINITY;
        //寻找距离v0最近的点
        for(w = 0; w < G.numVertexes; w++){
            if(!final[w] && *D[w] < min){
                k = w;
                min = *D[w];
            }
        }
        final[k] = 1;						/*将目前找到的顶点置1*/
        //修正当前最短路径及距离
        for(w = 0; w < G.numVertexes; w++){
            //如果经过v顶点的路径比现在该路径长度短
            if(!final[w] && (min + arc[k][w] < *G[w])){
                *D[w] = min + arc[k][w];	/*更新最小值*/
                *P[w] = k;					/*更新路径*/
            }
        }
    }
}
```

### 5.2Floyd算法

算法实现

```c
typedef int Patharc[MAXVEX][MAXVEX];
typedef int ShortPathTable[MAXVEX][MAXVEX];

//Floyd算法，求G中各顶点V到其余顶点w的最短路径P[v][w]及带权长度D[v][w]
void ShortestPath_Floyd(MGraph G, Patharc *P, ShortPathTable *D){
    int v, w, k;
    //初始化D与P
    for(v = 0; v < G.numVertexes; ++v){
        for(w = 0; w < G.numVertexes; ++w){
            *D[v][w] = G.arc[v][w];
            *P[v][w] = w;
        }
    }
    
    for(k = 0; k < G.numVertexes; ++k){
        for(v = 0; v < G.numVertexes; ++v){
            for(w = 0; w < G.numVertexes; ++w){
                //如果经过k顶点的路径比原两点路径短
                if(*D[v][w] > *D[v][k] + *D[k][w]){
                    *D[v][w] = *D[v][k] + *D[k][w];
                    *P[v][w] = *P[v][k];
                }
            }
        }
    }
}
```



## 6.拓扑排序

有向无环图

**AOV网**

以顶点表示活动，弧表示活动间优先制约关系



**拓扑有序序列**

在AOV网没有回路的前提下，将全部活动排列成一个线性序列，若从顶点V<sub>i</sub>到V<sub>j</sub>有一条路径，那么V<sub>i</sub>必在V<sub>j</sub>之前

我们称这样的线性序列为**拓扑有序序列**

**检测AOV中是否存在环**

对有向图构造拓扑有序序列，若所有点都在拓扑有序序列中，则AOV网必不存在环



## 7.关键路径

**AOE网**

以弧表示活动，以顶点表示活动的开始或者结束事件

**关键路径**

路径长度最长的路径

### 7.1定义参数

|     定义参数      |               作用                |
| :---------------: | :-------------------------------: |
| ve(V<sub>j</sub>) | 表示事件V<sub>j</sub>最早发生时间 |
| vl(V<sub>j</sub>) | 表示事件V<sub>j</sub>最迟发生时间 |
|       e(i)        |       表示活动i最早开始时间       |
|       l(i)        |       表示活动i最晚开始时间       |

l(i) - e(i) -----表示完成活动i的时间余量

**关键活动** -----l(i) == e(i)



**求关键路径步骤**

1. 求ve(V<sub>j</sub>)、vl(V<sub>j</sub>)
2. 求e(i)、l(i)
3. 计算l(i) - e(i)





# 查找

## 1.查找概论

**查找表(Search Table)**是由同一类型的数据元素构成的集合

**关键字(Key)**是数据元素中的某个数据项的值

若此关键字可以唯一地标记一个记录，则称此关键字为**主关键字(Primary Key)**

对于可以识别多个数据元素的关键词，称为**次关键字(Secondary Key)**



**查找就是根据给定的某个值，在查找表中确定一个其关键字等于给定值的数据元素**



**静态查找表**：只做查找操作的查找表

1. 查询特定的数据元素是否在查找表中
2. 检索特定的数据元素和各种属性



**动态查找表**：在查找过程中同时插入表中不存在的数据元素，或者从查找表中删除已经存在的某个数据元素

1. 查找时插入数据元素
2. 查找时删除数据元素





## 2.顺序表查找

针对线性表进行查找操作，所以为静态查找表



**顺序查找(Sequential Search)**又叫线性查找，是最基本的查找技术，查找过程如下：

从表中第一个（或最后一个）记录开始，逐个进行记录的关键字和给定值比较

若某个记录的关键字和给定值相等，则查找成功

若直到最后一个（或者第一个）记录的关键字和给定值比较都不等时，查找失败



实现算法如下

```c
int Sequential_Search(int *a, int n, int key){
    int i;
    for (i = 1; i <= n; i++){
        if (a[i] == ket)
            return i;
    }
    return 0;
}
```

优化

```c
//有哨兵顺序查找
int Sequential_Search2(int *a, int n, int key){
    int i;
    a[0] = key;					/*设置a[0]为关键字值，称之为“哨兵”*/
    i = n;						/*循环从数组尾部开始*/
	while (a[i] != key){
        i--;
    }
    return i;
}
```



## 3.有序表查找

### 3.1二分查找

**折半查找(Binary Search)**又称二分查找

前提是线性表中记录必须是**关键码有序**（通常从小到大有序），线性表必须采用顺序存储



```c
int Binary_Search(int *a, int n, int key){
    int low, high, mid;
    low = 1;
    high = n;
    while (low <= high){
        mid = (low + high) / 2;
        if (key < a[mid])
            high = mid - 1;
        else if(key > a[mid])
            low = mid + 1;
        else 
            return mid;
    }
    return 0;
}
```



**时间复杂度O(logn)**



### 3.2插值查找

将二分查找的代码做略微变换

$$mid = \frac{low + high}{2}$ =$low + \frac{1}{2}(high - low)$$

改为以下计算方案

$$mid = low + \frac{key - a[low]}{a[high] - a[low]}(high - low)$$





### 3.3斐波那契查找



```c
int Fibonacci_Search(int *a, int n, int ket){		/*F[n]为已经计算好的斐波那契数列*/
    int low, high, mid, i, k;
    low = 1;
    high = n;
    k = 0;
    while (n > F[k] - 1)							/*计算n位斐波那契数列的位置*/
        k++;											
    for (i = n; i < F[K] - 1; i++)					/*将数值补全*/
        a[i] = a[n];
    //查找开始
    while (low <= high){							
        mid = low + F[K - 1] - 1;					/*计算当前分隔下标*/
        if (key < a[mid]){
            high = mid - 1;
            k = k - 1;
        }
        else if (key > a[mid]){
            low = mid + 1;
            k = k - 2;
        }
        else{
            if (mid <= n)
                return mid;
            else
                return n;
        }
    }
    return 0;
}
```

**时间复杂度O(logn)**

### 3.4对比

时间复杂度相同

斐波那契查找只进行简单加减法运算$mid=low+F[k-1]-1$

折半查找进行加法与除法运算$mid=\frac{low+high}{2}$

插值查找进行复杂四则运算$$mid = low + \frac{key - a[low]}{a[high] - a[low]}(high - low)$$

三种有序表的查找法本质上是分隔点选择不同，各有优劣





## 4.线性索引查找

索引就是把一个关键字与它对应的记录相关联的过程

线性索引就是将索引项集合组织为线性结构，也称为**索引表**



### 4.1稠密索引

稠密索引是指在线性索引中，将数据集中的每个记录对应一个索引项

对于稠密索引来说，**索引项一定是按照关键码有序排列的**

意味着可以用到折半、插值、斐波那契等有序查找法



### 4.2分块索引

分块有序，是把数据集的记录分成了若干块，并且这些块需要满足一下两个条件

1. 块内无序
2. 块间有序

我们定义的分块索引项结构分三个部分

- 最大关键码
- 存储块中记录个数
- 用于指向块首数据元素的指针



在分块索引表中查找就是进行以下两步

1. 在分块索引表中查找要查关键字所在的块
2. 根据块首指针找到相应的块，并在块中顺序查找关键码



总的来说，分块索引在兼顾了对细分块不需要有序的情况下，大大增加了整体查找的速度，所以普遍被用于数据库表查找等技术的应用当中



### 4.3倒排索引

索引项的通用结构是

- 次关键码
- 记录号表

其中记录号表存储具有相同次关键字的所有记录的记录号（可以是指向记录的指针或者是该记录的主关键字）



## 5.二叉排序树

**二叉排序树(Binary Sort Tree)**，又称为二叉查找树。它或者是一棵空树，或者是具有以下性质的二叉树

- 若它的左子树不空，则左子树上所有结点的值均小于它的根结点的值
- 若它的右子树不空，则右子树上所有结点的值均大于它的根结点的值
- 它的左、右子树也分别为二叉排列树

构造一棵二叉排序树的目的，不是为了排序，而是为了提高查找和插入删除关键字的速度



### 5.1查找操作

```c
//二叉树的二叉链表的结点结构定义
typedef struct BiTNode{
    int data;
    struct BiTNode *lchild, *rchild;
}BiTNode, *BiTree;
```



二叉排序树的查找

```c
Status SearchBST(BiTree T, int key, BiTree f, BiTree *p){
    //递归查找二叉排序树T中是否存在key
    if (!T){								/*若查找不成功，指针p指向查找路径上访问的最后一个结点并返回FALSE*/
        *p = f;
        return FALSE;
    }
    else if (key == T->data){				/*若查找成功，则指针p指向该数据元素结点，并返回TRUE*/
        *p = T;
        return TRUE;
    }
    else if (key < T->data)
        return SearchBST(T->lchild, key, T, p); /*在左子树中继续查找*/
   	else if (key > T->data)
        return SearchBST(T->rchild, key, T, p); /*在右子树中继续查找*/
}
```



### 5.2插入操作

将关键字放到树中合适的位置

```c
Status InsertBST(BiTree *T, int key){
    BiTree p, s;
    if (!SearchBST(*T, key, NULL, &p)){			/*查找不成功*/
        s = new BiTNode;
        s->data = key;
        s->lchild = s->rchild = NULL;
        if (!p)
            *T = s;								/*插入s为新的根结点*/
        else if (key < p->data;)				
            p->lchild = s;						/*插入s为左孩子*/
        else
            p->rchild = s;						/*插入s为右孩子*/
        return TRUE;
    }    
    else 
        return FALSE;							/*树中已有与关键字相同结点，不再插入*/
}
```



### 5.3删除操作

删除结点三种情况

- 叶子结点
- 仅有左子树或右子树结点
- 左右子树都有的结点

```c
//查找关键字等于key的结点，找到则删除数据结点
Status DeleteBST(BiTree *T, int key){
    if (!T)
        return FLASE;
    else{
        if (key == T->data)						/*找到关键字key的数据元素*/
            return Delete(T);
        else if (key < T->data)
            return DeleteBST(T->lchild, key);
        else 
            return DeleteBST(T->rchild, key);
    }
}
```

上述代码与二叉排序树查找几乎完全相同，区别在于找到后执行的是删除操作



```C
Status Delete(BiTree *p){
    //从二叉排序树中删除结点p，并重接他的左右子树
    BiTree *q, *s;
    if (p->rchild == NULL){						/*右子树空则重接左子树(叶子也走此分支)*/
        q = p;
        p = p->lchild;
        delete(q);
    }
    else if (p->lchild == NULL){				/*左子树空则重接右子树*/
        q = p;
        p = p->rchild;
        delete q;
    }
    else {										/*左右均不空*/
        q = p;
        s = p->lchild;
        while (s->rchild){						/*找到左子树的右结点（找到待删结点的前驱）*/
            q = s;
            s = s->rchild;
        }					
        p->data = s->data;
        if (q != p)
            q->rchild = s->lchild;
        else
            q->lchild = s->lchild;
        delete s;
    } 
}
```



## 6.平衡二叉树

平衡二叉树是一种二叉排序树，其中每个结点的左子树和右子树高度差至多为1

是一种高度平衡的二叉排序树，二叉树上节点的左子树高度减去右子树高度的值称为**平衡因子BF(Balance Factor)**

那么平衡二叉树上所有结点的平衡因子只可能是1、0、-1

距离插入结点最近的，且平衡因子的绝对值大于1的结点为根的子树，我们称为**最小不平衡树**



{% mermaid %}
graph TD

	A1((A)) --- B1((B)) & D1(( ))
	B1 --- C1((C)) & E1(( ))
	%%style D fill:#f100,stroke-width:0px
    %%style E fill:#f100,stroke-width:0px%% 设置F属性为填充为白色，边框宽度为0
    linkStyle 1 stroke:#off, stroke-width:0px;
    linkStyle 3 stroke:#off, stroke-width:0px;
    
    
	A2((A)) --- B2((B)) & D2(( ))
	B2 --- C2(( )) & E2((C))
    linkStyle 5 stroke:#off, stroke-width:0px;
    linkStyle 6 stroke:#off, stroke-width:0px;
    
    A3((A)) --- B3(( )) & D3((B))
	D3 --- C3((C)) & E3(( ))
    linkStyle 8 stroke:#off, stroke-width:0px;
    linkStyle 11 stroke:#off, stroke-width:0px;
    
    A4((A)) --- B4(( )) & D4((B))
	D4 --- C4(( )) & E4((C))
    linkStyle 12 stroke:#off, stroke-width:0px;
    linkStyle 14 stroke:#off, stroke-width:0px;
    
    class D1,E1,D2,C2,B3,E3,B4,C4 X;
	classDef X fill:#f100, stroke-width:0px;
{% endmermaid %}

{% mermaid %}
graph TD
	A1((B)) --- B1((C)) & D1((A))
	A2((C)) --- B2((B)) & D2((A))
	A3((C)) --- B3((A)) & D3((B))
	A4((B)) --- B4((A)) & D4((C))
{% endmermaid %}

### 6.1代码实现

**结点结构**

增加一个变量`bf`用来存储平衡因子

```c
typedef struct BiTNode;{
    int data;
    int bf;
    struct BiTNode *lchild, *rchild;
}BiTNode, *BiTree;
```

**右旋操作**

```c
//对P为根的二叉排序树作右旋处理
void R_Rotate(BiTree *p){
    BiTree *L;
    L = p->lchild;
    p->lchild = L->lchild;
    L->rchild = p;
    p = L;
}
```

**左旋操作**

```c
//对P为根的二叉排序树作左旋处理
void L_Rotate(BiTree *p){
    BiTree *R;
	R = p->rchild;
    p->rchild = R->lchild;
    R->lchild = p;
    p = L;
}
```

**左平衡旋转**

```c
#define LH +1										/*左高*/
#define EH 0										/*等高*/
#define RH -1										/*右高*/

void LeftBalance(BiTree *T){
    BiTree *L, *Lr;
    L = T->lchild;
    switch (L->bf){									/*检查T的左子树平衡度，并做相应处理*/
        case LH:									/*（LL）新结点插入在T的左孩子的左子树上，要作单右旋处理*/
            T->bf = L->bf =EH;
            R_Rotate(T);
            break;
        case RH:									/*新结点插入在T的左孩子的右子树上，要做双旋处理*/
            Lr =L->rchild;							/*Lr指向T的左孩子的右子树根*/
            switch (Lr->bf){						/*修改T及其左孩子的平衡因子*/
                case LH:
                    T->bf = RH;
                    L->bf = EH;
                 	break;
                case EH:
                    T->bf = L->bf =EH;
                	break;
                case RH:
                    T->bf = EH;
                    L->bf = LH;
                    break;
            }
            Lr->bf =EH;
            L_Rotate(T->lchild);
            R_Rotate(T);
    }
}
```

**右平衡旋转**

```c
void RightBalance(BiTree *T){
    BiTree *R, *Rl;
    R = T->lchild;
    switch (R->bf){									/*检查T的右子树平衡度，并做相应处理*/
        case RH:									/*（RR）新结点插入在T的右孩子的右子树上，要作单左旋处理*/
            T->bf = R->bf =EH;
            L_Rotate(T);
            break;
        case LH:									/*新结点插入在T的右孩子的左子树上，要做双旋处理*/
            Rl =R->lchild;							/*Rl指向T的右孩子的左子树根*/
            switch (Rl->bf){						/*修改T及其右孩子的平衡因子*/
                case RH:
                    T->bf = LH;
                    R->bf = EH;
                 	break;
                case EH:
                    T->bf = R>bf =EH;
                	break;
                case LH:
                    T->bf = EH;
                    R->bf = RH;
                    break;
            }
            Rl->bf =EH;
            R_Rotate(T->rchild);
            L_Rotate(T);
    }
}
```





## 7.多路查找树（B树）

**多路查找树（Muiltl-Way Search Tree）**，其每个结点的孩子数可以多于两个，且每一个结点处可以存储多个元素



设置一个结点数据元素上限set a cap on the num of items

如果超出上限，就将其中一个元素给双亲结点if more than cap, give an item to parent

**left-middle**

再将超出上限的结点分成左右两个结点



### 7.1 2-3树

每个结点都有两个孩子或三个孩子

一个2结点包含一个元素和两个孩子（或没有孩子）

一个3结点包含一小一大两个元素和三个孩子（或没有孩子）





### 7.2 2-3-4树

一个4结点包含小中大3个元素和4个孩子（或没有孩子）



### 7.3 B树

**B树(B-tree)**是一种平衡的多路查找树，2-3树和2-3-4树都是B树的特例

结点最大的孩子数目称为B树的阶



### 7.4 B+树



## 8.散列表（哈希表）

### 8.1定义

$存储位置 = f (关键字)$

散列技术是在记录的存储位置和它的关键字之间建立一个确定的对应关系$f$,使得每个关键字key对应一个存储位置$f(key)$

对应关系$f$称为**散列函数**，又称**哈希(Hash)函数**

采用散列技术将记录存储在一块连续的存储空间中，这块连续存储空间称为**散列表**或**哈希表(Hash Table)**



散列技术既是一种存储方法，也是一种查找方法

散列技术最适合的求解问题是查找与给定值相等的记录



两个关键字$key_1 \neq key_2$，但是却有$f(key_1) = f(key)_2$，这种现象我们称为**冲突(collision)**，并把$key_1$和$key_2$称为这个函数的同义词(synonym)



### 8.2构造方法

 原则

1. 计算简单
2. 散列地址分布均匀



**1.直接定址法**

去关键字的某个线性函数值为散列地址

$f(key) = a * key + b$



**2.数字分析法**



**3.平方取中法**



**4.折叠法**



**5.除留余数法**

f(key) = key  mod  p

**6.随机数法**



### 8.3处理散列冲突

**1.开放定址法**

开放定址法是一旦发生冲突，就去寻找下一个空的散列地址，只要散列表足够大，空的散列地址总能找到，并将记录存入

公式是

$f_i(key) = (f(key)+d_i) MOD m$  $d_i = 1, 2, 3, …, m-1$

**线性探测法**

本来就不为同义词却争夺同一地址的情况，称为**堆积**



$f_i(key) = (f(key)+d_i) MOD m$  $d_i = 1^2, -1^, 2^2, -2^2,…,q^2, -q^2, q\leq m/2$

增加平方运算的目的是为了不让关键字都聚集在某一块区域，这种方法称为**二次探测法**





**2.再散列函数法**

对于散列表，实现准备多个散列函数

$f_i(key) = RH_i(key)$



这种方法可以使得关键字不产生聚集，相应增加了计算时间



**3.链地址法**

将所有关键字为同义词的记录存储在一个单链表中，称这种表为同义词子表

在散列表中只存储所有同义词子表头指针，无论有多少冲突，都只是在当前位置给单链表增加节点的问题



提供了不会出现找不到地址的保障，但查找时需要遍历单链表造成性能损耗



**4.公共溢出区法**

为所有冲突关键字建立一个公共溢出区来存放

查找时，对给定值通过散列表计算出散列地址后，先于基本表的相应位置进行对比，相等则查找成功

不相等，则到溢出表进行顺序查找



相对于基本表而言，冲突数据较少的情况下，公共溢出区的结构对查找性能来说还是非常高的



### 8.4散列表查找的实现

```c
#define SUCCESS 1
#define UNSUCCESS 0
#define HASHSIZE 12
#define NULLKEY -32768

typedef struct{
    int *elem;				/*数据元素存储基址，动态分配数组*/
    int count;				/*当前数据元素个数*/
}HashTable;

int m = 0;					/*散列表表长，全局变量*/
```



```c
//初始化散列表
Status InitHashTable(HashTable *H){
    int i;
    m = HASHSIZE;
    H->count = m;
    H->elem = new int;
    for (i = 0; i < m; i++){
        H->elem[i] = NULLKEY；
    }
    return OK;
}
```



```c
//散列函数
int Hash(int key){
    return key % m;        /*除留余数法*/
}
```



```c
//插入关键字进散列表
void InsertHash(HashTable *H, int key){
    int addr = Hash(key);				/*求散列地址*/
    while (H->elem[addr] != NULLKEY){	/*若不为空，则冲突*/
        addr = (addr + 1) % m;			/*开放定址法的线性探测*/
    }
    H->elem[addr] = key;				/*直到有空位后插入关键字*/
}
```



```c
//散列表查找关键字
Status SearchHash(HashTable H, int key, int *addr){
    *addr = Hash(key);					/*求散列地址*/
    while (H.elem[*addr] != key){		
        *addr = (*addr + 1) % m;		/*开放定址法的线性探测*/
        if (H.elem[*addr] == NULLKEY || *addr == Hash(key))		/*若循环回到原点*/
            return UNSUCCESS;
    }
    return SUCCESS;
}
```





# 排序

优秀排序算法的首要条件就是**速度**

## 1.基本概念与分类

**1.排序的稳定性**

假设$k_i = k_j$，且在排序前的序列中$r_i$领先与$r_j$即（$i < j$）

如果排序后$r_i$仍领先与$r_j$，则称所用的排序方法是稳定的；

反之，若可能使得排序后的序列中$r_j$领先与$r_i$，则称所用的排序的方法是不稳定的



**2.内排序与外排序**

内排序是在排序整个过程中，待排序的所有记录全部被放置在内存中

外排序是由于排序的记录个数太多，不能同时放置在内存中，整个排序过程需要在内外存之间多次交换数据才能进行



## 2.结构与函数

```c
#define MAXSIZE 1000
typedef struct{
    int r[MAXSIZE + 1];
    int length;
}SqList;
```



```c
//交换L中数组r的下标为i和j的值
void swap(SqList *L, int i, int j){
    int temp = L->r[i];
    L->r[i] = L->r[j];
    L->r[j]	= temp;
}
```



## 3.冒泡排序

冒泡排序是一种交换排序，最基本的思想是两两比较相邻记录的关键字，如果反序则交换，知道没有反序的记录为止

```c
//对顺序表进行冒泡排序
void BubbleSort(SqList *L){
    int i,j;
    for (i = 1; i < L->length; i++){
        for (j = L->length - 1; j >= i; j--){
            if (L->r[j - 1] > L->r[j])
                swap(L, j-1, j);
        }
    }
}
```



冒泡排序优化

```c
//改进
void BubbleSort(SqList *L){
    int i,j;
    /////////
    Status flag = TRUE;
    /////////
    for (i = 1; i < L->length && flag; i++){
        flag = FALSE;
        for (j = L->length - 1; j >= i; j--){
            if (L->r[j - 1] > L->r[j]){
                swap(L, j-1, j);
                flag = TRUE;
            } 
        }
    }
}
```

**总的时间复杂度为O($n^2$)**



## 4.简单选择排序

```c
//对顺序表L作简单选择排序
void SelectSort(SqList *L){
    int i, j, min;
    for (i = 1; i < L->length; i++){
        min = i;								/*当前下标定义为最小值*/
        for (j = i + 1; j <= L->length; j++){
            if (L->r[min] > L->r[j])			/*如果有小于当前最小值的关键字，将此关键字下标赋值给min*/
                min = j;
        }
        if (i != min)							/*若min不等于i，说明找到最小值，交换*/
            swap(L, i, min);
    }
}
```

**时间复杂度为O($n^2$)**

性能上略优于冒泡排序



## 5.直接插入排序

直接插入排序的基本操作是将一个记录插入到已经排好序的有序表中，从而得到一个新的、记录数增1的有序表

```c
//对顺序表L作直接插入排序
void InsertSort(SqList *L){
    int i, j;
    for (i = 2; i <= L->length; i++){
        if (L->r[i] < L->r[i - 1]){				/*将L->r[i]插入有序子表*/
            L->r[0] = L->r[i];					/*设置哨兵*/
            for (j = i - 1; L->r[j] > L->r[0]; j--)
                L->r[j + 1] = L->r[j];			/*记录后移*/
            L->r[j + 1] = L->r[0];				/*插入到正确位置*/
        }
    }
}
```

**时间复杂度为O($n^2$)**

性能上略优于冒泡排序和简单选择排序



## 6.希尔排序

(shell Sort)

**基本有序**：小的关键字基本在前面，大的基本在后面，不大不小的基本在中间

将相距某个”增量“的记录组成一个子序列，这样才能保证在子序列内分别进行直接插入排序后得到的结果是基本有序而不是局部有序



```c
//希尔排序算法
void ShellSort(SqList *L){
    int i, j, k = 0;
    int increment = L->length;
    do{
        increment = increment/3 + 1;					/*增量序列*/
        for (i = increment + 1; i <= L->length){
            if (L->r[i] < L->r[i - increment]){			/*需将L->[i]插入有序增量子表*/
                L->r[0] = L->r[i];						/*暂存在L->r[0]*/
                for (j = i - increment; j > 0 && L->r[0] < L->r[j]; j -= increment)
                    L->r[j + increment] = L->r[j];		/*记录后移，查找插入位置*/
                L->r[j + increment] = L->r[0];			/*插入*/
            }
        }
    }while (increment > 1);
}
```

**增量序列最后一个增量值必须等于1**

时间复杂度O($n^\frac{3}{2}$)



## 7.堆排序

堆是具有下列性质的二叉树：

- 每个结点的值都大于或等于其左右孩子结点的值，称为**大顶堆**
- 或者每个结点的值都小于或等于其左右孩子结点的值，称为**小顶堆**



```c
//对顺序表L进行堆排序
void HeapSort(SqList *L){
    int i;
    for (i = L->length/2; i > 0; i--)					/*构造大顶堆*/
        HeapAdjust(L, i, L->length);
    for (i = L->length; i > 1; i--){					
        swap(L, 1, i);									/*将堆顶记录和当前未经排序子序列最后一记录交换*/
        HeapAdjust(L, 1, i - 1);						/*将L->r[1..i - 1]重新调整为大顶堆*/
    }
}
```



```c
//堆调整
void HeapAdjust(SqList *L, int s, int m){
    int temp, j;
    temp = L->r[s];
    for (j = 2 * s; j <= m; j *= 2){					/*沿关键字较大的孩子结点向下筛选*/
        if (j < m && L->r[j] < L->r[j + 1])
            ++j;										/*j为关键字中较大的记录的下标*/
        if (temp >= L->r[j])
            break;										/*rc应插入在位置s上*/
        L->r[s] = L->r[j];
        s = j;
    }
    L->r[s] = temp;										/*插入*/
}
```



```c
//排序
for (i = L->lenth; i > 1; i--){
    swap(L, 1, i);
    HeapAdjust(L, 1, i - 1);
}
```



**时间复杂度O(nlogn)**

记录的比较是跳跃式进行，所以堆排序是一种不稳定的排序方法

初始构建堆所需要的次数较多，不适合待排序序列个数较少情况



## 8.归并排序

**归并排序（Merging Sort）**

```c
//对顺序表L作归并排序
void MergeSort(SqList *L){
    Msort(L->r, L->r, 1, L->length);
}
```



```c
void MSort(int SR[], int TR1[], int s, int t){
    int m;
    int TR2[MAXSIZE + 1];
    if (s == t){
        TR1[s] = SR[s];
    }
    else{	
        m = (s + t) / 2;					/*将SR[s..t]平分为SR[s..m]和s[m+1..t]*/
        MSort(SR, TR2, s, m);				/*将SR[s..m]归并为有序序列TR2[s..m]*/
        MSort(SR, TR2, m + 1, t);			/*将SR[m+1..t]归并为有序序列TR2[m+1..t]*/
        Merge(SR, TR2, s, m, t);			/*将TR2[s..m]和TR2[m+1..t]归并到TR1[s..m]*/
    }
}
```



```c
//将SR[s..m]和SR[m+1..t]归并到TR[s..m]
void Merge(int SR[], int TR[], int i, int m, int n){
    int j, k, l;
    for (j = m + 1, k = i; i <= m && j <= n; k++){			/*将SR中记录由小到大并入TR*/
        if (SR[i] < SR[J])
            TR[k] = SR[i++];
        else
            TR[k] = SR[j++];
        if (i <= m){
            for (l = 0; l <= m - i; l++)
                TR[k + l] = SR[i + l];						/*将剩余SR[i..m]复制到TR*/
        }
        if (j <= n){
            for (l = 0; l <= n - j; l++)
                TR[k + l] = SR[j + l];						/*将剩余SR[j..n]复制到TR*/
        }
    }
}
```

**时间复杂度O(nlogn)**

归并排序是一种稳定的排序算法，比较占用内存，但效率高且稳定



## 9.快速排序

**快速排序（Quick Sort）**的基本思想是：通过一趟排序将待排记录分割成独立的两部分

其中一部分记录的关键字比另一部分小，则可分别对这两部分记录继续进行排序，以达到整个序列有序的目的



```c
//对顺序表L作快速排序
void QuickSort(SqList *L){
    QSort(L, 1, L->length);
}
```



```c
//对顺序表L中子序列L->r[low..high]作快速排序
void QSort(SqList *L, int low, int high){
    int pivot;
    if (low < high){
        //将L->r[low..high]一分为二，算出枢轴值pivot
        pivot = Partition(L, low, high);
        QSort(L, low, pivot - 1);			/*对低子表递归排序*/
        QSort(L, pivot + 1, high);			/*对高子表递归排序*/
    }
}
```

Patition（）要做的，就是选取当中一个关键字，想尽办法将它放到一个位置

使得它左边的值都比它小，右边的值都比它大，这样的关键词称为枢轴(Pivot)



```c
int Patition(SqList *L, int low, int high){
    int pivotkey;
    pivotkey = L->r[low];				/*用子表的第一个记录作枢轴记录*/
    while (low < high){					/*从表的两端交替地向中间扫描*/
        while (low < high && L->r[low] >= pivotkey)
            high--;
        swap(L, low, high);				/*将比枢轴记录小的记录交换到低端*/
        
        while (low < high && L->r[low] <= pivotkey)
            low++;
        swap(L, low, high);
    }
    return low;							/*返回枢轴所在位置*/
}
```

**时间复杂度O($n^2$)**

由于关键字比较和交换是跳跃进行，因此快速排序是一种不稳定排序



#### **快速排序优化**

##### 1.优化选取枢轴

- 固定选取（原）
- 随机选取
- 三数取中

```c
int pivotkey;

int m = low + (high - low) / 2;
if (L->r[low] > L ->r[high])
    swap(L, low, high);
if (L->r[m] > L ->r[high])
    swap(L, m, high);
if (L->r[low] > L ->r[m])
    swap(L, low, high);
//此时，r[low]已经为整个序列左、中、右三个关键字的中间值

pivokey = L->r[low];
```

- 九数取中



##### 2.优化不必要的交换

==``L->r[0] = pivotkey``==

采用替换而不是交换的方式进行操作

L->r[low] = L->r[high]

```c
int Patition(SqList *L, int low, int high){
    int pivotkey;
    pivotkey = L->r[low];				/*用子表的第一个记录作枢轴记录*/
    L->r[0] = pivotkey
    while (low < high){					/*从表的两端交替地向中间扫描*/
        while (low < high && L->r[low] >= pivotkey)
            high--;
        L->r[low] = L->r[high]			/*采用替换而不是交换的方式进行操作*/
        
        while (low < high && L->r[low] <= pivotkey)
            low++;
        L->r[high] = L->r[low]
    }
    L->r[low] = L->r[0]
    return low;							/*返回枢轴所在位置*/
}
```

##### 3.优化小数组时的排序方案

```c
#define MAX_LENGTH_INSERT_SORT 7
void QSort(SqList *L, int low, int high){
    int pivot;
    if ((high - low) > MAX_LENGTH_INSERT_SORT){
        ......							/*采用快速排序*/
    }
    else
        InsertSort(L);					/*直接用插入排序*/
}
```



##### 4.优化递归操作





## 10.总结对比

|   排序方法   |        平均情况        |      最好情况      |   最坏情况    |     辅助空间      | 稳定性 |
| :----------: | :--------------------: | :----------------: | :-----------: | :---------------: | :----: |
|   冒泡排序   |        O($n^2$)        |       O($n$)       |   O($n^2$)    |       O(1)        |  稳定  |
| 简单选择排序 |        O($n^2$)        |      O($n^2$)      |   O($n^2$)    |       O(1)        |  稳定  |
| 直接插入排序 |        O($n^2$)        |       O($n)$       |   O($n^2$)    |       O(1)        |  稳定  |
|   希尔排序   | O($n\log{n}$)~O($n^2$) | O($n^\frac{3}{2}$) |   O($n^2$)    |       O(1)        | 不稳定 |
|    堆排序    |     O($n\log{n}$)      |   O($n\log{n}$)    | O($n\log{n}$) |       O(1)        | 不稳定 |
|   归并排序   |     O($n\log{n}$)      |   O($n\log{n}$)    | O($n\log{n}$) |       O(n)        |  稳定  |
|   快速排序   |     O($n\log{n}$)      |   O($n\log{n}$)    |   O($n^2$)    | O($\log{n}$)~O(1) | 不稳定 |



- 简单算法：冒泡、简单选择、直接插入
- 改进算法：希尔、堆、归并、快速



从**平均情况**看，最后三种改进算法胜过希尔排序，并远胜于3钟简单算法

从**最好情况**看，冒泡和直接插入排序更胜一筹。如果待排序序列总是基本有序，反而不应该考虑4种复杂的改进算法

从**最坏情况**看，堆排序与归并排序强于快速排序及其他简单排序

从**稳定性**看，归并排序独占鳌头，对非常在乎排序稳定性的应用中，归并排序是个好算法

从**待排序记录的个数**上看，待排序的个数越小，采用简单排序方法就越合适
