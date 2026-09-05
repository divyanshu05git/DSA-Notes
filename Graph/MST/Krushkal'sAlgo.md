Kruskal's Algorithm

1. Sort edges by weight
2. Initialize DSU
3. For every edge:
      if find(u) != find(v):
          add edge to MST
          union(u, v)

TC:
Sorting     → O(E log E)
DSU         → O(E α(V))
Total       → O(E log E)

SC → O(V)

DSU:
find  → O(α(V)) amortized
union → O(α(V)) amortized

```java
class Solution {
    class DSU{
        int parent[];
        int size[];
        
        public DSU(int n){
            parent=new int[n];
            size=new int[n];
            
            for(int i=0;i<n;i++){
                parent[i]=i;
                size[i]=1;
            }
        }
        
        public int find(int u){
            if(parent[u]==u) return u;
            
            int ulp=find(parent[u]);
            parent[u]=ulp;
            
            return ulp;
        }
        
        public void union(int u,int v){
            int p1=find(u);
            int p2=find(v);
            
            if(p1==p2) return;
            
            if(size[p1]>size[p2]){
                parent[p2]=p1;
                size[p1]+=size[p2];
            }
            else{
                parent[p1]=p2;
                size[p2]+=size[p1];
            }
        }
    }
	int kruskalsMST(int V, int[][] edges) {
		
		//n log n
		Arrays.sort(edges,(a,b)->{
		    return a[2]-b[2];
		});
		
		DSU dsu=new DSU(V);
		
		int mst=0;
		
		//amortized complexity ->O(4 * alpha * m(edgesSize)) -> O(m)
		for(int e[]:edges){
		    int u=e[0];
		    int v=e[1];
		    int wt=e[2];
		    
		    if(dsu.find(u)!=dsu.find(v)){
		        mst+=wt;
		        dsu.union(u,v);
		    }
		}
		
		return mst;
	}
}

```
