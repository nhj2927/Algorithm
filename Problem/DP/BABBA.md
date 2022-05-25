# BABBA

[문제](https://www.acmicpc.net/problem/9625)

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

	static int K;
	static int[][] Dy;

	static void input() {
		K = scan.nextInt();
		Dy = new int[K + 1][2];
	}

	static void pro() {
		Dy[0][0] = 1;

		for (int i = 1; i <= K; i++) {
			Dy[i][0] = Dy[i - 1][1];
			Dy[i][1] = Dy[i - 1][0] + Dy[i - 1][1];
		}

		System.out.println(Dy[K][0] + " " + Dy[K][1]);
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
