``` java
class Solution {
    boolean vis[];
    Map<Integer,List<Integer>> g;
    public boolean isCycle(int V, int[][] edges) {
        
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
                if(bfs(i)) return true;
            }
            
        }
        
        return false;
    }
    public boolean bfs(int i){
        
        
        Queue<int[]> q=new LinkedList<>();
        q.add(new int[]{i,-1});
        vis[i]=true;
        
        while(!q.isEmpty()){
            int pair[]=q.poll();
            int node=pair[0];
            int par=pair[1];
            
            for(int e:g.get(node)){
                if(!vis[e]){
                    q.add(new int[]{e,node});
                    vis[e]=true;
                }
                else{
                    if(e!=par) return true; //if node e is not parent then cycle
                }
            }
        }
        
        return false;
    }
}
```
