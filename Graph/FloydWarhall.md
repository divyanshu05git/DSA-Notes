Floyd–Warshall uses Dynamic Programming to find the shortest paths between every pair of vertices 
by considering each vertex as an intermediate vertex. 
It maintains a distance matrix dis[i][j], where dis[i][j] represents the shortest distance from vertex i to vertex j
.For every intermediate vertex k, we update dis[i][j] = min(dis[i][j], dis[i][k] + dis[k][j]). 

Time complexity  O(n³).
Space complexity O(n²).

```java
class Solution {
    public void floydWarshall(int[][] dist) {
        // Code here
        int n = dist.length;
       
       
        for(int via=0;via<n;via++){
            for(int i=0;i<n;i++){
                for(int j=0;j<n;j++){
                    if(dist[i][via]==1e8 || dist[via][j]==1e8) continue;
                    dist[i][j]=Math.min(dist[i][j],dist[i][via]+dist[via][j]);
                }
            }
        }
    }
}
```
