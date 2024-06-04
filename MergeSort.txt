//MergeSort
#include<stdio.h>
#include<stdlib.h>
#include<time.h>
Merge(int A[],int low,int mid,int high)
{	
	int k=low,B[high],i=low,j=mid+1;
	while(i<=mid && j<=high)
	{
		if(A[i]<A[j])
		{
			B[k]=A[i];
			k++;
			i++;
		}
		else
		{
			B[k]=A[j];
			k++;
			j++;
		}		
	}
	while(i<=mid)
	{
		B[k]=A[i];
		k++;
		i++;
	}
	while(j<=high)
	{
		B[k]=A[j];
		k++;
		j++;
	}
	for(i=low;i<=high;i++)
	{		
		A[i]=B[i];
	}
}
mergeSort(int A[],int low,int high)
{

	
	if(low<high)
	{
		int mid=(high+low)/2;
		mergeSort(A,low,mid);
		mergeSort(A,mid+1,high);
		Merge(A,low,mid,high);
		
	}
}
void main()
{
	clock_t start,end;
	
	int i,n;
	printf("Enter no. of Elements:");
	scanf("%d",&n);
	int *a=(int*)malloc(n*sizeof(int));
	for(i=0;i<n;i++)
		a[i]=rand()%n;
	start=clock();
	mergeSort(a,0,n-1);
	end=clock();
	for(i=0;i<n;i++)
		printf("%d ",a[i]);
	
	
	double CPU_time;
	CPU_time=((double)(end-start)/CLOCKS_PER_SEC);
	printf("CPU-time:%lf",CPU_time);
}
