//Prims_Algo
#include <stdio.h>    
#include <limits.h>    
#define vertices 5  
int minimum_key(int n,int k[], int mst[])    
{  
    int minimum  = INT_MAX, min,i;    
      
    for (i = 0; i < n; i++)  
        if (mst[i] == 0 && k[i] < minimum )   
            minimum = k[i], min = i;    
    return min;    
}    
 
void prim(int n,int g[10][10])    
{    
     
    int parent[n];    
    int k[n];       
    int mst[n];      
    int i, count,edge,v; 
    for (i = 0; i < n; i++)  
    {  
        k[i] = INT_MAX;  
        mst[i] = 0;    
    }  
    k[0] = 0; 
    parent[0] = -1;  
    for (count = 0; count < n-1; count++)    
    {    
        edge = minimum_key(n,k,mst);    
        mst[edge] = 1;    
        for (v = 0; v < n; v++)    
        {  
            if (g[edge][v] && mst[v] == 0 && g[edge][v] <  k[v])    
            {  
                parent[v]  = edge, k[v] = g[edge][v];    
            }  
        }  
     }    
     printf("\n Edge \t  Weight\n");  
     for (i = 1; i < n; i++)    
     printf(" %d <-> %d    %d \n", parent[i], i, g[i][parent[i]]);    
      
}    
int main()    
{   
	int i,j,n,g[10][10];
	printf("Enter the number of vertices:");
	scanf("%d",&n);
	printf("Enter the cost of the graph:\n");
	for(i=0;i<n;i++)
	{
		for(j=0;j<n;j++)
		{
			scanf("%d",&g[i][j]);
		}	
	}
	 

    prim(n,g);    
    return 0;  
}  

