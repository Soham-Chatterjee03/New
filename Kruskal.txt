//Kruskal
#include <stdio.h>
#include <stdlib.h>

struct Edge{
    int src, dest, weight;
};

struct Graph{
    int V, E;
    struct Edge* edge;
};

struct Graph* createGraph(int V, int E){
    struct Graph* graph = (struct Graph*)malloc(sizeof(struct Graph));
    graph->V = V;
    graph->E = E;
    graph->edge = (struct Edge*)malloc(E * sizeof(struct Edge));
    return graph;
}

int find(int parent[], int i){
    if (parent[i] == -1)
        return i;
    return find(parent, parent[i]);
}

void Union(int parent[], int x, int y){
    int xset = find(parent, x);
    int yset = find(parent, y);
    parent[xset] = yset;
}

int compare(const void* a, const void* b){
    struct Edge* a1 = (struct Edge*)a;
    struct Edge* b1 = (struct Edge*)b;
    return a1->weight - b1->weight;
}

void KruskalMST(struct Graph* graph) {
    int V = graph->V;
    struct Edge result[V];
    int e = 0;
    int i = 0;

    qsort(graph->edge, graph->E, sizeof(graph->edge[0]), compare);

    int* parent = (int*)malloc(V * sizeof(int));

    for (int v = 0; v < V; ++v){
        parent[v] = -1;
    }
    while (e < V - 1 && i < graph->E){
        struct Edge next_edge = graph->edge[i++];
        int x = find(parent, next_edge.src);
        int y = find(parent, next_edge.dest);
        if (x != y) {
            result[e++] = next_edge;
            Union(parent, x, y);
        }
    }
    printf("Edges in the minimum spanning tree:\n");
    for (i = 0; i < e; ++i)
        printf("(%d, %d) -> %d\n", result[i].src, result[i].dest, result[i].weight);
    free(parent);
}

int main() {
    int V, E;
    printf("Enter the number of vertices: ");
    scanf("%d", &V);
    printf("Enter the number of edges: ");
    scanf("%d", &E);

    struct Graph* graph = createGraph(V, E);

    printf("Enter the source, destination, and weight for each edge:\n");
    for (int i = 0; i < E; ++i) {
        scanf("%d %d %d", &graph->edge[i].src, &graph->edge[i].dest, &graph->edge[i].weight);
    }

    KruskalMST(graph);
    return 0;
}