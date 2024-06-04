//0_1 Knapsack
#include<stdio.h>
int max(int a,int b)
{
	return(a>b)?a:b;
}

int KnapSack(int W,int wt[],int val[],int n)
{
	int i,w;
	int K[n+1][W+1];
	
	for(i=0;i<=n;i++)
	{
		for(w=0;w<=W;w++)
		{
			if(i==0||w==0)
				K[i][w]=0;
			else if(wt[i-1]<=w)
				K[i][w]=max(val[i-1]+K[i-1][w-wt[i-1]],K[i-1][w]);
			else K[i][w]=K[i-1][w];
		}
	}
	
	int res=K[n][W];
	printf("Maximum value in the knapsack=%d\n",res);
	w=W;
	printf("Items included in the knapsack:\n");
	int sol[n];
	for(i=0;i<n;i++)
		sol[i]=0;
	for(i=n;i>0 && res>0;i--)
	{
		if(res==K[i-1][w])
			continue;
		else
		{
			sol[i-1]=1;
			printf("Item %d(Value:%d,Weight:%d)\n",i,val[i-1],wt[i-1]);
			res=res-val[i-1];
			w=w-wt[i-1];
		}
		
	}
	printf("Solution Vector: ");
	for(i=0;i<n;i++)
			printf("%d ",sol[i]);
	return K[n][W];
}
void main()
{
	int n,i;
	printf("Enter the total number of items: ");
	scanf("%d",&n);
	int *val=(int*)malloc(n*sizeof(int));
	int *wt=(int*)malloc(n*sizeof(int));
	for(i=0;i<n;i++)
	{
		printf("Enter the profit of bag %d: ",i+1);
		scanf("%d",&val[i]);
		printf("Enter the weight of bag %d: ",i+1);
		scanf("%d",&wt[i]);
	}
	int W;
	printf("Enter the weight of the knapsack bag:");
	scanf("%d",&W);
	KnapSack(W,wt,val,n);
}
