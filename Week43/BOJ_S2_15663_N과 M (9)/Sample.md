#   [2023.10.09] BOJ_S2_15663_N과 M (9)
https://www.acmicpc.net/problem/15663

<접근법>

```
1. N개의 수 정렬
2. dfs 이용 m개의 수를 완전 탐색하여 선택할때 앞전에 이미 dfs를 수행한 숫자는 넘기기위해 temp 변수를 통해 중복된 수 넘김
```




```java
/**
 * 메모리  : 24800 KB
 * 시간   : 304 ms
 */
import java.util.Arrays;
import java.util.Scanner;

public class BJ_15663 {
    public static void main(String[] args) {
        try (Scanner sc = new Scanner(System.in)) {
            String[] inps = sc.nextLine().split(" ");
            int N = Integer.parseInt(inps[0]);
            int M = Integer.parseInt(inps[1]);

            int[] ns = Arrays.stream(sc.nextLine().split(" ")).mapToInt(Integer::parseInt).toArray();
            Arrays.sort(ns);

            StringBuilder answer = new StringBuilder();
            dfs(N, M, ns, 0, new int[M], new boolean[N], answer);

            System.out.println(answer);
        }
    }

    static void dfs(int N, int M, int[] ns, int depth, int[] sels, boolean[] isVisited, StringBuilder answer) {
        if (depth == M) {
            for (int i = 0; i < M; i++) {
                answer.append(sels[i]).append(" ");
            }
            answer.append("\n");
            return;
        }

        int temp = 0;
        for (int i = 0; i < N; i++) {
            // 선택하지 않았고 중복되지 않을 경우
            if (!isVisited[i] && temp != ns[i]) {
                isVisited[i] = true;
                sels[depth] = ns[i];
                temp = ns[i];
                dfs(N, M, ns, depth + 1, sels, isVisited, answer);
                isVisited[i] = false;
            }
        }
    }
}
```