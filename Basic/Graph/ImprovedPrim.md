# Improved Prim

```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.PriorityQueue;

class Path {
	public String node1;
	public String node2;
	public int weight;

	public Path(String node1, String node2, int weight) {
		this.node1 = node1;
		this.node2 = node2;
		this.weight = weight;
	}

	public String toString() {
		return "(" + this.weight + ", " + this.node1 + ", " + this.node2 + ")";
	}
}

class Edge implements Comparable<Edge> {
	public String node;
	public int weight;

	public Edge(String node, int weight) {
		this.node = node;
		this.weight = weight;
	}

	public String toString() {
		return "(" + this.weight + ", " + this.node + ")";
	}

	@Override
	public int compareTo(Edge edge) {
		return this.weight - edge.weight;
	}
}

public class ImprovedPrim {
	public ArrayList<Path> improvedPrimFunc(HashMap<String, HashMap<String, Integer>> graph, String startNode) {
		ArrayList<Path> mst = new ArrayList<>();
		PriorityQueue<Edge> keys = new PriorityQueue<>();
		HashMap<String, Edge> keysObjects = new HashMap<String, Edge>();
		HashMap<String, String> mstPath = new HashMap<String, String>();
		Integer totalWeight = 0;
		HashMap<String, Integer> linkedEdges = new HashMap<>();
		Edge edgeObject, poppedEdge, linkedEdge;

		// 초기화
		for (String key : graph.keySet()) {
			if (key == startNode) {
				edgeObject = new Edge(key, 0);
				mstPath.put(key, key);
			} else {
				edgeObject = new Edge(key, Integer.MAX_VALUE);
				mstPath.put(key, null);
			}
			keys.add(edgeObject);
			keysObjects.put(key, edgeObject);
		}

		while (keys.size() > 0) {
			poppedEdge = keys.poll();
			keysObjects.remove(poppedEdge.node);

			mst.add(new Path(mstPath.get(poppedEdge.node), poppedEdge.node, poppedEdge.weight));
			totalWeight += poppedEdge.weight;

			linkedEdges = graph.get(poppedEdge.node);
			for (String adjacent : linkedEdges.keySet()) {
				if (keysObjects.containsKey(adjacent)) {
					linkedEdge = keysObjects.get(adjacent);

					if(linkedEdge.weight > linkedEdges.get(adjacent)) {
						linkedEdge.weight = linkedEdges.get(adjacent);
						mstPath.put(adjacent, poppedEdge.node);

						keys.remove(linkedEdge);
						keys.add(linkedEdge);
					}
				}
			}
		}
		System.out.println(totalWeight);
		return mst;
	}
}

```
