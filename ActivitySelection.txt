//Activity Selection
#include<stdio.h>
#include<stdlib.h>
void main()
{
	int n,i,j;
	printf("Enter total number of task to be performed:");
	scanf("%d",&n);
	int *stime=(int*)malloc(n*sizeof(int));
	int *etime=(int*)malloc(n*sizeof(int));
	printf("Enter the starting time of all the tasks");
	for(i=0;i<n;i++)
		scanf("%d",&stime[i]);
	printf("Enter the ending time of all the tasks");
	for(i=0;i<n;i++)
		scanf("%d",&etime[i]);
	int sol[n];
	for(i=0;i<n;i++)
		sol[i]=0;
	sol[0]=1;
	j=0;
	for(i=1;i<n;i++)
	{
		if(stime[i]>=etime[j])
		{
			sol[i]=1;
			j=i;
		}
	}
	printf("Solution Vector: ");
	for(i=0;i<n;i++)
		printf("%d ",sol[i]);
}
