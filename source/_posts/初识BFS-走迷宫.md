---
title: 初识BFS---走迷宫
date: 2020-02-29 22:34:06
tags: 算法
---
## BFS
- 全称宽度优先搜索（广度优先搜索）
- 实现过程：
1. 把根节点放到队列的末尾。
2. 每次从队列的头部取出一个元素，查看这个元素所有的下一级元素，把它们放到队列的末尾。并把这个元素记为它下一级元素的前驱。
3. 找到所要找的元素时结束程序。
4. 如果遍历整个树还没有找到，结束程序。
(摘自百度百科)


### 二维：走迷宫
#### [vj题目地址](https://vjudge.net/problem/OpenJ_Bailian-3752)
**题目描述**
> 一个迷宫由R行C列格子组成，有的格子里有障碍物，不能走；有的格子是空地，可以走。
给定一个迷宫，求从左上角走到右下角最少需要走多少步(数据保证一定能走到)。只能在水平方向或垂直方向走，不能斜着走。

**Input**
>第一行是两个整数，Ｒ和Ｃ，代表迷宫的长和宽。（ 1<= R，C <= 40)
>接下来是Ｒ行，每行Ｃ个字符，代表整个迷宫。
>空地格子用'.'表示，有障碍物的格子用'#'表示。
迷宫左上角和右下角都是'.'。


**Output**
>输出从左上角走到右下角至少要经过多少步（即至少要经过多少个空地格子）。计算步数要包括起点和终点。


**Sample Input**
>5 5
>..###
#....
#.#.#
#.#.#
#.#..


**Sample Output**
>9

#### ac代码
这是跟着一个老师学的，然后自己实现了一遍
[b站视频讲解入口](https://www.bilibili.com/video/av41856043?p=2)
```
#include <iostream>
#include <queue>
using namespace std;

int r,c;
char mp[45][45];
int vis[45][45];
int dir[][2]={-1,0,1,0,0,-1,0,1};

typedef struct Node{
    int x,y;
    int step;
}node;

int bfs(int u,int v){
    vis[u][v]=1;
    node tmp,nxt;
    tmp.x=u;
    tmp.y=v;
    tmp.step=1;
    queue<node> q;
    q.push(tmp);
    while(!q.empty()){
        tmp=q.front();
        q.pop();
        for(int i=0;i<4;i++){
            nxt.x=tmp.x+dir[i][0];
            nxt.y=tmp.y+dir[i][1];
            nxt.step=tmp.step+1;
            if (nxt.x<0||nxt.y<0||nxt.x>=r||nxt.y>=c||vis[nxt.x][nxt.y]||mp[nxt.x][nxt.y]=='#') continue;
            if (nxt.x==r-1&&nxt.y==c-1) return nxt.step;
            vis[nxt.x][nxt.y]=1;
            q.push(nxt);
        }
    }
}
```
#### 收获与反思
收获就是广搜终于不是只理解思路而已了，多加了一点点实现哈哈哈哈
反思就是我二维数组没学好，以至于浪费了好多时间一直找不到错误，原来二维数组a[i][j]在设置范围的时候j一定得准确不然就错了。
基础很重要啊，继续练习~~