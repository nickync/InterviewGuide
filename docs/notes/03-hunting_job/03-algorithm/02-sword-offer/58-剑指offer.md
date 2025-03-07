---
layout:  post
category:  algorithm
title:  No58、对称的二叉树
tagline:  by 阿秀
tags:
    - 原创
    - 剑指offer
    - 数据结构与算法
    - 算法
    - 社招
    - 校招
    - 阿秀
excerpt: No58、对称的二叉树
comment: false
---

<h1 align="center">带你快速刷完67道剑指offer</h1>

<div align="center">
  <a href="/notes/05-xiustar/01-xiustar_reading_guide/01-introduce.html#阿秀组建了一个校招学习圈子">
      <img src="https://axiu-image-bed.oss-cn-shanghai.aliyuncs.com/img/202205222116157.png">
  </a></div>


> 如果你想在校招中顺利拿到更好的offer，阿秀建议你多看看<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[前人的经验](/notes/05-xiustar/01-xiustar_reading_guide/01-introduce.md)</font> ，比如<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[准备](/notes/05-xiustar/02-campus_prepare/02-01-校招重要时间点科普.md)</font> 、<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[简历](/notes/05-xiustar/03-resume/01-00-简历开篇词.md)</font> 、<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[实习](/notes/05-xiustar/04-school_practice/20220320-从公司角度来看，为什么要招实习生.md)</font> 、<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[上岸总结](/notes/05-xiustar/05-campus_recruitment/2020-12-16-双非渣硕的秋招之路总结（已拿抖音研发岗SP）.md)</font> 、<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[offer选择](/notes/05-xiustar/06-offer/01-offer_choose.md)</font> 、<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[也欢迎来一起参加秋招打卡活动](/notes/05-xiustar/01-xiustar_reading_guide/01-introduce.html#阿秀组建了一个校招学习圈子)</font> 等；如果你是计算机小白，学习/转行/校招路上感到迷茫或者需要帮助，可以<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[点此联系阿秀](/notes/08-other/02-question.md#_4、阿秀-如何才能联系到你)</font>；免费分享阿秀个人学习计算机以来的收集到的好资源，<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[点此白嫖](/notes/07-resources/01-free/01-introduce.md)</font>；如果你需要《阿秀的学习笔记》网站中求职相关知识点的**PDF版本**的话，可以<font style="font-weight:bold; color:#4169E1;text-decoration:underline;">[点此下载](/notes/08-other/02-question.md#_5、如何下载阿秀的学习笔记内容pdf版本)</font> 

## **No58、对称的二叉树**

 <font style="font-weight:normal; color:#4169E1;text-decoration:underline;" target="_blank">[牛客网原题链接](https://www.nowcoder.com/practice/ff05d44dfdb04e1d83bdbdab320efbcb?tpId=13&&tqId=11211&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)</font>

### **题目描述**

请实现一个函数，用来判断一棵二叉树是不是对称的。注意，如果一个二叉树同此二叉树的镜像是同样的，定义其为对称的。 

### **示例1**

**输入**

~~~
{8,6,6,5,7,7,5}
~~~
**返回值**

~~~
true
~~~
**示例2**

**输入**

~~~
{8,6,9,5,7,7,5}
~~~
**返回值**

~~~
false
~~~



### **1、递归法比较好做，也很方便**

~~~cpp
bool isEqual(TreeNode*node1,TreeNode*node2){
    if(node1==nullptr && node2 ==nullptr)  return true;
    if(node1 ==nullptr || node2==nullptr) return false;//减少逻辑判断
    if(node1->val == node2->val) {
        return isEqual(node1->left,node2->right) && isEqual(node1->right,node2->left);//注意这里是右左，左右来进行判断

    }else
        return false;
}
bool isSymmetrical(TreeNode* pRoot) {
    if(pRoot==nullptr) return true;//这里是返回true的
    return isEqual(pRoot->left,pRoot->right);
}
~~~



### **二刷：**

### **1、对称 是指 8 6 6 5 7 7 5这样的对称，我的左子树要跟你的右子树一样才叫对称**

运行时间：2ms 占用内存：380k

~~~cpp
bool isEqual(TreeNode*node1, TreeNode*node2){
    if(node1 == nullptr && node2 == nullptr) return true;
    if(node1 == nullptr || node2 == nullptr) return false;
    if(node1->val != node2->val) return false;

    return isEqual(node1->left, node2->right) && isEqual(node1->right, node2->left);
}

bool isSymmetrical(TreeNode* pRoot)
{
    if(pRoot == nullptr) return true;
    return isEqual(pRoot->left, pRoot->right);
}
~~~

<p id = "对称的二叉树"></p>

