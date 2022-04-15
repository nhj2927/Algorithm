# Prim

```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.PriorityQueue;

class Edge implements Comparable<Edge> {
	public int weight;
	public String node1;
	public String node2;

	public Edge(int weight, String node1, String node2) {
		this.weight = weight;
		this.node1 = node1;
		this.node2 = node2;
	}

	public String toString() {
		return "(" + this.weight + ", " + this.node1 + ", " + this.node2 + ")";
	}

	@Override
	public int compareTo(Edge edge) {
		return this.weight - edge.weight;
	}
}

public class Prim {
	public ArrayList<Edge> primFunc(String startNode, ArrayList<Edge> edges) {
		Edge currentEdge, poppedEdge, adjacentEdgeNode;
		ArrayList<Edge> currentEdgeList, candidateEdgeList, adjacentEdgeNodes;

		ArrayList<String> connectedNodes = new ArrayList<String>();
		ArrayList<Edge> mst = new ArrayList<Edge>();
		HashMap<String, ArrayList<Edge>> adjacentEdges = new HashMap<>();
		PriorityQueue<Edge> priorityQueue;

		// 초기화
		// adjacentEdges에 edges에 있는 vertex 삽입
		for (int i = 0; i < edges.size(); i++) {
			currentEdge = edges.get(i);
			if (!adjacentEdges.containsKey(currentEdge.node1)) {
				adjacentEdges.put(currentEdge.node1, new ArrayList<Edge>());
			}
			if (!adjacentEdges.containsKey(currentEdge.node2)) {
				adjacentEdges.put(currentEdge.node2, new ArrayList<Edge>());
			}
		}

		// adjacentEdges의 각 vertex에 연결된 vertex list 삽입
		for (int i = 0; i < edges.size(); i++) {
			currentEdge = edges.get(i);
			currentEdgeList = adjacentEdges.get(currentEdge.node1);
			currentEdgeList.add(new Edge(currentEdge.weight, currentEdge.node1, currentEdge.node2));
			currentEdgeList = adjacentEdges.get(currentEdge.node2);
			currentEdgeList.add(new Edge(currentEdge.weight, currentEdge.node2, currentEdge.node1));
		}

		connectedNodes.add(startNode);
		candidateEdgeList = adjacentEdges.getOrDefault(startNode, new ArrayList<Edge>());
		priorityQueue = new PriorityQueue<>();
		for (int i = 0; i < candidateEdgeList.size(); i++) {
			priorityQueue.add(candidateEdgeList.get(i));
		}

		while (priorityQueue.size() > 0) {
			poppedEdge = priorityQueue.poll();
			if (!connectedNodes.contains(poppedEdge.node2)) {
				connectedNodes.add(poppedEdge.node2);
				mst.add(new Edge(poppedEdge.weight, poppedEdge.node1, poppedEdge.node2));

				adjacentEdgeNodes = adjacentEdges.getOrDefault(poppedEdge.node2, new ArrayList<Edge>());
				for (int i = 0; i < adjacentEdgeNodes.size(); i++) {
					adjacentEdgeNode = adjacentEdgeNodes.get(i);
					if (!connectedNodes.contains(adjacentEdgeNode.node2)) {
						priorityQueue.add(adjacentEdgeNode);
					}
				}
			}
		}

		return mst;
	}
}

```
