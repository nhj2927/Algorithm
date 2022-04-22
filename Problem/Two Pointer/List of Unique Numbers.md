# List of Unique Numbers

[문제]()

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
	static FastReader scan = new FastReader();

	static void input() {
		N = scan.nextInt();
		nums = new int[N + 1];
		for (int i = 1; i <= N; i++) {
			nums[i] = scan.nextInt();
		}
	}

	static void pro() {
		long ans = 0;
		int[] cnt = new int[100001];

		int R = 1;
		for (int L = 1; L <= N; L++) {
			while (R <= N && cnt[nums[R]] == 0) {
				cnt[nums[R++]]++;
			}
			cnt[nums[L]]--;
			ans += R - L;
		}

		System.out.println(ans);
	}

	static int N;
	static int[] nums;

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
