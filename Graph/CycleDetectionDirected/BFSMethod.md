For BFS we are using KAHN'S Algorithm (BFS TopoSort)
TC->O(V+E)

```java
class Solution {
    public boolean isCyclic(int V, int[][] edges) {
        // code here
        Map<Integer,List<Integer>> g=new HashMap<>();
        
        for(int i=0;i<V;i++){
            g.put(i,new ArrayList<>());
        }
        
        int indegree[]=new int[V];
        
        for(int a[]:edges){
            g.get(a[0]).add(a[1]);
            
            indegree[a[1]]++;
        }
        
        
        Queue<Integer> q=new LinkedList<>();
        
        for(int i=0;i<V;i++){
            if(indegree[i]==0) q.add(i);
        }
        
        int cnt=0;
        
        while(!q.isEmpty()){
            int node=q.poll();
            cnt++;
            
            for(int e:g.get(node)){
                
                indegree[e]--;
                if(indegree[e]==0) q.add(e);
            }
        }
        
        return cnt!=V;
    }
}
```
