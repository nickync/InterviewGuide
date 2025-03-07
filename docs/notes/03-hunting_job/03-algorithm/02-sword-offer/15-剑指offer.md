---
layout:  post
category:  algorithm
title:  No15、反转链表
tagline:  by 阿秀
tags:
    - 原创
    - 剑指offer
    - 数据结构与算法
    - 算法
    - 社招
    - 校招
    - 阿秀
excerpt: No15、反转链表
comment: false
---

<h1 align="center">带你快速刷完67道剑指offer</h1>

<div align="center">
  <a href="/notes/05-xiustar/01-xiustar_reading_guide/01-introduce.html#阿秀组建了一个校招学习圈子">
      <img src="https://axiu-image-bed.oss-cn-shanghai.aliyuncs.com/img/202205222116157.png">
  </a></div>


> 如果你想在校招中顺利拿到更好的offer，阿秀建议你多看看<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[前人的经验](/notes/05-xiustar/01-xiustar_reading_guide/01-introduce.md)</font> ，比如<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[准备](/notes/05-xiustar/02-campus_prepare/02-01-校招重要时间点科普.md)</font> 、<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[简历](/notes/05-xiustar/03-resume/01-00-简历开篇词.md)</font> 、<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[实习](/notes/05-xiustar/04-school_practice/20220320-从公司角度来看，为什么要招实习生.md)</font> 、<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[上岸总结](/notes/05-xiustar/05-campus_recruitment/2020-12-16-双非渣硕的秋招之路总结（已拿抖音研发岗SP）.md)</font> 、<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[offer选择](/notes/05-xiustar/06-offer/01-offer_choose.md)</font> 、<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[也欢迎来一起参加秋招打卡活动](/notes/05-xiustar/01-xiustar_reading_guide/01-introduce.html#阿秀组建了一个校招学习圈子)</font> 等；如果你是计算机小白，学习/转行/校招路上感到迷茫或者需要帮助，可以<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[点此联系阿秀](/notes/08-other/02-question.md#_4、阿秀-如何才能联系到你)</font>；免费分享阿秀个人学习计算机以来的收集到的好资源，<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[点此白嫖](/notes/07-resources/01-free/01-introduce.md)</font>；如果你需要《阿秀的学习笔记》网站中求职相关知识点的**PDF版本**的话，可以<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[点此下载](/notes/08-other/02-question.md#_5、如何下载阿秀的学习笔记内容pdf版本)</font> 




## **No15、反转链表**

<font style="font-weight:normal; color:#4169E1;text-decoration:underline;" target="_blank">[牛客网原题链接](https://www.nowcoder.com/practice/75e878df47f24fdc9dc3e400ec6058ca?tpId=13&&tqId=11168&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)</font>

### **题目描述**

 输入一个链表，反转链表后，输出新链表的表头。 

### **示例1**

**输入**

```
{1,2,3}
```

**返回值**

```
{3,2,1}
```

很好的解答

https://blog.csdn.net/qq_42351880/article/details/88637387

### **1、头插法 很经典的做法啊**

~~~cpp
struct ListNode {
	int val;
	struct ListNode* next;
	ListNode(int x) :
		val(x), next(NULL) {
	}
}; 

ListNode* ReverseList(ListNode* pHead) {

	struct ListNode* Head = NULL;
	struct ListNode* node = (ListNode*)malloc(sizeof(struct ListNode));

	while (pHead != nullptr) {
		node = pHead;
		pHead = pHead->next;

		node->next = Head;
		Head = node;
	}
	return Head;
}

void test02()
{
	ListNode* head = (ListNode*)malloc(sizeof(ListNode));
	head->val = 1;

	ListNode* node1 = (ListNode*)malloc(sizeof(ListNode));
	node1->val = 2;

	ListNode* node2 = (ListNode*)malloc(sizeof(ListNode));
	node2->val = 3;

	ListNode* node3 = (ListNode*)malloc(sizeof(ListNode));
	node3->val = 4;

	head->next = node1;
	node1->next = node2;
	node2->next = node3;
	node3->next = nullptr;

	auto node = ReverseList(head);
	while(node!=nullptr){
	
		cout << node->val << endl;
		node = node->next;
	}
	}
~~~



### **2、第二种方法，借助三个结点进行不断更替**

~~~cpp
ListNode* ReverseList(ListNode* pHead) {

	struct ListNode* node0 = NULL;
	struct ListNode* node1 = (ListNode*)malloc(sizeof(struct ListNode));
	struct ListNode* node2 = (ListNode*)malloc(sizeof(struct ListNode));
	node1 = pHead;
	node2 = pHead->next;
	while (node1 != nullptr) {
		node1->next = node0;

		node0 = node1;
		node1 = node2;
		if (node2!= nullptr) {
			node2 = node2 -> next;
		}
	}
	return node0;
}
~~~



### **二刷：**

### **1、头插法来做，将元素开辟在栈上，这样会避免内存泄露**

运行时间：3ms  占用内存：364k

~~~cpp
ListNode* ReverseList(ListNode* pHead) {

	// 头插法
	if (pHead == nullptr || pHead->next == nullptr) return pHead;
	ListNode dummyNode = ListNode(0);
	ListNode* pre = &(dummyNode);
	pre->next = pHead;
	ListNode* cur = pHead->next;
	pHead->next = nullptr;
	//pre = cur;
	ListNode* temp = nullptr;
	while (cur != nullptr) {
		temp = cur;
		cur = cur->next;
		temp->next = pre->next;
		pre->next = temp;
	}
	return dummyNode.next;

}
~~~



### **2、借助三个节点来进行迭代即可**

运行时间：3ms  占用内存：504k

~~~cpp
    ListNode* ReverseList(ListNode* pHead) {


	    if (pHead == nullptr || pHead->next == nullptr) return pHead;
	    ListNode * pre = nullptr,*cur = pHead,*after = pHead->next;
        while(cur != nullptr){//建议画个图看看就知道了
            cur->next = pre;
            pre = cur;
            cur = after;
            if(after != nullptr)
                after = after->next;
        }
        
        return pre;
    }
~~~

<p id = "反转链表"></p>

