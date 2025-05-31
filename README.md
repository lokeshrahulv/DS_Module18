# DS_Module18
# Ex26 Prim’s Algorithm

## DATE:
## AIM:
To write a C program to implement Prim's Algorithm for finding Total Cost of tree.

## Algorithm


1. Initialize Constants and Variables
   - Define `infinity = 9999` and `MAX = 20`.  
   - Declare global matrices `G[MAX][MAX]`, `spanning[MAX][MAX]`, and integer `n`.

2. Read Graph Input in `main()`  
   - Read number of vertices `n`.  
   - Input the adjacency matrix `G[i][j]` using `scanf`.

3. Define `prims()` Function
   - Convert `G` to `cost[][]` matrix (replace 0s with infinity).  
   - Initialize arrays: `visited[]`, `distance[]`, and `from[]`.

4. Construct Minimum Spanning Tree
   - Repeat for `n-1` edges:  
     - Find the minimum unvisited vertex.  
     - Add the edge to `spanning[][]`.  
     - Update distances and mark vertex as visited.

5. Output the Result
   - Print the `spanning[][]` matrix and the total cost returned by `prims()`.

## Program:
```
Program to implement Prim's Algorithm
Developed by: LOKESH RAHUL V V
RegisterNumber: 212222100024

#include<stdio.h>
#include<stdlib.h>
 
#define infinity 9999
#define MAX 20
 
int G[MAX][MAX],spanning[MAX][MAX],n;
 
int prims();
 
int main()
{
int i,j,total_cost;
scanf("%d",&n);
for(i=0;i<n;i++)
for(j=0;j<n;j++)
scanf("%d",&G[i][j]);
total_cost=prims();

for(i=0;i<n;i++)
{
for(j=0;j<n;j++)
printf("%d ",spanning[i][j]);
printf("\n");
}
printf("\nTotal cost of spanning tree=%d",total_cost);
return 0;
}
 
int prims()
{
int cost[MAX][MAX];
int u,v,min_distance,distance[MAX],from[MAX];
int visited[MAX],no_of_edges,i,min_cost,j;
//create cost[][] matrix,spanning[][]
for(i=0;i<n;i++)
for(j=0;j<n;j++)
{
if(G[i][j]==0)
cost[i][j]=infinity;
else
cost[i][j]=G[i][j];
spanning[i][j]=0;
}
//initialise visited[],distance[] and from[]
distance[0]=0;
visited[0]=1;
for(i=1;i<n;i++)
{
distance[i]=cost[0][i];
from[i]=0;
visited[i]=0;
}
min_cost=0; //cost of spanning tree
no_of_edges=n-1; //no. of edges to be added
while(no_of_edges>0)
{
//find the vertex at minimum distance from the tree
min_distance=infinity;
for(i=1;i<n;i++)
if(visited[i]==0&&distance[i]<min_distance)
{
v=i;
min_distance=distance[i];
}
u=from[v];
//insert the edge in spanning tree
spanning[u][v]=distance[v];
spanning[v][u]=distance[v];
no_of_edges--;
visited[v]=1;
//updated the distance[] array
for(i=1;i<n;i++)
if(visited[i]==0&&cost[i][v]<distance[i])
{
distance[i]=cost[i][v];
from[i]=v;
}
min_cost=min_cost+cost[u][v];
}
return(min_cost);
}
```

## Output:

![image](https://github.com/user-attachments/assets/29cb3c21-0913-4917-9156-bb943c7ccb31)



## Result:
Thus, the C program to implement Prim's Algorithm for finding Total Cost of tree is implemented successfully.
# Ex27 Kruskal’s Algorithm
## DATE:
## AIM:
To write a C program to implement Kruskal's Algorithm for finding minimum cost

## Algorithm

1. Initialize Variables and Data Structures
   - Set `ne = 1`, `mincost = 0`.  
   - Declare `cost[9][9]` for the adjacency matrix and `parent[9]` for disjoint sets.  
   - Define helper functions: `find(int)` to find root and `uni(int, int)` to union sets.

2. Read Input  
   - Input number of vertices `n`.  
   - Fill `cost[i][j]` matrix using `scanf`.  
   - Replace `0` values with `999` (representing infinity/no edge).

3. Build Minimum Spanning Tree  
   - While `ne < n`:  
     - Find the edge with minimum weight not yet used.  
     - Use `find()` to check if it connects different trees.  
     - If so, use `uni()` to merge sets and include edge in MST.

4. Update Costs and MST Info  
   - Print selected edge and update `mincost`.  
   - Set `cost[a][b]` and `cost[b][a]` to `999` to avoid reselecting.

5. Output Final Result  
   - Print the total cost of the MST using `printf("Minimum cost = %d\n", mincost);`.


## Program:
```
Program to implement Kruskal's Algorithm
Developed by: LOKESH RAHUL V V
RegisterNumber: 212222100024
```
```
    #include <stdio.h>
    #include <stdlib.h>
    int i,j,k,a,b,u,v,n,ne=1;
    int min,mincost=0,cost[9][9],parent[9];
    int find(int);
    int uni(int,int);
    int main()
    {
          scanf("%d",&n);
          for(i=1;i<=n;i++)
     {
     for(j=1;j<=n;j++)
     {
     scanf("%d",&cost[i][j]);
     if(cost[i][j]==0)
     cost[i][j]=999;
     }
     }
         while(ne < n)
     {
     for(i=1,min=999;i<=n;i++)
     {
     for(j=1;j <= n;j++)
     {
     if(cost[i][j] < min)
     {
     min=cost[i][j];
     a=u=i;
     b=v=j;
     }
     }
     }
     u=find(u);
     v=find(v);
     if(uni(u,v))
     {
     printf("%d edge (%d,%d) =%d\n",ne++,a,b,min);
     mincost +=min;
     }
     cost[a][b]=cost[b][a]=999;
     }
     printf("Minimum cost = %d\n",mincost);
     return 0;
       }
    int find(int i)
    {
     while(parent[i])
     i=parent[i];
     return i;
    }
    int uni(int i,int j)
    {
     if(i!=j)
     {
     parent[j]=i;
     return 1;
     }
     return 0;
    }

```

## Output:

![image](https://github.com/user-attachments/assets/12b2ed8b-bc94-495d-b5d3-22eabb5c0e1f)



## Result:
Thus, the C program to implement Kruskal's Algorithm for finding minimum cost is implemented successfully.
# Ex28 Dijkstra’s Algorithm
## DATE:
## AIM:
To write a C Program to implement Dijkstra's Algorithm to find the shortest path

## Algorithm

1. Initialize Constants and Variables  
   - Define `INFINITY = 9999`, `MAX = 10`.  
   - Declare graph matrix `G[MAX][MAX]`, and arrays for `distance`, `visited`, and `pred`.

2. Input Graph and Starting Node  
   - Read number of nodes `n`, then input adjacency matrix `G[i][j]`.  
   - Replace `0` with `INFINITY` to indicate no direct edge.  
   - Read the starting node `u`.

3. Set Up for Dijkstra's Algorithm 
   - Initialize `distance[i]` with `G[u][i]`, set `pred[i] = u`, and mark all nodes unvisited.  
   - Mark the start node as visited and set its distance to 0.

4. Compute Shortest Paths 
   - Repeat for `n-1` nodes:  
     - Select the nearest unvisited node.  
     - Mark it visited and update distances of its unvisited neighbors if a shorter path is found.

5. Display Results
   - For each node (except the start), print the shortest distance from the start and trace the path using `pred[]`.


## Program:
```
Program to implement Dijkstra's Algorithm 
Developed by: LOKESH RAHUL V V
RegisterNumber: 212222100024
```
```
#include<stdio.h>
#define INFINITY 9999
#define MAX 10
 
void dijkstra(int G[MAX][MAX],int n,int startnode);
 
int main()
{
int G[MAX][MAX],i,j,n,u;
scanf("%d",&n);
for(i=0;i<n;i++)
for(j=0;j<n;j++)
scanf("%d",&G[i][j]);
scanf("%d",&u);
dijkstra(G,n,u);
return 0;
}
 
void dijkstra(int G[MAX][MAX],int n,int startnode)
{
 
int cost[MAX][MAX],distance[MAX],pred[MAX];
int visited[MAX],count,mindistance,nextnode,i,j;
//pred[] stores the predecessor of each node
//count gives the number of nodes seen so far
//create the cost matrix
for(i=0;i<n;i++)
for(j=0;j<n;j++)
if(G[i][j]==0)
cost[i][j]=INFINITY;
else
cost[i][j]=G[i][j];
//initialize pred[],distance[] and visited[]
for(i=0;i<n;i++)
{
distance[i]=cost[startnode][i];
pred[i]=startnode;
visited[i]=0;
}
distance[startnode]=0;
visited[startnode]=1;
count=1;
while(count<n-1)
{
mindistance=INFINITY;
//nextnode gives the node at minimum distance
for(i=0;i<n;i++)
if(distance[i]<mindistance&&!visited[i])
{
mindistance=distance[i];
nextnode=i;
}
//check if a better path exists through nextnode
visited[nextnode]=1;
for(i=0;i<n;i++)
if(!visited[i])
if(mindistance+cost[nextnode][i]<distance[i])
{
distance[i]=mindistance+cost[nextnode][i];
pred[i]=nextnode;
}
count++;
}
 
//print the path and distance of each node
for(i=0;i<n;i++)
if(i!=startnode)
{
printf("Distance of node%d=%d\n",i,distance[i]);
printf("Path=%d",i);
j=i;
do
{
j=pred[j];
printf("<-%d",j);
}while(j!=startnode);
}
}

```

## Output:

![image](https://github.com/user-attachments/assets/121d86c2-a203-4174-aa9d-5389b62714ef)



## Result:
Thus, the Program to implement Dijkstra's Algorithm to find the shortest path is implemented successfully.
# Ex29 Travelling Salesman Problem
## DATE:
## AIM:
To write a C Program to implement Travelling Salesman Problem for finding shortest path.
## Algorithm

1. Initialize Global Variables  
   - `a[10][10]`: Cost matrix (travel cost between cities).  
   - `visited[10]`: Flags for visited cities (all initially 0).  
   - `n`: Number of cities, and `cost = 0`: Total minimum cost.

2. Input Data – `get()` Function  
   - Reads number of cities `n` and fills the `a[i][j]` cost matrix.  
   - Initializes all cities as **not visited**.

3. Find Minimum Cost Path – `mincost(city)`  
   - Marks the current city as visited and prints it.  
   - Finds the next city with the **least cost** using `least(city)`.  
   - If all cities are visited, returns to the starting city.  
   - Updates total `cost` and **recursively continues** from the next city.

4. Select Least Cost City – `least(city)`  
   - Checks all unvisited neighbors of the current city.  
   - Picks the city with the **minimum travel cost** and returns it.  
   - Adds the intermediate cost for each decision.

5. Display Result – `put()`  
   - Prints the **total minimum cost** after all cities are visited and returned.

6. Main Function Execution  
   - Calls `get()` → `mincost(0)` → `put()` in sequence.  
   - Begins from city `0` and completes the tour.


## Program:
```
Program to implement Travelling Salesman Problem for finding shortest path
Developed by: LOKESH RAHUL V V
RegisterNumber: 212222100024
```
```
#include<stdio.h>
int a[10][10],visited[10],n,cost=0;

void get()
{
	int i,j;
		scanf("%d",&n);
	for(i=0;i < n;i++)
	{
			for( j=0;j < n;j++)
			scanf("%d",&a[i][j]);
		visited[i]=0;
	}
	}

void mincost(int city)
{
	int ncity;
	int least(int);
	visited[city]=1;	
	printf("%d -->",city+1);
	ncity=least(city);
	if(ncity==999)
	{
		ncity=0;
		printf("%d",ncity+1);
		cost+=a[city][ncity];
		return;
	}
	mincost(ncity);
}

int least(int c)
{
	int i,nc=999;
	int min=999,kmin;
	for(i=0;i < n;i++)
	{
		if((a[c][i]!=0)&&(visited[i]==0))
			if(a[c][i] < min)
			{
				min=a[i][0]+a[c][i];
				kmin=a[c][i];
				nc=i;
			}
	}
	if(min!=999)
		cost+=kmin;
	return nc;
}

void put()
{
	printf("\n\nMinimum cost:%d",cost);
	}

int main()
{
	get();
	mincost(0);
	put();
	return 0;
	}

```

## Output:

![image](https://github.com/user-attachments/assets/cba89abe-c91d-4dd9-9101-0b6508c93555)



## Result:
Thus, the C program to implement Travelling Salesman Problem for finding shortest path is implemented successfully.
# Ex30 Finding Total Cost of Spanning Tree
## DATE:
## AIM:
To write a C Program to implement Prim's Algorithm for finding Total Cost of spanning tree.
## Algorithm

1. Initialize Variables: Define `infinity = 9999`, `MAX = 20`, and declare the adjacency matrix `G[MAX][MAX]`, MST matrix `spanning[MAX][MAX]`, and integer `n`.

2. Input Graph Data: Read the number of vertices `n` and edge weights into `G[i][j]`.

3. Run `prims()` Function:
   - Initialize `cost[][]`, `spanning[][]`, `distance[]`, `from[]`, and `visited[]`.
   - While there are edges left to add to the MST, find the vertex with the smallest `distance[]`, update the MST, and adjust `distance[]` for unvisited vertices.

4. Print MST: After the `prims()` function completes, print the `spanning[][]` matrix representing the minimum spanning tree.

5. Display Total Cost: Output the `min_cost` of the spanning tree, which is the total minimum cost.


## Program:
```
Program to implement Prim's Algorithm for finding Total Cost of spanning tree.
Developed by: LOKESH RAHUL V V
RegisterNumber: 212222100024
```
```
#include<stdio.h>
#include<stdlib.h>
 
#define infinity 9999
#define MAX 20
 
int G[MAX][MAX],spanning[MAX][MAX],n;
 
int prims();
 
int main()
{
int i,j,total_cost;
scanf("%d",&n);
for(i=0;i<n;i++)
for(j=0;j<n;j++)
scanf("%d",&G[i][j]);
total_cost=prims();

for(i=0;i<n;i++)
{
for(j=0;j<n;j++)
printf("%d ",spanning[i][j]);
printf("\n");
}
printf("\nTotal cost of spanning tree=%d",total_cost);
return 0;
}
 
int prims()
{
int cost[MAX][MAX];
int u,v,min_distance,distance[MAX],from[MAX];
int visited[MAX],no_of_edges,i,min_cost,j;
//create cost[][] matrix,spanning[][]
for(i=0;i<n;i++)
for(j=0;j<n;j++)
{
if(G[i][j]==0)
cost[i][j]=infinity;
else
cost[i][j]=G[i][j];
spanning[i][j]=0;
}
//initialise visited[],distance[] and from[]
distance[0]=0;
visited[0]=1;
for(i=1;i<n;i++)
{
distance[i]=cost[0][i];
from[i]=0;
visited[i]=0;
}
min_cost=0; //cost of spanning tree
no_of_edges=n-1; //no. of edges to be added
while(no_of_edges>0)
{
//find the vertex at minimum distance from the tree
min_distance=infinity;
for(i=1;i<n;i++)
if(visited[i]==0&&distance[i]<min_distance)
{
v=i;
min_distance=distance[i];
}
u=from[v];
//insert the edge in spanning tree
spanning[u][v]=distance[v];
spanning[v][u]=distance[v];
no_of_edges--;
visited[v]=1;
//updated the distance[] array
for(i=1;i<n;i++)
if(visited[i]==0&&cost[i][v]<distance[i])
{
distance[i]=cost[i][v];
from[i]=v;
}
min_cost=min_cost+cost[u][v];
}
return(min_cost);
}
```

## Output:

![image](https://github.com/user-attachments/assets/551b82e4-0ef7-413c-91cc-c3d55c6e454d)



## Result:
Thus the C program to implement Prim's Algorithm for finding Total Cost of spanning tree is implemented successfully.
