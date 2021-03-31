---
layout: post
title: "프로그래머스 소수 찾기"
categories:
  - algorithm
tags:
  - 알고리즘
  - 프로그래머스
  - 완전탐색
---

### 문제 링크
<https://programmers.co.kr/learn/courses/30/lessons/42839>

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.HashSet;

class Solution {
    static int[] arr = { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 };
    static HashSet<Integer> set1 = new HashSet<Integer>();
    
    public int solution(String numbers) {
        
        for (int i = 0; i < numbers.length(); i++) {
            int num = Character.getNumericValue(numbers.charAt(i));
                
            if (num== 0)
                arr[0]++;
            else if (num== 1)
                arr[1]++;
            else if (num == 2)
                arr[2]++;
            else if (num == 3)
                arr[3]++;
            else if (num == 4)
                arr[4]++;
            else if (num == 5)
                arr[5]++;
            else if (num == 6)
                arr[6]++;
            else if (num == 7)
                arr[7]++;
            else if (num == 8)
                arr[8]++;
            else if (num == 9)
                arr[9]++;
        }

        func(arr, 0, "");
        int answer = set1.size();
        return answer;
    }
    
    static void func(int[] arr, int count, String str) {
        if(str.equals("0")){
            return;
        }
        if(str==""){

        }else if(Integer.parseInt(str)==2){
            set1.add(Integer.parseInt(str));
        }else if (Integer.parseInt(str)%2!=0 && check(Integer.parseInt(str))) {
            set1.add(Integer.parseInt(str));
        }

        if (arr[0] > 0) {
            arr[0]--;
            func(arr, count + 1, str + 0);
            arr[0]++;
        }
        if (arr[1] > 0) {
            arr[1]--;
            func(arr, count + 1, str + 1);
            arr[1]++;
        }
        if (arr[2] > 0) {
            arr[2]--;
            func(arr, count + 1, str + 2);
            arr[2]++;
        }
        if (arr[3] > 0) {
            arr[3]--;
            func(arr, count + 1, str + 3);
            arr[3]++;
        }
        if (arr[4] > 0) {
            arr[4]--;
            func(arr, count + 1, str + 4);
            arr[4]++;
        }
        if (arr[5] > 0) {
            arr[5]--;
            func(arr, count + 1, str + 5);
            arr[5]++;
        }
        if (arr[6] > 0) {
            arr[6]--;
            func(arr, count + 1, str + 6);
            arr[6]++;
        }
        if (arr[7] > 0) {
            arr[7]--;
            func(arr, count + 1, str + 7);
            arr[7]++;
        }
        if (arr[8] > 0) {
            arr[8]--;
            func(arr, count + 1, str + 8);
            arr[8]++;
        }
        if (arr[9] > 0) {
            arr[9]--;
            func(arr, count + 1, str + 9);
            arr[9]++;
        }
    }
    static boolean check(int n){
        if(n==0 || n==1) return false;
        for(int i=3; i<=(int)Math.sqrt(n); i+=2){
            if(n%i==0) return false;
        }
        return true;
    }
    
}
```