---
layout: post
title: "백준 2661번 좋은수열"
categories:
  - algorithm
tags:
  - 알고리즘
  - 백준
  - 백트래킹
---

### 문제 링크
<https://www.acmicpc.net/problem/2661>

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {
    static int N;

    public static void main(String[] args) throws NumberFormatException, IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        N = Integer.parseInt(br.readLine());

        String list = "1";
        getList(list, 1);
    }

    static boolean check(String list) {
        for (int i = 1; i < (list.length() / 2) + 1; i++) {
            if (list.substring(list.length() - i, list.length())
                    .equals(list.substring(list.length() - (i * 2), list.length() - i))) {
                return false;
            }
        }
        return true;
    }

    static void getList(String list, int count) {
        if (count == N) {
            System.out.println(list);
            System.exit(0);
        }
        for (int i = 1; i < 4; i++) {
            if (check(list + i)) {
                getList(list+i, count + 1);
            }
        }
    }
}

```