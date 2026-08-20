```java
class Solution {
    Map<Integer,List<Integer>> g;
    int indegree[];
    ArrayList<Integer> ls;
    boolean vis[];
    public ArrayList<Integer> topoSort(int V, int[][] edges) {
        // code here
        ls=new ArrayList<>();
        
        indegree=new int[V];
        g=new HashMap<>();
        vis=new boolean[V];
        
        for(int i=0;i<V;i++){
            g.put(i,new ArrayList<>());
        }
        
        for(int a[]:edges){
            int u=a[0];
            int v=a[1];
            
            
            g.get(u).add(v);
            
            indegree[v]++;

        }
        
        for(int i=0;i<V;i++){
            if(vis[i]) continue;
            if(indegree[i]==0) dfs(i);
        }
        
        
        return ls;
    }
    public void dfs(int node){
        ls.add(node);
        vis[node]=true;
        
        for(int e:g.get(node)){
            if(vis[e]) continue;
            
            indegree[e]--;
            if(indegree[e]==0) dfs(e);
        }
    }
}
```
