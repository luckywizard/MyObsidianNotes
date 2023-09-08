


## 盲搜类算法：
### 1. BFS算法：
**广度优先算法（Breadth First Search  -BFS）**

![[Pasted image 20221204145837.png]]
![[Pasted image 20221204145914.png]]


### 2. DFS算法:  
**深度优先算法（Depth First Search  -DFS）**
![[Pasted image 20221204150016.png]]

![[Pasted image 20221204150038.png]]


### 3. BFS 和 DFS 的比较
 ![[Pasted image 20221204150211.png]]

BFS:  能进行逐层扫描遍历，__能够准确找到最短路径__，计算量相对较大。应用于完整性、最优性的案例

DFS:  在一个分支中快速搜索，有可能得到解，但 __不能保证是最优解__ 。应用于需要深入钻取的案例，比如迷宫等


## A-Star算法：
路径规划导航方面
![[Pasted image 20221204150928.png]]

A-Star 算法引入了路径成本F的概念
![[Pasted image 20221204151052.png]]

选F最小的路径

![[Pasted image 20221204155419.png]]
















