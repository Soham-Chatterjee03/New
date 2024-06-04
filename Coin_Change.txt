//Coin_Change
#include<stdio.h>
#include<stdlib.h>
int max(int coins[],int n)
{
	int max=0;
	int i;
	for(i=1;i<n;i++)
	{
		if(coins[max]<coins[i])
			max=i;
	}
	return max;
}
void main()
{
	int n,i;
	printf("Enter number of coins: ");
	scanf("%d",&n);
	int coins[100];
	printf("Enter the values");
	for(i=0;i<n;i++)
		scanf("%d",&coins[i]);
	printf("Enter the amount: ");
	int amount;
	scanf("%d",&amount);
	int sol[n];
	for(i=0;i<n;i++)
		sol[i]=0;
	for(i=0;i<n;i++)
	{
		int k=max(coins,n);
		while(amount>=coins[k])
		{
			amount=amount-coins[k];
			sol[k]+=1;
		}
		coins[k]=-1;
	}		

	for(i=0;i<n;i++)
		printf("%d ",sol[i]);
}
