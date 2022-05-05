# RGB 거리

[문제](https://www.acmicpc.net/problem/1149)

```java
import java.io.BufferedReader;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;
import java.util.StringTokenizer;

public class Main {
	static StringBuilder sb = new StringBuilder();
	static FastReader scan = new FastReader();

	static int N;
	static int[][] Dy, prev, cost;

	static void input() {
		N = scan.nextInt();

		Dy = new int[N + 1][3];
		cost = new int[N + 1][3];

		for (int i = 1; i <= N; i++) {
			cost[i][0] = scan.nextInt();
			cost[i][1] = scan.nextInt();
			cost[i][2] = scan.nextInt();
		}
	}

	static void pro() {
		Dy[1][0] = cost[1][0];
		Dy[1][1] = cost[1][1];
		Dy[1][2] = cost[1][2];

		for (int i = 2; i <= N; i++) {
			for (int j = 0; j < 3; j++) {
				Dy[i][j] = Integer.MAX_VALUE;

				for (int k = 0; k < 3; k++) {
					if (j == k)
						continue;

					Dy[i][j] = Math.min(Dy[i][j], Dy[i - 1][k] + cost[i][j]);
				}
			}
		}

		int ans = Dy[N][0];
		for (int i = 1; i < 3; i++) {
			ans = Math.min(ans, Dy[N][i]);
		}
		System.out.println(ans);
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
