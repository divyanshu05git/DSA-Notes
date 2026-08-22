We havent done DIJIKSTRA as it is confirmed that graph is acyclic
So instead we used topological sort

TC -> O(V+E)

```java
class Solution {
    Stack<Integer> st;
    boolean vis[];
    Map<Integer,List<int[]>> g;
    public ArrayList<Integer> shortestPath(int V, int[][] edges) {
        // Code here
        g=new HashMap<>();
        
        for(int i=0;i<V;i++){
            g.put(i,new ArrayList<>());
        }
        
        for(int a[]:edges){
            int u=a[0];
            int v=a[1];
            int d=a[2];
            
            g.get(u).add(new int[]{v,d});
        }
        
        int dis[]=new int[V];
        Arrays.fill(dis,-1);
        
        vis=new boolean[V];
        st=new Stack<>();
        dfs(0);
        
        dis[0]=0;
        while(!st.isEmpty()){
            int node=st.pop();
            
            for(int a[]:g.get(node)){
                int u=a[0];
                int wt=a[1];
                
                if(dis[u]==-1 || dis[u]>dis[node]+wt){
                    dis[u]=dis[node]+wt;
                }
            }
        }
        
        ArrayList<Integer> ls=new ArrayList<>();
        for(int e:dis) ls.add(e);
        
        return ls;
        
    }
    public void dfs(int node){
        vis[node]=true;
        
        for(int a[]:g.get(node)){
            int nxtNode=a[0];
            if(vis[nxtNode]) continue;
            
            dfs(nxtNode);
        }
        
        st.push(node);
    }
}
```
