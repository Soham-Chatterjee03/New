//N_Queens
#include<stdio.h>
#include<stdlib.h>
void printSolution(int N,int board[N][N])
{
	int i,j;
	for(i=0;i<N;i++)
	{
		for(j=0;j<N;j++)
			printf("%2d",board[i][j]);
		printf("\n");
	}
	printf("\n");
}
int isSafe(int N,int board[N][N],int row,int col)
{
	int i,j;
	for(i=0;i<col;i++)//left
		if(board[row][i])
			return 0;
	
	for(i=row,j=col;i>=0 && j>=0;i--,j--)//upper diagonal on left
		if(board[i][j])
			return 0;
	
	for(i=row,j=col;i<N && j>=0;i++,j--)//lower diagonal on left
		if(board[i][j])
			return 0;
	return 1;
}
int solveNQUtil(int N,int board[N][N],int col)
{
	int i;
	if(col>=N)
		return 1;
	for(i=0;i<N;i++)
	{
		if(isSafe(N,board,i,col))
		{
			board[i][col]=1;
			if(solveNQUtil(N,board,col+1))
				return 1;
			board[i][col]=0;
		}	
	}
	return 0;
}
void solveNQ(int N)
{
	int board[N][N],i,j;
	for(i=0;i<N;i++)
	{
		for(j=0;j<N;j++)
			board[i][j]=0;
	}
	if(solveNQUtil(N,board,0)==0)
	{
		printf("Solution does not exist");
		return;
	}
	printSolution(N,board);
}
void main()
{
	int N;
	printf("Enter the value pf N: ");
	scanf("%d",&N);
	solveNQ(N);
}
