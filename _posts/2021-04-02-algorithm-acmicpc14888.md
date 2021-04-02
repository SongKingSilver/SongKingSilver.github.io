---
layout: post
title: "백준 14888번 연산자 끼워넣기"
categories:
  - algorithm
tags:
  - 알고리즘
  - 백준
  - 백트래킹
  - 완전탐색
---

### 문제 링크
<https://www.acmicpc.net/problem/14888>

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class ex005 {
    static int N;
    static int max = -1000000000;
    static int min = 1000000000;

    public static void main(String[] args) throws NumberFormatException, IOException {
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));

        N = Integer.parseInt(in.readLine());

        int[] arr = new int[N];
        StringTokenizer st = new StringTokenizer(in.readLine());
        int[] oper = new int[4];
        for (int i = 0; i < N; i++) {
            arr[i] = Integer.parseInt(st.nextToken());
        }
        st = new StringTokenizer(in.readLine());
        for (int i = 0; i < 4; i++) {
            oper[i] = Integer.parseInt(st.nextToken());
        }
        func(arr, oper, 1, arr[0]);
        System.out.println(max);
        System.out.println(min);
    }

    static void func(int[] arr, int[] oper, int count, int value) {
        if (count == N) {
            if (value > max)
                max = value;
            if (value < min)
                min = value;
            return;
        }
        if (oper[0] > 0) {
            oper[0]--;
            func(arr, oper, count + 1, value + arr[count]);
            oper[0]++;
        }
        if (oper[1] > 0) {
            oper[1]--;
            func(arr, oper, count + 1, value - arr[count]);
            oper[1]++;
        }
        if (oper[2] > 0) {
            oper[2]--;
            func(arr, oper, count + 1, value * arr[count]);
            oper[2]++;
        }
        if (oper[3] > 0) {
            oper[3]--;
            func(arr, oper, count + 1, value / arr[count]);
            oper[3]++;
        }
    }
}


```