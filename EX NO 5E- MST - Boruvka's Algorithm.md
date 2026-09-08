
# EX 5E Minimum Spanning Tree -Boruvka's Algorithm
## DATE: 08.09.2026
## AIM:
To write a Java program to for given constraints.
Boruvka's Algorithm - Minimum Spanning Tree

Find the MST using Boruvka's Algorithm for a weighted undirected graph.
<img width="292" height="235" alt="image" src="https://github.com/user-attachments/assets/06246b27-37a9-40a8-bd7a-37a1d5187cd1" />

## Algorithm
1. Start by making each vertex a separate component using the parent[] array.
2. For every component, find its cheapest outgoing edge.
3. Add the selected cheapest edges to the MST and join the corresponding components using union().
4. Repeat the process until the number of components becomes 1 and all MST edges are selected.
5. Print each selected edge and calculate the total weight of the MST.

## Program:
```
/*
Program to implement Reverse a String
Developed by: EZHIL NEVEDHA K
Register Number:  212223230055
*/
import java.util.*;

public class BoruvkaMST {
    static int[] parent;

    static int find(int i) {
        if (parent[i] != i)
            parent[i] = find(parent[i]);
        return parent[i];
    }

    static void union(int x, int y) {
        parent[find(x)] = find(y);
    }

    static int boruvkaMST(int V, List<Edge> edges) {
        parent = new int[V];

        for (int i = 0; i < V; i++) {
            parent[i] = i;
        }

        int components = V;
        int totalWeight = 0;

        while (components > 1) {
            Edge[] cheapest = new Edge[V];

            for (Edge edge : edges) {
                int set1 = find(edge.src);
                int set2 = find(edge.dest);

                if (set1 == set2)
                    continue;

                if (cheapest[set1] == null ||
                    edge.weight < cheapest[set1].weight) {
                    cheapest[set1] = edge;
                }

                if (cheapest[set2] == null ||
                    edge.weight < cheapest[set2].weight) {
                    cheapest[set2] = edge;
                }
            }

            for (int i = 0; i < V; i++) {
                if (cheapest[i] != null) {
                    Edge edge = cheapest[i];

                    int set1 = find(edge.src);
                    int set2 = find(edge.dest);

                    if (set1 == set2)
                        continue;

                    union(set1, set2);

                    System.out.println("Edge: " + edge.src + "-" +
                                       edge.dest + " Weight: " +
                                       edge.weight);

                    totalWeight += edge.weight;
                    components--;
                }
            }
        }

        return totalWeight;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int V = sc.nextInt();
        int E = sc.nextInt();

        List<Edge> edges = new ArrayList<>();

        for (int i = 0; i < E; i++) {
            edges.add(new Edge(
                sc.nextInt(),
                sc.nextInt(),
                sc.nextInt()
            ));
        }

        int totalWeight = boruvkaMST(V, edges);

        System.out.println("Total Weight of MST: " + totalWeight);

        sc.close();
    }
}

class Edge {
    int src, dest, weight;

    Edge(int s, int d, int w) {
        src = s;
        dest = d;
        weight = w;
    }
}
```

## Output:
<img width="737" height="437" alt="image" src="https://github.com/user-attachments/assets/22d3369b-b337-4801-97b3-d17a3e7bb9d5" />



## Result:
The program successfully implemented and the expected output is verified.
