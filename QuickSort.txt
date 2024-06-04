//QuickSort
#include<stdio.h>
#include<stdlib.h>
int Partition(int a[],int low,int high)
{
	int pivot=a[high],i=low-1,j;
	for(j=low;j<high;j++)
	{
		if(a[j]<=pivot)
		{
			i++;
			int temp=a[i];
			a[i]=a[j];
			a[j]=temp;	
		}
	}
	int temp=a[i+1];
	a[i+1]=a[high];
	a[high]=temp;
	return i+1;
}
QuickSort(int a[],int low,int high)
{
	if(low<high)
	{
		int PartitionIndex=Partition(a,low,high);
		QuickSort(a,low,PartitionIndex-1);
		QuickSort(a,PartitionIndex+1,high);
	}
}
void main()
{
	int n,i;
	printf("Enter the no. of elements in the array:");
	scanf("%d",&n);
	int *a=(int*)malloc(n*sizeof(int));
	for(i=0;i<n;i++)
		a[i]=rand()%n;
	QuickSort(a,0,n-1);
	for(i=0;i<n;i++)
		printf("%d ",a[i]);
}
