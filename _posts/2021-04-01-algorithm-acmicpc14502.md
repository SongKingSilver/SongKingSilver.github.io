---
layout: post
title: "백준 14502번 연구소"
categories:
  - algorithm
tags:
  - 알고리즘
  - 백준
  - bfs
  - 완전탐색
---

### 문제 링크
<https://www.acmicpc.net/problem/14502>

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;
import java.awt.Point;

public class Main3 {
    static int n, m, max;
    static int[][] map;
    static int[][] visited;
    static int[] dx = { 1, -1, 0, 0 }; // 좌표 비교용
    static int[] dy = { 0, 0, 1, -1 };

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        n = Integer.parseInt(st.nextToken()); //가로
        m = Integer.parseInt(st.nextToken()); //세로
        map = new int[n][m];    //2차원 맵
        visited = new int[n][m];  //방문체크
        for (int i = 0; i < n; i++) {  // 맵입력
            StringTokenizer input = new StringTokenizer(br.readLine());
            for (int j = 0; j < m; j++) {
                map[i][j] = Integer.parseInt(input.nextToken());
            }
        }

        sol(0); //시작
        System.out.println(max);
    }

    static void sol(int depth) {
        int count = 0; //카운트
        if (depth == 3) {  //벽 3개 세웟을경우
            for (int i = 0; i < n; i++) {  
                for (int j = 0; j < m; j++) {
                    if (visited[i][j] == 0 && map[i][j] == 2) {  //다 돌면서 방문 안되있고 바이러스가 있는 위치에서 전염ㄱㄱ
                        bfs(i, j);
                    }
                }
            }

            for (int i = 0; i < n; i++) {
                for (int j = 0; j < m; j++) {
                    if (map[i][j] == 0) {
                        count++;
                    }
                }
            }
            if (count > max) {
                max = count;
            }

            for (int i = 0; i < n; i++) {
                for (int j = 0; j < m; j++) {
                    if (map[i][j] == 2 && visited[i][j] == 1) {
                        map[i][j] = 0;
                        visited[i][j] = 0;
                    }
                }
            }
            return;
        }

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (map[i][j] == 0) {
                    map[i][j] = 1;
                    sol(depth + 1);
                    map[i][j] = 0;
                }
            }
        }
    }

    static void bfs(int x, int y) {
        Queue<Point> que = new LinkedList<>();  //큐 ㄱ
        que.offer(new Point(x, y));  //자신의 위치

        int nx, ny;

        while (!que.isEmpty()) {
            Point now = que.poll();

            for (int i = 0; i < 4; i++) {
                nx = now.x + dx[i];
                ny = now.y + dy[i];

                if ((nx < n && nx >= 0) && (ny < m && ny >= 0)) { //유효성 - 맵 밖으로 빠져 나가지 않게-
                    if (map[nx][ny] == 0) {  // 빈곳이라면 
                        que.offer(new Point(nx, ny)); //큐에 넣고
                        visited[nx][ny] = 1; //방문체크 - 나중에 다시 전염 안된 상태로 돌릴려고 저장
                        map[nx][ny] = 2; //전염
                    }
                }
            }
        }

    }

}

```