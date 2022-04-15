# Kruskal

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.HashMap;

class Edge implements Comparable<Edge>{
	public int weight;
	public String nodeV;
	public String nodeU;

	public Edge(int weight, String nodeV, String nodeU) {
		this.weight = weight;
		this.nodeV = nodeV;
		this.nodeU = nodeU;
	}

	public String toString() {
		return "(" + this.weight + ", " + this.nodeV + ", " + this.nodeU + ")";
	}

	@Override
	public int compareTo(Edge edge) {
		return this.weight - edge.weight;
	}
}

public class Kruskal {
	HashMap<String, String> parent = new HashMap<String, String>();
	HashMap<String, Integer> rank = new HashMap<String, Integer>();

	public String find(String node) {
		// path compression 기법
		if (parent.get(node) != node) {
			parent.put(node, find(parent.get(node)));
		}
		return parent.get(node);
	}

	public void union(String nodeV, String nodeU) {
		String root1 = find(nodeV);
		String root2 = find(nodeU);

		//union-by-rank 기법
		if (rank.get(root1) > rank.get(root2)) {
			parent.put(root2, root1);
		} else {
			parent.put(root1, root2);
			rank.put(root1, rank.get(root1) + 1);
		}
	}

	public void makeSet(String node) {
		parent.put(node, node);
		rank.put(node, 0);
	}

	public ArrayList<Edge> kruskalFunc(ArrayList<String> vertices, ArrayList<Edge> edges) {
		ArrayList<Edge> mst = new ArrayList<Edge>();
		Edge currentEdge;

		// 초기화
		for (int i = 0; i < vertices.size(); i++) {
			makeSet(vertices.get(i));
		}

		// 간선 weight 기반 sorting
		Collections.sort(edges);

		// 구현
		for (int i = 0; i < edges.size(); i++) {
			currentEdge = edges.get(i);
			if (find(currentEdge.nodeU) != find(currentEdge.nodeV)) {
				union(currentEdge.nodeU, currentEdge.nodeV);
				mst.add(currentEdge);
			}
		}

		return mst;
	}
}

```
