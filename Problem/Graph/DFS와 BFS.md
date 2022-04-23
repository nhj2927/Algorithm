# DFS와 BFS

[문제](https://www.acmicpc.net/problem/1260)

```java
import java.io.BufferedReader;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;
import java.util.ArrayList;
import java.util.Collections;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

public class Main {
	static StringBuilder sb = new StringBuilder();
	static FastReader scan = new FastReader();

	static int N, M, start;
	static ArrayList<Integer>[] adj;
	static boolean[] visit;

	static void input() {
		N = scan.nextInt();
		M = scan.nextInt();
		start = scan.nextInt();
		adj = new ArrayList[N + 1];
		for (int i = 1; i <= N; i++) {
			adj[i] = new ArrayList<>();
		}
		for (int i = 1; i <= M; i++) {
			int v1 = scan.nextInt();
			int v2 = scan.nextInt();
			adj[v1].add(v2);
			adj[v2].add(v1);
		}
		for (int i = 1; i <= N; i++) {
			Collections.sort(adj[i]);
		}
	}

	static void dfs(int x) {
		visit[x] = true;
		sb.append(x).append(' ');

		for (int y : adj[x]) {
			if (visit[y])
				continue;
			dfs(y);
		}
	}

	static void bfs(int x) {
		Queue<Integer> que = new LinkedList<>();

		que.add(x);
		visit[x] = true;

		while (!que.isEmpty()) {
			int v = que.poll();
			sb.append(v).append(' ');

			for (int y : adj[v]) {
				if (visit[y]) continue;

				que.add(y);
				visit[y] = true;
			}
		}
	}

	static void pro() {
		visit = new boolean[N + 1];
		dfs(start);
		sb.append('\n');
		for (int i = 1; i <= N; i++)
			visit[i] = false;
		bfs(start);

		System.out.println(sb.toString());
	}

	public static void main(String[] args) {
		input();
		pro();
	}

	static class FastReader {
		BufferedReader br;
		StringTokenizer st;

		public FastReader() {
			br = new BufferedReader(new java.io.InputStreamReader(System.in));
		}

		public FastReader(String s) throws FileNotFoundException {
			br = new BufferedReader(new FileReader(new File(s)));
		}

		String next() {
			while (st == null || !st.hasMoreElements()) {
				try {
					st = new StringTokenizer(br.readLine());
				} catch (IOException e) {
					e.printStackTrace();
				}
			}
			return st.nextToken();
		}

		int nextInt() {
			return Integer.parseInt(next());
		}

		long nextLong() {
			return Long.parseLong(next());
		}

		double nextDouble() {
			return Double.parseDouble(next());
		}

		String nextLine() {
			String str = "";
			try {
				str = br.readLine();
			} catch (IOException e) {
				e.printStackTrace();
			}
			return str;
		}
	}
}

```
