//BellmanFord
#include<stdio.h>
#include<stdlib.h>
struct Edge
{
	int src,dest,weight;
};
struct Graph
{
	int V,E;
	struct Edge *edge;
};
struct Graph* createGraph(int V,int E)
{
	struct Graph* graph=(struct Graph*)malloc(sizeof(struct Graph));
	graph->V=V;
	graph->E=E;
	graph->edge=(struct Edge*)malloc(sizeof(struct Edge));
	return graph;
}

void print(int dist[],int n)
{
	printf("Distance from Source\n");
	int i;
	for(i=0;i<n;i++)
		printf("%d\t\t%d",i,dist[i]);
}

void BellmanFord(struct Graph* graph,int src)
{
	int V=graph->V;
	int E=graph->E;
	int dist[V];
	int i,j;
	for(i=0;i<V;i++)
		dist[i]=INT_MAX;
	dist[src]=0;
	
	for(i=1;i<=V-1;i++)
	{
		for(j=0;j<E;j++)
		{
		int u=graph->edge[j].src;
		int v=graph->edge[j].dest;
		int weight=graph->edge[j].weight;
		if(dist[u]!=INT_MAX && dist[u]+ weight<dist[v])
			dist[v]=dist[u]+weight; 
		}
	}
	for(j=0;j<E;j++)
	{
		int u=graph->edge[j].src;
		int v=graph->edge[j].dest;
		int weight=graph->edge[j].weight;
		if(dist[u]!=INT_MAX && dist[u]+ weight<dist[v])
			printf("Graph contains the negative weight cycle\n");
	}
	
	print(dist,V);
}
void main()
{
	int V,E;
	printf("Enter the number of vertices in the graph:");
	scanf("%d",&V);
	printf("Enter the number of edges in the graph:");
	scanf("%d",&E);
	struct Graph* graph=createGraph(V,E);
	int i;
	for(i=0;i<E;i++)
	{
		printf("Enter the source of edge %d: ",i+1);
		scanf("%d",&graph->edge[i].src);
		printf("Enter the destination of edge %d: ",i+1);
		scanf("%d",&graph->edge[i].dest);
		printf("Enter the weight of edge %d: ",i+1);
		scanf("%d",&graph->edge[i].weight);
	}
	BellmanFord(graph,0);
}
