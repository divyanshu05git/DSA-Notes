```java
class Solution {
    List<List<Integer>> ls;
    int disc[];
    int low[];
    boolean vis[];
    int timer;
    Map<Integer,List<Integer>> g;
    public List<List<Integer>> criticalConnections(int n, List<List<Integer>> connections) {
        g=new HashMap<>();
        ls=new ArrayList<>();

        disc=new int[n];
        low=new int[n];
        vis=new boolean[n];

        for(int i=0;i<n;i++){
            disc[i]=-1;
            low[i]=-1;

            g.put(i,new ArrayList<>());
        }

        for(List<Integer> edge:connections){
            int u=edge.get(0);
            int v=edge.get(1);

            g.get(u).add(v);
            g.get(v).add(u);
        }

        timer=0;
        for(int i=0;i<n;i++){
            if(!vis[i]) dfs(i,-1);
        }

        return ls;
    }
    public void dfs(int node,int par){
        vis[node]=true;
        disc[node]=low[node]=timer++;

        for(int e:g.get(node)){
            if(e==par) continue;

            if(!vis[e]){
                dfs(e,node);

                low[node]=Math.min(low[node],low[e]);
                if(low[e]>disc[node]){
                    List<Integer> temp=new ArrayList<>();
                    temp.add(node);
                    temp.add(e);
                    ls.add(new ArrayList<>(temp));
                }
            }
            else{
                low[node]=Math.min(low[node],disc[e]);
            }
        }

        return ;
    }

}
```
