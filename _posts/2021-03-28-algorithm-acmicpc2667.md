---
layout: post
title: "백준 2667번 문제 단지번호붙이기(bfs)"
categories:
  - algorithm
tags:
  - 알고리즘
  - 백준
  - bfs
---
### 문제 링크
<a href=https://www.acmicpc.net/problem/2667>
https://www.acmicpc.net/problem/2667
</a>

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.LinkedList;
import java.util.Queue;
import java.util.Scanner;
import java.awt.Point;

public class Main {
    static int[] dx = { 1, -1, 0, 0 }; // 좌표 비교용
    static int[] dy = { 0, 0, 1, -1 };
    static boolean[][] visited = new boolean[25][25]; // 방문체크
    static int[][] map = new int[25][25]; // 맵크기
    static int N;
    static ArrayList danJi = new ArrayList();
    private static boolean add;

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
                    bfs(i,j);
                }
            }
        }

        System.out.println(danJi.size());
        Collections.sort(danJi);

        for (int i = 0; i < danJi.size(); i++) {
            System.out.println(danJi.get(i));
        }
    }

    static void bfs(int x, int y) {
        int nx, ny;
        int danjiSize = 1;
        visited[x][y] = true;
        Queue<Point> que = new LinkedList<>();
        que.offer(new Point(x, y));

        while (!que.isEmpty()) {
            Point now = que.poll();

            for (int i = 0; i < 4; i++) {
                nx = now.x + dx[i];
                ny = now.y + dy[i];
                    // x                     //y
                if ((nx < N && nx >= 0) && (ny < N && ny >= 0)) {
                    if(map[nx][ny] == 1 && visited[nx][ny]==false){
                        que.offer(new Point(nx,ny));
                        visited[nx][ny] = true;
                        danjiSize++;
                    }
                }

            }
        }
        danJi.add(danjiSize);
    }
}
```