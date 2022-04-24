# ACM Craft

[문제](https://www.acmicpc.net/problem/1005)

```java
import java.io.BufferedReader;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

public class Main {
	static StringBuilder sb = new StringBuilder();
	static FastReader scan = new FastReader();

	static int N, M, Q, W;
	static int[] T, T_done, indeg;
	static ArrayList<Integer>[] adj;

	static void input() {
		N = scan.nextInt();
		M = scan.nextInt();
		T = new int[N + 1];
		T_done = new int[N + 1];
		indeg = new int[N + 1];
		adj = new ArrayList[N + 1];

		for (int i = 1; i <= N; i++) {
			adj[i] = new ArrayList<>();
		}

		for (int i = 1; i <= N; i++) {
			T[i] = scan.nextInt();
		}
		for (int i = 1; i <= M; i++) {
			int x = scan.nextInt();
			int y = scan.nextInt();
			adj[x].add(y);
			indeg[y]++;
		}
		W = scan.nextInt();
	}

	static void pro() {
		Queue<Integer> que = new LinkedList<>();

		for (int i = 1; i <= N; i++) {
			if (indeg[i] == 0) {
				T_done[i] = T[i];
				que.add(i);
			}
		}

		while (!que.isEmpty()) {
			int x = que.poll();

			for (int y : adj[x]) {
				indeg[y]--;
				if (indeg[y] == 0) {
					que.add(y);
				}
				T_done[y] = Math.max(T_done[y], T_done[x] + T[y]);
			}
		}

		System.out.println(T_done[W]);
	}

	public static void main(String[] args) {
		Q = scan.nextInt();

		for (int i = 0; i < Q; i++) {
			input();
			pro();
		}
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
