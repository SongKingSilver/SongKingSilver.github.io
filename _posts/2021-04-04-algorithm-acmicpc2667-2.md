---
layout: post
title: "백준 2667번 문제 단지번호붙이기(dfs)"
categories:
  - algorithm
tags:
  - 알고리즘
  - 백준
  - dfs
---
### 문제 링크
<https://www.acmicpc.net/problem/2667>

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Scanner;

public class Main2 {
    static int[] dx = { 1, -1, 0, 0 }; // 좌표 비교용
    static int[] dy = { 0, 0, 1, -1 };
    static boolean[][] visited = new boolean[25][25]; // 방문체크
    static int[][] map = new int[25][25]; // 맵크기
    static int N,count;
    static ArrayList danJi = new ArrayList();

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in); // 입력 받기
        N = sc.nextInt();// 입력, 맵사이즈 N*N

        for (int i = 0; i < N; i++) {
            String input = sc.next();
            for (int j = 0; j < N; j++) {
                map[i][j] = input.charAt(j) - '0';
            }
        }

        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                if (visited[i][j] == false && map[i][j] == 1) {
                    count =1;
                    dfs(i, j);
                    danJi.add(count);
                }
            }
        }

        System.out.println(danJi.size());
        Collections.sort(danJi);

        for (int i = 0; i < danJi.size(); i++) {
            System.out.println(danJi.get(i));
        }
    }

    static void dfs(int x, int y) {
        int nx, ny;
        visited[x][y] = true;

        for (int i = 0; i < 4; i++) {
            nx = x + dx[i];
            ny = y + dy[i];
            // x //y
            if ((nx < N && nx >= 0) && (ny < N && ny >= 0)) {
                if (map[nx][ny] == 1 && visited[nx][ny] == false) {
                    dfs(nx,ny);
                    count++;
                }
            }

        }
    }
}
```