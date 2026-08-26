Bellman-Ford is a Single Source Shortest Path algorithm.
It finds the shortest distance from one source to all vertices.
Unlike Dijkstra, it can handle negative edge weights and can detect negative-weight cycles.

Time Complexity:  O(V × E)
Space complexity: O(V)

```java
class Solution {
    public ArrayList<Integer> bellmanFord(int V, int[][] edges, int src) {
        // code here
        int INF=100000000;
        int dis[]=new int[V];
        Arrays.fill(dis,INF);
        
        dis[src]=0;
        
        //relaxing all edges
        for(int i=0;i<V-1;i++){
            for(int a[]:edges){
                int u=a[0];
                int v=a[1];
                int wt=a[2];
                
                //check if node u unreachable or not first
                if(dis[u]!=INF && dis[v]>dis[u]+wt){
                    dis[v]=dis[u]+wt;
                }
            }
        }
        
        //check for negative weight cycle
        for(int a[]:edges){
            int u=a[0];
            int v=a[1];
            int wt=a[2];

            if(dis[u]!=INF && dis[v]>dis[u]+wt) {
                ArrayList<Integer> ls=new ArrayList<>();
                ls.add(-1);
                
                return ls;
            }
        }
        
        ArrayList<Integer> ls=new ArrayList<>();
        for(int e:dis) ls.add(e);
        
        return ls;
    }
}

```
