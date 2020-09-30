# Add in your CPP codes here















//Sum of all pair shortest paths in a Tree
// C++ program for the above approach 

#include <iostream> 
using namespace std; 
#define INF 99999 

// Function that performs the Floyd 
// Warshall to find all shortest paths 
int floyd_warshall(int* graph, int V) 
{ 

	int dist[V][V], i, j, k; 

	// Initialize the distance matrix 
	for (i = 0; i < V; i++) { 
		for (j = 0; j < V; j++) { 
			dist[i][j] = *((graph + i * V) + j); 
		} 
	} 

	for (k = 0; k < V; k++) { 

		// Pick all vertices as 
		// source one by one 
		for (i = 0; i < V; i++) { 

			// Pick all vertices as 
			// destination for the 
			// above picked source 
			for (j = 0; j < V; j++) { 

				// If vertex k is on the 
				// shortest path from i to 
				// j then update dist[i][j] 
				if (dist[i][k] 
						+ dist[k][j] 
					< dist[i][j]) { 
					dist[i][j] 
						= dist[i][k] 
						+ dist[k][j]; 
				} 
			} 
		} 
	} 

	// Sum the upper diagonal of the 
	// shortest distance matrix 
	int sum = 0; 

	// Traverse the given dist[][] 
	for (i = 0; i < V; i++) { 

		for (j = i + 1; j < V; j++) { 

			// Add the distance 
			sum += dist[i][j]; 
		} 
	} 

	// Return the final sum 
	return sum; 
} 

// Function to generate the tree 
int sumOfshortestPath(int N, int E, 
					int edges[][3]) 
{ 
	int g[N][N]; 
	for (int i = 0; i < N; i++) { 
		for (int j = 0; j < N; j++) { 
			g[i][j] = INF; 
		} 
	} 

	// Add edges 
	for (int i = 0; i < E; i++) { 

		// Get source and destination 
		// with weight 
		int u = edges[i][0]; 
		int v = edges[i][1]; 
		int w = edges[i][2]; 

		// Add the edges 
		g[u][v] = w; 
		g[v][u] = w; 
	} 

	// Perform Floyd Warshal Algorithm 
	return floyd_warshall((int*)g, N); 
} 

// Driver code 
int main() 
{ 
	// Number of Vertices 
	int N = 4; 

	// Number of Edges 
	int E = 3; 

	// Given Edges with weight 
	int Edges[][3] 
		= { { 0, 1, 1 }, { 1, 2, 2 }, 
			{ 2, 3, 3 } }; 

	// Function Call 
	cout << sumOfshortestPath(N, E, Edges); 

	return 0; 
} 
