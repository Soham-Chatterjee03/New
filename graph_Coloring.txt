//graph-color
#include <stdio.h>
#include<stdbool.h>
#define MAX_VERTICES 20 // Maximum number of vertices

void printSolution(int color[], int V);

bool isSafe(int v, bool graph[MAX_VERTICES][MAX_VERTICES], int color[], int c, int V)
{
	int i;
    for (i = 0; i < V; i++)
        if (graph[v][i] && c == color[i])
            return false;
    return true;
}

bool graphColoringUtil(bool graph[MAX_VERTICES][MAX_VERTICES], int m, int color[], int v, int V)
{
    if (v == V)
        return true;
	int c;
    for (c = 1; c <= m; c++) {
        if (isSafe(v, graph, color, c, V)) {
            color[v] = c;

            if (graphColoringUtil(graph, m, color, v + 1, V) == true)
                return true;

            color[v] = 0;
        }
    }

    return false;
}

bool graphColoring(bool graph[MAX_VERTICES][MAX_VERTICES], int m, int V)
{
    int color[MAX_VERTICES],i;
    for (i = 0; i < V; i++)
        color[i] = 0;

    if (graphColoringUtil(graph, m, color, 0, V) == false) {
        printf("Solution does not exist\n");
        return false;
    }

    printSolution(color, V);
    return true;
}

void printSolution(int color[], int V)
{
    printf("Solution Exists: Following are the assigned colors \n");
    int i;
	for (i = 0; i < V; i++)
        printf(" %d ", color[i]);
    printf("\n");
}

int main()
{
    int m, V;
    printf("Enter the number of vertices (maximum %d): ", MAX_VERTICES);
    scanf("%d", &V);

    if (V > MAX_VERTICES || V < 0) {
        printf("Invalid number of vertices\n");
        return 1;
    }

    bool graph[MAX_VERTICES][MAX_VERTICES];
    int x;
	int i,j;
    printf("Enter the adjacency matrix:\n");
    for (i = 0; i < V; i++) {
        for (j = 0; j < V; j++) {
            scanf("%d", &x);
            graph[i][j] = x;
        }
    }

    printf("Enter the number of colors: ");
    scanf("%d", &m);

    graphColoring(graph, m, V);
    return 0;
}
