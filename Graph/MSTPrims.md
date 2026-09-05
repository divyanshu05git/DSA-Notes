Time: O(E * logV)
Space: O(V+E)
```java
class Solution {
    public int spanningTree(int V, int[][] edges) {
        // code here
        Map<Integer,List<int[]>> g=new HashMap<>();
        for(int i=0;i<V;i++){
            g.put(i,new ArrayList<>());
        }
        
        for(int a[]:edges){
            int u=a[0];
            int v=a[1];
            int wt=a[2];
            
            g.get(u).add(new int[]{v,wt});
            g.get(v).add(new int[]{u,wt});
        }
        
        boolean vis[]=new boolean[V];
        
        //wt,node
        PriorityQueue<int[]> pq=new PriorityQueue<>((a,b)->{
            return a[0]-b[0];
        });
        pq.add(new int[]{0,0});
        
        int mst=0;
        while(!pq.isEmpty()){
            int a[]=pq.poll();
            int node=a[1];
            int wt=a[0];
            
            if(vis[node]) continue;
            
            vis[node]=true;
            mst+=wt;
            
            for(int e[]:g.get(node)){
                int newNode=e[0];
                int newWt=e[1];
                
                if(!vis[newNode]) pq.add(new int[]{newWt,newNode});
            }
            
        }
        
        return mst;
    }
}

```
