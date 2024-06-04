//TowerOfHanoi
#include<stdio.h>
void Tower(int n,char S,char H,char D)
{
	if(n==0)return;
	Tower(n-1,S,D,H);
	printf("%c -> %c\n",S,D);
	Tower(n-1,H,S,D);
	return;
}
void main()
{
	int n;
	printf("Enter the total number of disk:");
	scanf("%d",&n);
	Tower(n,'A','B','C');
}
