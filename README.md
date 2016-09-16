# printing-all-elements-in-a-cycle-in-directed-graph
printing all  elements in a cycle in directed graph
//strongly_connected_components.cpp
#include <bits/stdc++.h>
using namespace std;

#define ll long long int
#define sf scanf
#define sf_d(var) scanf("%d",&var)
#define sf_dd(var) scanf("%lld",&var)
#define pf printf
#define pf_d(var) printf("%d",var)
#define pf_dd(var) printf("%lld",var)
#define psp printf(" ")
#define pnlin printf("\n")
#define vi vector<int>
#define pb push_back
#define v_iter vector<int>::iterator
#define fr(start,end) for(int z=start;z<end;z++)
#define tr(cont,it) for(typeof(cont.begin()) it=cont.begin();it!=cont.end();it++)
#define mod 1000000007
#define srt(cont) sort(cont.begin(),cont.end())
#define all(m) m.begin(),m.end()

void dfs(int i,vector<bool>& vwb,vi& vg,vector<bool>& vgb,int & min,vector< vi >& g)
{
    vgb[i]=true;
    vg.pb(i);
    for(int j=0;j<g[i].size();j++)
    {
    	if(vgb[g[i][j]])
    	{
    		vi::reverse_iterator iter=vg.rbegin();
    		pf_d(g[i][j]);
    		pf("<-");pf_d(*iter);
    		while(*iter!=g[i][j])
    		{
    		    iter++;
    		    pf("<-");pf_d(*iter);
    		}    
    		/*if(min>count)
    			min=count;*/
    		pnlin;	
    	}
    	else if(vwb[g[i][j]])
    		dfs(g[i][j],vwb,vg,vgb,min,g);
    }
    vwb[i]=false;
    vg.pop_back();
    vgb[i]=false;
}

void dfs_utill(vector< vi >& g,int& min)
{
	vector<bool> vwb(g.size(),true);
	vi vg;
	for(int k=1;k<g.size();k++)
		if(vwb[k])
		{
			vector<bool> vgb(g.size(),false);
			dfs(k,vwb,vg,vgb,min,g);
		}
}

int main()
{
    int n,e,t1,t2,min=2000;
    sf_d(n);
    sf_d(e);
    vector< vi > g(n+1);
    fr(0,e)
    {
        sf_d(t1);sf_d(t2);
        g[t1].pb(t2);
    }
    dfs_utill(g,min);
    if(min==2000)
    	min=1;
    //pf_d(min);	
    
    return 0;
}
