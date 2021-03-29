---
layout: post
title: "백준 10819번 문제 차이를 최대로"
categories:
  - algorithm
tags:
  - 알고리즘
  - 백준
  - dfs
---

### 문제 링크
<https://www.acmicpc.net/problem/10819>


```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class ex001_2 {

    static boolean np(int numbers[],int N) {
        //	1. 교차점 찾기 
            int i = N - 1;
        //	뒤쪽 부터 탐색하여 꼭대기(i) 찾기 
            while(i > 0 && numbers[i - 1] >= numbers[i]) i--;
                
        //	i = 0이면 순열 생성 못함 
            if(i == 0) return false;
                
        //	2. 교차할 데이터의 위치 찾기 
            int j = N - 1;
        //	뒤쪽 부터 탐색하여 교환할 큰값(j) 찾기 
            while(numbers[i - 1] >= numbers[j])	j--;
                
        //	3. i-1 번째 데이터와 j번째 데이터 교환 (swap)
            swap(numbers,i - 1, j);
                
        //	4. 다음 순열을 위해서 교환후 꼭지점 이후는 (index)를 내림차순으로 
            int k = N - 1;
            while(i < k) {
                    swap(numbers, i++, k--);			
            }
            return true;
        }
        static void swap(int numbers[], int i, int j) {
            int temp = numbers[i];
            numbers[i] = numbers[j];
            numbers[j] = temp;
        }

        static int getMax(int[] arr) {
            int sum = 0;
            for(int i = 0 ; i < arr.length - 1 ;i++) {
                sum += Math.abs(arr[i] - arr[i+1]);
            }
            return sum;
        }

        public static void main(String[] args) throws IOException {
            BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
            int N = Integer.parseInt(in.readLine());
            int[] arr = new int[N];
            StringTokenizer st = new StringTokenizer(in.readLine());
            int max=0;
            for(int i = 0 ; i < N ; i++) {
                arr[i] = Integer.parseInt(st.nextToken());
            }
            
            Arrays.sort(arr);
            do {
                if(max < getMax(arr)) max=getMax(arr);
            } while (np(arr,N));
            System.out.println(max);
        }
}
```