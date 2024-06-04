//Heap-Sort
#include<stdio.h>
#include<stdlib.h>
int left(int i)
{
	return (2*i)+1;
}
int right(int i)
{
	return (2*i)+2;
}
void MaxHeapify(int A[],int heapSize,int i)
{
	int largest=i;
	int l=left(i);
	int r=right(i);
	if (l<=heapSize && A[l]>A[largest])
		largest=l;
	if (r<=heapSize && A[r]>A[largest])
		largest=r;
	if(largest!=i)
	{
		int temp=A[i];
		A[i]=A[largest];
		A[largest]=temp;
		MaxHeapify(A,heapSize,largest);
	}
}
void BuildMaxHeap(int A[],int length)
{
	int i;
	for(i=length/2;i>=0;i--)
	{
		MaxHeapify(A,length,i);
	}
}
void HeapSort(int A[],int n)
{
	int i;
	int heapSize=n-1;
	BuildMaxHeap(A,n);
	for(i=n-1;i>=0;i--)
	{
			int temp=A[0];
			A[0]=A[i];
			A[i]=temp;
			heapSize=heapSize-1;
			MaxHeapify(A,heapSize,0);
	}
}
void main()
{
	int i,n;
	printf("Enter the total no. of elements:");
	scanf("%d",&n);
	int *A=(int*)malloc(n*sizeof(int));
	for(i=0;i<n;i++)
		A[i]=rand()%n;
	HeapSort(A,n);
	for(i=0;i<n;i++)
		printf("%d ",A[i]);
}
