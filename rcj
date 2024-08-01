#include <iostream>
#include <vector>
#include <queue>
#include <climits>

using namespace std;

struct Edge {
    int destination;
    int weight;
};

struct Graph {
    int V;
    vector<vector<Edge>> adjList;

    Graph(int V) {
        this->V = V;
        adjList.resize(V);
    }

    void addEdge(int src, int dest, int weight) {
        adjList[src].push_back({dest, weight});
        adjList[dest].push_back({src, weight}); // For undirected graph
    }

    vector<int> dijkstra(int start) {
        vector<int> dist(V, INT_MAX);
        vector<bool> visited(V, false);
        priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;

        pq.push({0, start});
        dist[start] = 0;

        while (!pq.empty()) {
            int u = pq.top().second;
            pq.pop();

            if (visited[u]) continue;
            visited[u] = true;

            for (auto &edge : adjList[u]) {
                int v = edge.destination;
                int weight = edge.weight;

                if (dist[u] + weight < dist[v]) {
                    dist[v] = dist[u] + weight;
                    pq.push({dist[v], v});
                }
            }
        }

        return dist;
    }
};

struct Train {
    int id;
    string name;
    int capacity;
};

void allocateTrain(const Train &train, int start, int end, int distance) {
    cout << "Allocating train " << train.name << " (ID: " << train.id 
         << ") with capacity " << train.capacity 
         << " for route from station " << start 
         << " to station " << end 
         << " with distance " << distance << " km." << endl;
}

int main() {
    // Number of stations
    int V = 5;

    // Creating a graph with V stations
    Graph g(V);

    // Adding edges between stations (stations are indexed from 0)
    g.addEdge(0, 1, 10);
    g.addEdge(0, 2, 3);
    g.addEdge(1, 2, 1);
    g.addEdge(1, 3, 2);
    g.addEdge(2, 3, 8);
    g.addEdge(3, 4, 7);
    g.addEdge(2, 4, 2);

    // Define trains
    vector<Train> trains = {
        {1, "Express", 300},
        {2, "Local", 150},
        {3, "Superfast", 500}
    };

    int startStation = 0;
    int endStation = 4;

    // Find shortest path from startStation to endStation
    vector<int> distances = g.dijkstra(startStation);

    // Output the shortest distance
    cout << "Shortest distance from station " << startStation << " to station " << endStation << " is: " << distances[endStation] << " km." << endl;

    // Allocate a train for the found route
    allocateTrain(trains[0], startStation, endStation, distances[endStation]);

    return 0;
}
