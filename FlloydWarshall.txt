//Floyd Warshall
#include<stdio.h>
#define INF 99999
int n;
int g[100][100], d[100][100], p[100][100];
void printmatrix()
{
	int i, j;
	for(i=0;i<n;i++)
	{
		for(j=0;j<n;j++)
		if(d[i][j]==INF)
		printf("INF ");
		else
		printf("%d ", d[i][j]);
		printf("\n");
	}//for
}//printmatrix()
void printPredMat()
{
	int i, j;
	for(i=0;i<n;i++)
	{
		for(j=0;j<n;j++)
		if(p[i][j]==-1)
		printf("NIL ");
		else
		printf("%d ", p[i][j]);
		printf("\n");
	}//for
}//printPredMat()
void FloydWarshall()
{
	int i, j, k;
	for(i=0;i<n;i++)
	for(j=0;j<n;j++)
	{
		d[i][j]=g[i][j];
		if(i==j||g[i][j]==INF)
		p[i][j]=-1;
		else
		p[i][j]=i;
	}//for
	for(k=0;k<n;k++)
	for(i=0;i<n;i++)
	for(j=0;j<n;j++)
	if(d[i][k]+d[k][j]<d[i][j])
	{
		d[i][j]=d[i][k]+d[k][j];
		p[i][j]=p[k][j];
	}//if
	printf("Distance matrix:\n");
	printmatrix();
	printf("Predessor matrix:\n");
	printPredMat();
}//FloydWarshall()
int main()
{
	printf("Enter number of vertices: ");
	scanf("%d", &n);
	int i, j;
	printf("Enter weight matrix:(use 99999 to represent infinity)\n");
	for(i=0;i<n;i++)
	for(j=0;j<n;j++)
	scanf("%d", &g[i][j]);
	FloydWarshall();
	return 0;
}//main()
