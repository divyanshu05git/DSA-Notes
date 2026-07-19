```java
class Main{
public static int articulation(int n,int arr[][],int cost[]){
        Map<Integer,List<Integer>> g=new HashMap<>();
        int disc[]=new int[n];
        int low[]=new int[n];
        boolean vis[]=new boolean[n];
        boolean arti[]=new boolean[n];

        for(int i=0;i<n;i++){
            disc[i]=low[i]=-1;
            g.put(i,new ArrayList<>());
        }

        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                if(arr[i][j]==1){
                    g.get(i).add(j);
                }
            }
        }

        timer=0;
        for(int i=0;i<n;i++){
            if(!vis[i]) dfs(i,-1,disc,low,vis,arti,g);
        }

        int ans=0;
        for(int i=0;i<n;i++){
            if(arti[i]) ans+=cost[i];
        }


        return ans;
    }
    public static void dfs(int node,int par,int disc[],int low[],boolean vis[],boolean arti[],Map<Integer,List<Integer>> g){
        vis[node]=true;
        disc[node]=low[node]=timer++;

        int child=0;

        for(int e:g.get(node)){
            if(e==par) continue;
            if(!vis[e]){
                child++;
                dfs(e,node,disc,low,vis,arti,g);

                low[node]=Math.min(low[node],low[e]);

                if(low[e]>=disc[node] && par!=-1){
                    arti[node]=true;
                }
            }
            else{
                low[node]=Math.min(low[node],disc[e]);
            }

            
        }

        if(child>1 && par==-1){
            arti[node]=true;
        }
    }
  }
```  
    
