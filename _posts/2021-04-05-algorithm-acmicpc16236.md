---
layout: post
title: "백준 16236번 문제 아기상어"
categories:
  - algorithm
tags:
  - 알고리즘
  - 백준
  - bfs
---
### 문제 링크
<https://www.acmicpc.net/problem/16236>

채점을 하니 틀렸다고 나온다 왜그런건지 모르겠다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;
import java.awt.Point;

public class ssss {
    static Point bsPoint = new Point();
    static int[][] map;
    static int[] dx = {1,-1,0,0};
    static int[] dy = {0,0,-1,1};
    static int sS = 2;
    static int exp = 0;
    static int sumTime=0;
    static int n;
    

    public static void main(String[] args) throws NumberFormatException, IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        n = Integer.parseInt(br.readLine());
        map = new int[n][n];
        for (int i = 0; i < n; i++) {
        StringTokenizer input = new StringTokenizer(br.readLine());
            for (int j = 0; j < n; j++) {
                map[i][j] = Integer.parseInt(input.nextToken());
                if (map[i][j]==9) {
                    map[i][j]=0;
                    bsPoint.setLocation(i, j);
                }
            }
        }
        for(;;){
            bsPoint=scanMaps(bsPoint.x,bsPoint.y);
            if(bsPoint.x==-1){
                System.out.println(sumTime);
                break;
            }
        }
    }

    static Point scanMaps(int x, int y){
        Queue<Point> que = new LinkedList<>();
        int[][] visited= new int[n][n];
        visited[x][y]=1;
        int[][] dis= new int[n][n];
        que.offer(new Point(x,y));
        int nx,ny;
        
        while(!que.isEmpty()){
            Point now = que.poll();

            for (int i = 0; i < 4; i++) {
                nx = now.x + dx[i];
                ny = now.y + dy[i];
                if ((nx < n && nx >= 0) && (ny < n && ny >= 0)) { 
                    if((map[nx][ny]==0 || sS == map[nx][ny]) && visited[nx][ny]==0){
                        que.offer(new Point(nx, ny));
                        dis[nx][ny] = dis[now.x][now.y] + 1;
                        visited[nx][ny]= 1;
                    }
                    if(sS > map[nx][ny] && map[nx][ny]!=0 && visited[nx][ny]==0){
                        dis[nx][ny] = dis[now.x][now.y] + 1;
                        visited[nx][ny]= 2;
                    }
                }
            }
        }
        int min=100;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if(visited[i][j]==2 && dis[i][j]<min){
                    min = dis[i][j];
                }
            }
        }
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if(visited[i][j]==2 && dis[i][j]==min){
                    map[i][j]=0;
                    sumTime+=dis[i][j];
                    exp++;
                    if(exp==sS){
                        exp=0;
                        sS++;
                    }
                    return new Point(i,j);
                }
            }
        }
        return new Point(-1,-1);
    }
}

```