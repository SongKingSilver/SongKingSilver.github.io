---
layout: post
title: "백준 2178번 미로 탐색"
categories:
  - algorithm
tags:
  - 알고리즘
  - 백준
  - bfs
---

### 문제 링크
<https://www.acmicpc.net/problem/2178>

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;
import java.awt.Point;

public class Main2 {
    static int[] dx = { 1, -1, 0, 0 }; // 좌표 비교용
    static int[] dy = { 0, 0, 1, -1 };
    static int[][] visited;
    static int n;
    static int m;
    static int[][] map;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        n = Integer.parseInt(st.nextToken());
        m = Integer.parseInt(st.nextToken());
        map = new int[n][m];
        visited = new int[n][m];
        visited[0][0] = 0;
        for (int i = 0; i < n; i++) {
            String input = br.readLine();
            for (int j = 0; j < m; j++) {
                map[i][j] = input.charAt(j) - '0';
            }
        }
        bfs(0, 0);
        System.out.println(visited[n-1][m-1]);
    }

    static void bfs(int x, int y) {
        Queue<Point> que = new LinkedList<>();
        visited[x][y] = 1;
        que.offer(new Point(x, y));

        int nx, ny;

        while (!que.isEmpty()) {
            Point now = que.poll();

            for (int i = 0; i < 4; i++) {
                nx = now.x + dx[i];
                ny = now.y + dy[i];

                if ((nx < n && nx >= 0) && (ny < m && ny >= 0)) {
                    if (map[nx][ny] == 1 && visited[nx][ny] == 0) {
                        que.offer(new Point(nx, ny));
                        visited[nx][ny] = visited[now.x][now.y] + 1;
                    }
                }
            }
        }
    }
}

```