TC-> (V+E)
```java
class Solution {
    Map<Integer,List<Integer>> g;
    boolean vis[];
    boolean pathVis[];
    public boolean isCyclic(int V, int[][] edges) {
        // code here
        g=new HashMap<>();
        vis=new boolean[V];
        pathVis=new boolean[V];
        
        for(int i=0;i<V;i++) g.put(i,new ArrayList<>());
        
        for(int a[]:edges){
            int u=a[0];
            int v=a[1];
            
            g.get(u).add(v);
        }
        
        for(int i=0;i<V;i++){
            if(!vis[i]){
                if(dfs(i)==true) return true;
            }
        }
        
        return false;
    }
    public boolean dfs(int node){
        vis[node]=true;
        pathVis[node]=true;
        
        for(int e:g.get(node)){
            if(!vis[e]){
                if(dfs(e)==true) return true;
            }
            else{
                if(pathVis[e]) return true;
            }
        }
        
        pathVis[node]=false;
        return false;
    }
    
}
```
