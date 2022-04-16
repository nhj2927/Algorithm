# NQueen

[문제](https://www.acmicpc.net/problem/9663)

```java
import java.io.BufferedReader;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;
import java.util.Arrays;
import java.util.StringTokenizer;

public class Main {
	static StringBuilder sb = new StringBuilder();

	static void input() {
		FastReader scan = new FastReader();
		N = scan.nextInt();
		col = new int[N + 1];
		col[0] = -1;
	}

	static boolean attackable(int r1, int c1, int r2, int c2) {
		if (c1 == c2) {
			return true;
		}
		if (Math.abs(r1 - r2) == Math.abs(c1 - c2)) {
			return true;
		}
		return false;
	}

	static void rec_func(int row) {
		if (row == N + 1) {
			ans++;
		} else {
			for (int i = 1; i <= N; i++) {
				boolean possible = true;
				for (int j = 1; j < row; j++) {
					if (attackable(row, i, j, col[j])) {
						possible = false;
						break;
					}
				}
				if (possible) {
					col[row] = i;
					rec_func(row + 1);
					col[row] = 0;
				}
			}
		}
	}

	static int N, ans;
	static int[] col;

	public static void main(String[] args) {
		input();
		rec_func(1);
		System.out.println(ans);
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
