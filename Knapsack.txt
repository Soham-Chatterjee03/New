//knapsack
#include<stdio.h>
#include<stdlib.h>
int max(float pw[],int n)
{ 
	int max=0;
	int i;
	for(i=0;i<n;i++)
	{
		if(pw[max]<pw[i])
			max=i;
	}
	return max;
}
void main()
{
	double capacity;
	printf("Enter the capacity of the knapsack bag: ");
	scanf("%lf",&capacity);
	int n;
	printf("Enter the no. of elements in total: ");
	scanf("%d",&n);
	double *p=(double*)malloc(n*sizeof(double));
	double *w=(double*)malloc(n*sizeof(double));
	int i;
	for(i=0;i<n;i++)
	{
		printf("Enter the profit of %d item:",i+1);
		scanf("%lf",&p[i]);
		printf("Enter the weight of %d item:",i+1);
		scanf("%lf",&w[i]);
	}
	float pw[n];
	for(i=0;i<n;i++)
	{
		pw[i]=p[i]/w[i];
	}
	double sol[n];
	double tot_prof=0;
	for(i=0;i<n;i++)
	{
		int k=max(pw,n);
		pw[k]=-1;
		if(capacity>0)
		{
			if(capacity-w[k]>=0)
			{
				sol[k]=1.0000;
				tot_prof=tot_prof+p[k];
				capacity=capacity-w[k];
			}
			else
			{
				sol[k]=capacity/w[k];
				capacity=capacity-w[k];
				tot_prof=tot_prof+(p[k]*sol[k]);
			}			
		}
	}
	printf("Total Profit=%lf",tot_prof);
	printf("\nSolution Vector: ");
	for(i=0;i<n;i++)
		printf("%lf ",sol[i]);
}
