//dijktras
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

// Structure to represent a graph
struct Graph {
    int V, E;
    int** adjMatrix;
};

// Create a graph with V vertices and E edges
struct Graph* createGraph(int V, int E) {
    struct Graph* graph = (struct Graph*)malloc(sizeof(struct Graph));
    graph->V = V;
    graph->E = E;
    
    // Allocate memory for the adjacency matrix
    graph->adjMatrix = (int**)malloc(V * sizeof(int*));
    for (int i = 0; i < V; i++) {
        graph->adjMatrix[i] = (int*)malloc(V * sizeof(int));
        for (int j = 0; j < V; j++) {
            graph->adjMatrix[i][j] = INT_MAX; // Initialize all distances to infinity
        }
    }
    
    return graph;
}

// Utility function to find the vertex with minimum distance value
int minDistance(int dist[], int sptSet[], int V) {
    int min = INT_MAX, min_index;
    
    for (int v = 0; v < V; v++)
        if (sptSet[v] == 0 && dist[v] <= min)
            min = dist[v], min_index = v;
    
    return min_index;
}

// Function to print the constructed distance array
void print(int dist[], int n) {
    printf("Vertex \t Distance from Source\n");
    for (int i = 0; i < n; i++)
        printf("%d \t\t %d\n", i, dist[i]);
}

// Dijkstra's algorithm for a graph represented using an adjacency matrix
void Dijkstra(struct Graph* graph, int src) {
    int V = graph->V;
    int dist[V];
    int sptSet[V];
    
    // Initialize all distances as INFINITE and sptSet[] as false
    for (int i = 0; i < V; i++)
        dist[i] = INT_MAX, sptSet[i] = 0;
    
    // Distance of source vertex from itself is always 0
    dist[src] = 0;
    
    // Find shortest path for all vertices
    for (int count = 0; count < V - 1; count++) {
        // Pick the minimum distance vertex from the set of vertices not yet processed
        int u = minDistance(dist, sptSet, V);
        
        // Mark the picked vertex as processed
        sptSet[u] = 1;
        
        // Update dist value of the adjacent vertices of the picked vertex
        for (int v = 0; v < V; v++)
            if (!sptSet[v] && graph->adjMatrix[u][v] != INT_MAX && dist[u] != INT_MAX 
                && dist[u] + graph->adjMatrix[u][v] < dist[v])
                dist[v] = dist[u] + graph->adjMatrix[u][v];
    }
    
    // Print the constructed distance array
    print(dist, V);
}

void main() {
    int V, E;
    printf("Enter the number of vertices in the graph: ");
    scanf("%d", &V);
    printf("Enter the number of edges in the graph: ");
    scanf("%d", &E);
    
    struct Graph* graph = createGraph(V, E);
    
    for (int i = 0; i < E; i++) {
        int src, dest, weight;
        printf("Enter the source of edge %d: ", i + 1);
        scanf("%d", &src);
        printf("Enter the destination of edge %d: ", i + 1);
        scanf("%d", &dest);
        printf("Enter the weight of edge %d: ", i + 1);
        scanf("%d", &weight);
        
        graph->adjMatrix[src][dest] = weight;
        // Uncomment the following line if the graph is undirected
        // graph->adjMatrix[dest][src] = weight;
    }
    
    Dijkstra(graph, 0);
}

