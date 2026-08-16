``` java

class Solution {
    boolean vis[];
    Map<Integer,List<Integer>> g;
    public boolean isCycle(int V, int[][] edges) {
        // Code here
        vis=new boolean[V];
        g=new HashMap<>();
        for(int i=0;i<V;i++){
            g.put(i,new ArrayList<>());
        }
        
        for(int e[]:edges){
            int u=e[0];
            int v=e[1];
            
            g.get(u).add(v);
            g.get(v).add(u);
        }
        
        for(int i=0;i<V;i++){
            if(!vis[i]){
                if(dfs(i,-1)) return true;
            }
            
        }
        
        return false;
    }
    public boolean dfs(int node,int par){
        vis[node]=true;
        
        for(int e:g.get(node)){
            if(!vis[e]){
                if(dfs(e,node)) return true;
            }
            else{
                if(e!=par) return true;
            }
        }
        
        return false;
    }
}
```
