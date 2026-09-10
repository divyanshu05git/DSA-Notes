---------------------
Build graph    ->   O(V)
Process edges   ->  O(E)
Find indegree 0  -> O(V)
Kahn's BFS       -> O(V + E)
Total           ->  O(V + E)
```java
class Solution {
    public ArrayList<Integer> topoSort(int V, int[][] edges) {
        // code here
        ArrayList<Integer> ls=new ArrayList<>();
        
        int indegree[]=new int[V];
        Map<Integer,List<Integer>> g=new HashMap<>();
        
        for(int i=0;i<V;i++){
            g.put(i,new ArrayList<>());
        }
        
        for(int a[]:edges){
            int u=a[0];
            int v=a[1];
            
            g.get(u).add(v);
            indegree[v]++;

        }
        
        
        Queue<Integer> q=new LinkedList<>();
        for(int i=0;i<V;i++){
            if(indegree[i]==0) q.add(i);
        }
        
        while(!q.isEmpty()){
            int node=q.poll();
            ls.add(node);
            
            for(int e:g.get(node)){
                indegree[e]--;
                if(indegree[e]==0) q.add(e);
            }
            
        }
        
        return ls;
    }
}
```
