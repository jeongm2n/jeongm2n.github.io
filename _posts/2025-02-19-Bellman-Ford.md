---
layout: post
categories: algorithm
title: "[알고리즘] 벨만 포드 (Bellman-Ford)"
---

<br>

# 벨만 포드 (Bellman-Ford)

<br>
<br>

## 벨만 포드란?

<p>
그래프에서 최단 경로를 구하는 데에 사용되는데, 음수 가중치가 존재할 때 사용할 수 있는 알고리즘이다. <br>
다익스트라와 플로이드 워셜은 가중치가 양수일 때만 사용 가능하다는 차이가 있다. <br>

<br>

단, 음수 사이클이 없는 경우에만 벨만-포드 알고리즘을 통해 최단 경로를 구할 수 있다.<br>
음수 사이클이 존재하는 경우에는 벨만-포드 알고리즘을 통해 음수 사이클이 존재함을 확인할 수 있다.<br>
</p>

<br>
<br>

## 벨만 포드의 과정

<br>

1. 특정 노드를 출발점으로 설정하고 N-1번의 반복으로 모든 간선을 확인하며 dist[] 배열의 값을 갱신한다.
2. 한 번 더 모든 간선을 확인하며 dist[] 배열의 값이 갱신되는지 확인하고 갱신되면 음수 사이클 존재, 아니면 음수 사이클이 없는 것이다.

<br>

or

<br>

1. 특정 노드를 출발점으로 설정하고 N번의 반복으로 모든 간선을 확인하며 dist[] 배열의 값을 갱신한다.
2. 만약 N번째에도 dist[] 배열의 값에 갱신된다면 음수 사이클이 존재, 아니라면 음수 사이클이 없는 것이다.

<br>
<br>

<img width="100%" alt="Image" src="https://github.com/user-attachments/assets/5c52c446-6792-4abe-b0fd-51b4c200710e" />

<br>

위와 같은 그래프가 있다고 가정해보자. (음수 사이클이 없는 경우) 
<br>

처음 dist[] 배열은 INF(Integer.MAX_VALUE)로 설정한다.

<br>

> 간선 정보
> - 1 -> 2 = 6
> - 1 -> 3 = 7
> - 2 -> 3 = 8
> - 2 -> 4 = 5
> - 2 -> 5 = -4
> - 3 -> 4 = -3
> - 4 -> 5 = 9

<br>
<br>

반복문의 첫 번째에서 dist[] 값이 갱신되는 것을 확인해보자.<br>

<br>

정점 1을 출발점으로 지정하고 간선을 확인해보자.
```
dist[1] = 0;
```

<br>
<br>

1️⃣
<img width="100%" alt="Image" src="https://github.com/user-attachments/assets/d0841fb3-95db-4cc7-890f-751a52158ce1" />

<br>

1 -> 2 (6) <br>
1 -> 3 (7)

두 간선으로 먼저 dist[]의 값을 갱신한다.

|   | 1 | 2 | 3 | 4 | 5 |
|:---:|:---:|:---:|:---:|:---:|:---:|
|dist|0|6|7|INF|INF|

<br>
<br>

2️⃣
<img width="100%" alt="Image" src="https://github.com/user-attachments/assets/2e51c717-b9a6-487f-8e30-2fd3cf8f9be8" />

<br>

2 -> 3 (8) <br>
2 -> 4 (5) <br>
2 -> 5 (-4)<br>

세 간선으로 dist[]의 값을 갱신한다.

<br>

2 -> 3 간선의 경우 이미 dist[3]의 값이 7인데 1 -> 2 -> 3으로 가는 경우는 14의 가중치로 더 크기 때문에 dist[3]의 값은 갱신되지 않는다.

|   | 1 | 2 | 3 | 4 | 5 |
|:---:|:---:|:---:|:---:|:---:|:---:|
|dist|0|6|7|11|2|

<br>
<br>

3️⃣
<img width="100%" alt="Image" src="https://github.com/user-attachments/assets/0fa2ae77-a327-4369-b019-d81d237bb154" />


<br>

3 -> 4 (-3) <br>

위 간선으로 dist[]의 값을 갱신한다.

<br>

dist[3]+(-3)이 기존의 dist[4]=11 보다 작으므로 값을 갱신한다.

|   | 1 | 2 | 3 | 4 | 5 |
|:---:|:---:|:---:|:---:|:---:|:---:|
|dist|0|6|7|4|2|

<br>
<br>

4️⃣
<img width="100%" alt="Image" src="https://github.com/user-attachments/assets/3627b625-951c-4ed4-92ab-caf36098c907" />

<br>

4 -> 5 (9) <br>

위 간선으로 dist[]의 값을 갱신한다.

<br>

dist[4]+9가 기존의 dist[5]=2 보다 크므로 값을 갱신하지 않는다.

<br>
<br>

위 과정 후 모든 간선에 대한 반복문을 한 번 더 돌려서 dist[] 배열에서 갱신되는 값이 있다면 음수 사이클이 존재하는 것이다.

<br>
<br>

## JAVA 코드

```java
package Dijkstra.Bellman;

import java.io.*;
import java.util.*;

public class prac {
    static int N, M;
    static final int INF = Integer.MAX_VALUE;
    static ArrayList<Edge> edges = new ArrayList<>();

    static class Edge{
        int s, e, w;
        public Edge(int s, int e, int w){
            this.s = s;
            this.e = e;
            this.w = w;
        }
    }

    static void bellman(){
        int[] dist = new int[N+1];
        Arrays.fill(dist, INF);
        dist[1] = 0;

        boolean isCycle = false;

        for(int i=0; i<N-1; i++){ //최단 거리 갱신하는 반복문
            for(Edge edge : edges){
                int s = edge.s;
                int e = edge.e;
                int w = edge.w;

                if(dist[s]!=INF && dist[e]>dist[s]+w) dist[e] = dist[s]+w;
            }
        }

        for(Edge edge : edges){ //음수 사이클이 존재하는지 확인하는 반복문
            int s = edge.s;
            int e = edge.e;
            int w = edge.w;

            if(dist[s]!=INF && dist[e]>dist[s]+w){
                dist[e] = dist[s]+w;
                isCycle = true;
            }
        }

        System.out.println(isCycle ? "음수 사이클이 존재합니다!" : "음수 사이클이 존재하지 않습니다.");
    }

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        N = Integer.parseInt(st.nextToken());
        M = Integer.parseInt(st.nextToken());

        for(int i=0; i<M; i++){
            st = new StringTokenizer(br.readLine());

            int s = Integer.parseInt(st.nextToken());
            int e = Integer.parseInt(st.nextToken());
            int w = Integer.parseInt(st.nextToken());

            edges.add(new Edge(s, e, w));
        }

        bellman();
    }
}

```