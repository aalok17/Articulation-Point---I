# Articulation-Point---I
Problem of Day Solution (12-dec-2022)(GFG)

```
import sys
sys.setrecursionlimit(10**6)
def dfs(node,adj,low,tin,vis,ans,time,parent):
    low[node]=tin[node]=time
    vis[node]=True
    child=0
    for i in adj[node]:
        if i==parent:
            continue
        if vis[i]==False:
            child+=1
            dfs(i,adj,low,tin,vis,ans,time+1,node)
            low[node]=min(low[node],low[i])
            
            if low[i]>=tin[node] and parent!=-1:
                ans[node]=1
            
        else:
            low[node]=min(low[node],tin[i])
   
    if parent==-1 and child>1:
       
        ans[node]=1

class Solution:
    
    #Function to return Breadth First Traversal of given graph.
    def articulationPoints(self, V, adj):
        low,tin,vis,ans=[-1]*V,[-1]*V,[False]*V,[-1]*V
        for i in range(V):
            if vis[i]==False:
                dfs(i,adj,low,tin,vis,ans,0,-1)
        res=[]
       
        for i in range(len(ans)):
            if ans[i]==1:
                res.append(i)
        if len(res)!=0:
            return res
        return [-1]
