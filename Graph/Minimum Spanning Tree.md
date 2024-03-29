## Minimum Spanning Tree
Given a weighted, undirected and connected graph of V vertices and E edges. The task 

is to find the sum of weights of the edges of the Minimum Spanning Tree.

## Example 

```bash
Input:
3 3
0 1 5
1 2 3
0 2 1
```
![image](https://user-images.githubusercontent.com/94613732/204126158-433e516a-7314-4643-8836-dfe7a708d86e.png)

```
Output:
4
Explanation:
```
![image](https://user-images.githubusercontent.com/94613732/204126164-c3645a7a-4a47-42ea-add1-355d19980269.png)

```

The Spanning Tree resulting in a weight
of 4 is shown above.

```

## Solution

```python
import sys
class Solution:
        
    def spanningTree(self, V, graph):
        
        
        weight = [sys.maxsize for i in range(V)]
        visited = [False for i in range(V)]
        
        weight[0] = 0
        finalAns = 0

        for i in range(V) :

            minVertex = -1

            for j in range(V) :

                if visited[j] == False and (minVertex==-1 or weight[minVertex]>weight[j]) :

                    minVertex = j

            visited[minVertex] = True

            finalAns = finalAns+weight[minVertex]

            for ele,w in adj[minVertex] :

                if visited[ele] == False and weight[ele]>w :

                    weight[ele] = w

        return finalAns
 ```
#### Complexity
```bash
Time Complexity :
Space Complexity : 
```
## Geeksforgeeks
[Minimum Spanning Tree](https://practice.geeksforgeeks.org/problems/minimum-spanning-tree/1?page=1&category[]=Graph&sortBy=submissions)
