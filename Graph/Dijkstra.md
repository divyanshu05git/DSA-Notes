Dijkstra algo is used to find shortest path for both directed and undirected weighted graph.

1->Weighted Undirected
```java
class Solution {
    public ArrayList<Integer>  dijkstra(int V, int[][] edges, int src) {
        // code here
        
        Map<Integer,List<int[]>> g=new HashMap<>();
        for(int i=0;i<V;i++) g.put(i,new ArrayList<>());
        for(int ar[]:edges){
            int u=ar[0];
            int v=ar[1];
            int wt=ar[2];
            
            g.get(u).add(new int[]{v,wt});
            g.get(v).add(new int[]{u,wt});
        }
        
        int dis[]=new int[V];
        Arrays.fill(dis,Integer.MAX_VALUE);
        
        PriorityQueue<int[]> pq=new PriorityQueue<>((a,b)->a[1]-b[1]);
        pq.add(new int[]{src,0});
        dis[src]=0;
        
        while(!pq.isEmpty()){
            int peek[]=pq.poll();
            int node=peek[0];
            int dist=peek[1];
            
            if(dist!=dis[node]) continue;
            
            for(int a[]:g.get(node)){
                int nxtNode=a[0];
                int wt=a[1];
                
                if(dis[nxtNode]>dist+wt){
                    dis[nxtNode]=dist+wt;
                    pq.add(new int[]{nxtNode,dis[nxtNode]});
                }
            }
        }
        
        ArrayList<Integer> res=new ArrayList<>();
        for(int e:dis) res.add(e);
        
        return res;
    }
}
```

2->Weighted Directed(Cyclic and Acyclic Both)
```java
class Solution {
    public ArrayList<Integer> shortestPath(int V, int[][] edges) {
        // Code here
        Map<Integer,List<int[]>> g=new HashMap<>();
        
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
        
        PriorityQueue<int[]> pq=new PriorityQueue<>((a,b)->{
            return a[1]-b[1];
        });
        dis[0]=0;
        pq.add(new int[]{0,0});
        
        while(!pq.isEmpty()){
            int pair[]=pq.poll();
            int node=pair[0];
            int currDis=pair[1];
            
            for(int arr[]:g.get(node)){
                int nxtNode=arr[0];
                int wt=arr[1];
                
                if(dis[nxtNode]==-1 || dis[nxtNode]>currDis+wt){
                    dis[nxtNode]=currDis+wt;
                    pq.add(new int[]{nxtNode,dis[nxtNode]});
                }
            }
        }
        
        ArrayList<Integer> ls=new ArrayList<>();
        for(int i=0;i<V;i++) ls.add(dis[i]);
        
        return ls;
    }
}
```
