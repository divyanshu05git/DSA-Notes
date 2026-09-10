
```java
class Solution {
    Map<Integer,List<Integer>> g;
    ArrayList<Integer> ls;
    boolean vis[];
    Stack<Integer> st;
    public ArrayList<Integer> topoSort(int V, int[][] edges) {
        // code here
        ls=new ArrayList<>();
        
        g=new HashMap<>();
        vis=new boolean[V];
        
        for(int i=0;i<V;i++){
            g.put(i,new ArrayList<>());
        }
        
        for(int a[]:edges){
            int u=a[0];
            int v=a[1];
            
            g.get(u).add(v);

        }
        st=new Stack<>();
        
        for(int i=0;i<V;i++){
            if(vis[i]) continue;
            dfs(i);
        }
        
        while(!st.isEmpty()) ls.add(st.pop());
        
        
        return ls;
    }
    public void dfs(int node){
        vis[node]=true;
        
        for(int e:g.get(node)){
            if(vis[e]) continue;
            dfs(e);
        }
        
        st.push(node);
    }
}
```
