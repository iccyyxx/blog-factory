---
title: BFS--Dungeon Master
date: 2020-03-01 15:14:54
tags: 算法
---
## 三维：Dungeon Master
### [vj题目入口](https://vjudge.net/problem/POJ-2251)
**题目描述**
>You are trapped in a 3D dungeon and need to find the quickest way out! The dungeon is composed of unit cubes which may or may not be filled with rock. It takes one minute to move one unit north, south, east, west, up or down. You cannot move diagonally and the maze is surrounded by solid rock on all sides.
>Is an escape possible? If yes, how long will it take?


**Input**
>The input consists of a number of dungeons. Each dungeon description starts with a line containing three integers L, R and C (all limited to 30 in size).
L is the number of levels making up the dungeon.
R and C are the number of rows and columns making up the plan of each level.
Then there will follow L blocks of R lines each containing C characters. Each character describes one cell of the dungeon. A cell full of rock is indicated by a '#' and empty cells are represented by a '.'. Your starting position is indicated by 'S' and the exit by the letter 'E'. There's a single blank line after each level. Input is terminated by three zeroes for L, R and C.

**Output**
>Each maze generates one line of output. If it is possible to reach the exit, print a line of the form
Escaped in x minute(s).
where x is replaced by the shortest time it takes to escape.
If it is not possible to escape, print the line
Trapped!

**Sample Input**
>3 4 5
S....
.###.
.##..
###.#
#####
#####
##.##
##...
#####
#####
#.###
####E
1 3 3
S##
#E#
###
0 0 0

**Sample Output**
>Escaped in 11 minute(s).
Trapped!

### ac代码
```
#include <iostream>
#include <queue>
using namespace std;
int l,r,rr;
char mp[40][40][40];
typedef struct Node{
    int a;
    int b;
    int c;
    int step;
}node;
int dir[7][3]={
    1,0,0,
    -1,0,0,
    0,1,0,
    0,-1,0,
    0,0,1,
    0,0,-1,
};
int bfs(int i,int j,int k) {
    int vis[40][40][40]={0};
    node t1, t2;
    t1.a = i;
    t1.b = j;
    t1.c = k;
    t1.step=0;
    queue<node> q;
    while (!q.empty()) {q.pop();}
    q.push(t1);
    while (!q.empty()) {
        t1 = q.front();
        q.pop();
        vis[t1.a][t1.b][t1.c] = 1;
        for (int x = 0; x < 6; x++) {
            t2.a = t1.a + dir[x][0];
            t2.b = t1.b + dir[x][1];
            t2.c = t1.c + dir[x][2];
            if (t2.a < 0 || t2.b < 0 || t2.c < 0 || t2.a >= l || t2.b >= r || t2.c >= rr || vis[t2.a][t2.b][t2.c] ||
                mp[t2.a][t2.b][t2.c] == '#')
                {continue;}
            t2.step=t1.step+1;
            if (mp[t2.a][t2.b][t2.c] == 'E') {
                cout << "Escaped in "<<t2.step <<" minute(s).\n";
                return 0;
            }
            vis[t2.a][t2.b][t2.c] = 1;
            q.push(t2);
        }
    }
    cout<<"Trapped!\n";
    return 0;
}

int main(){
    while( cin >> l >> r >> rr){
        if (l==0&&r==0&&rr==0) {return 0;}
    for (int i=0;i<l;i++){
        for (int j=0;j<r;j++){
            for (int k=0;k<rr;k++)
                cin >> mp[i][j][k];
        }
    }
    for (int i=0;i<l;i++){
        for (int j=0;j<r;j++){
            for (int k=0;k<rr;k++)
                {
                    if (mp[i][j][k]=='S') {
                    bfs(i,j,k);
                    }
                }
        }
    }}
    return 0;
}
```
### 收获与反思
- 似乎广搜简单的题目没有自己想象中的那么难，一个类型的题目做法其实大同小异，思路清晰没什么大问题
- 做题的时候因为太高兴过了样例没检查结果就PE了，找了好久才发现分钟数前后需要空格
- 这种多输入的题目记得标记要重置，队列要清空！