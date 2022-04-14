# Dijkstra.md

```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.PriorityQueue;

class Edge implements Comparable<Edge> {
	public int distance;
	public String vertex;

	public Edge(int distance, String vertex) {
		this.distance = distance;
		this.vertex = vertex;
	}

	public String toString() {
		return "vertex: " + this.vertex + ", distance: " + this.distance;
	}

	@Override
	public int compareTo(Edge edge) {
		return this.distance - edge.distance;
	}
}

public class Dijkstra {
	public HashMap<String, Integer> dijkstraFunc(HashMap<String, ArrayList<Edge>> graph, String start) {
		Edge edgeNode;
		int currentDistance, weight, distance;
		String currentNode, adjacent;
		ArrayList<Edge> nodeList;
		Edge adjacentNode;
		HashMap<String, Integer> distances = new HashMap<>();
		PriorityQueue<Edge> priorityQueue = new PriorityQueue<>();

		// 초기화
		for (String node : graph.keySet()) {
			distances.put(node, Integer.MAX_VALUE);
		}
		distances.put(start, 0);

		priorityQueue.add(new Edge(distances.get(start), start));

		// 알고리즘
		while (priorityQueue.size() > 0) {
			edgeNode = priorityQueue.poll();
			currentDistance = edgeNode.distance;
			currentNode = edgeNode.vertex;

			if (distances.get(currentNode) < currentDistance) {
				continue;
			}

			nodeList = graph.get(currentNode);
			for (int i = 0; i < nodeList.size(); i++) {
				adjacentNode = nodeList.get(i);
				adjacent = adjacentNode.vertex;
				weight = adjacentNode.distance;

				distance = currentDistance + weight;

				if (distances.get(adjacent) > distance) {
					priorityQueue.add(new Edge(distance, adjacent));
					distances.put(adjacent, distance);
				}
			}
		}

		return distances;
	}
}

```
