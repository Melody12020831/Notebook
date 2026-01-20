---
statistics: True
---

# Compiler Principle

!!! info "课程信息"
    - **智云链接**：[🔗]()
    - **授课**：陈明帅
    - **教材**：Modern Compiler Implementation in C (Andrew W.Appel)
    - **PPT**： 📁
    - **作业**：📝
    - **我的笔记**：[📝](Chapter1.md)
    - **历年题**：
    - **复习资料**：

!!! note "学习建议"
    1. 平时作业要认真做

    2. 编译原理的实验不难，但代码量大，需要投入很多时间，且 lab 关联性不小，经常需要前后照应。因为实验文档已经比较完善，所以可以尝试集中一段时间写一口气写完整套实验

    3. 编译原理的大题题型相对固定，可多参考历年卷提炼考点。需要注意 22 年之前用的是龙书，我们目前用的虎书，考点有差别。注意最后的垃圾回收、面向对象、循环优化三章也是会考的，具体考察程度可能每年不同，需要询问老师助教。

    4. 期末题量不小，不一定能做完，故建议大家考前动手多做些大题，提高大题熟练度以免考场卡壳浪费时间。建议简单的题和难的题都应该动手，而不是看一眼觉得会了就不做了。

    5. 陈老师的期中考历年卷可以在 98 上找到，题型基本不变，考前熟悉一下题型即可。

    6. 参考笔记：https://compiler-note-7908cb.pages.zjusct.io/CP2/

    7. [咸鱼暄](https://space.bilibili.com/18777618/channel/collectiondetail?sid=288316&ctype=0)作为整体知识的了解，[国防科大](https://www.bilibili.com/video/BV11t411V74n/)作为前端细节以及部分后端细节的掌握，[CS143](https://www.bilibili.com/video/BV17K4y147Bz/)作为剩下后端基础部分的掌握

    8. 以下内容推荐来源(https://www.cc98.org/topic/5641876)
    
    (2)Lexical Analysis 推荐资源：咸鱼暄、国防科大、CS143。
    
    (3)Parsing 推荐资源：国防科大。
    
    (4) Abstract Syntax & 5 Semantic Analysis 推荐资源：CS143。 
    
    (6) Activation Records 推荐资源：国防科大，CS143。
    
    (7) Translation to Intermediate Code & Basic Blocks and Traces & 9 Instruction Selection 推荐资源：@泽林道人（三章），国防科大(仅对基本块划分算法有用)，CS143(仅对基本块划分算法有用)。
    
    (10) Liveness Analysis 推荐资源：CS143、国防科大。

    (11) Register Allocation 推荐资源：CS143。

    (13) Garbage Collection 推荐资源：CS143。

    (18) Loop Optimiztions 推荐资源：CS143，国防科大。

    9. [编译原理推荐实验文档(北大)](https://pku-minic.github.io/online-doc/#/)

    10. 理论课：看cms智云。cms对算法流程的讲解还是比较清晰的，看完之后，一定要自己独立的在纸上画一遍

    11. 实验: 尽量早点开始，如果可能的话，在春学期就做完。可以参考南大编译原理自学。手搓的时候还挺有成就感的。然后因为感觉寄存器分配实在太coooool所以就写bonus3，从基本块划分一直实现到寄存器分配(包括precolored寄存器,spill后重新建图, 以及RISC-V调用规范)。

    12. 