---
layout: post
title: "백준 14889번 스타트와 링크"
categories:
  - algorithm
tags:
  - 알고리즘
  - 백준
  - 완전탐색
  - 백트래킹
---

### 문제 링크
<https://www.acmicpc.net/problem/14889>


```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class ex003 {
    static int N;
    static int[][] s;
    static int min = 100;

    public static void main(String[] args) throws NumberFormatException, IOException {
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(in.readLine());

        s = new int[N][N];
        boolean[] team = new boolean[N];
        int[] temp = new int[N + 1];

        for (int i = 1; i <= N; i++) {
            temp[i] = i;
        }

        for (int i = 0; i < N; i++) {
            StringTokenizer st = new StringTokenizer(in.readLine());
            for (int j = 0; j < N; j++) {
                s[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        func(team, temp, 0,0);
        System.out.println(min);
    }

    static void func(boolean[] team, int[] temp, int count,int start) {

        int new_max = 0;
        int a_max = 0;
        int b_max = 0;
        if (count == N / 2) {
            for (int i = 0; i < N; i++) {
                if (!team[i]) {
                    for (int j = 0; j < N; j++) {
                        if (!team[j]){
                            a_max += s[temp[i]][temp[j]];
                        }
                    }
                }
            }
            for (int i = 0; i < N; i++) {
                if (team[i]) {
                    for (int j = 0; j < N; j++) {
                        if (team[j]){
                            b_max += s[temp[i]][temp[j]];
                        }
                    }
                }
            }
            new_max = Math.abs(a_max - b_max);

            min = Math.min(new_max, min);
            return;
        }

        for (int i = start; i < N; i++) {
            if (!team[i]) {
                team[i] = true;
                func(team, temp, count + 1,i+1);
                team[i] = false;
            }
        }
    }
}
```