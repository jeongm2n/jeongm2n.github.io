---
layout: post
categories: algorithm
title: "[알고리즘] 위상 정렬(Topological Sorting)"
---

<br>

# 위상 정렬(Topological Sorting)

<br>
<br>

## 위상 정렬이란?

<p>
그래프의 노드를 순서에 맞게 정렬하는 알고리즘이다. 쉽게 말하면 어떤 일을 순서에 따라 처리하는(?) 느낌이라고 할 수 있다.<br>
위상 정렬은 <span style="background-color:salmon">단방향</span>이면서 <span style="background-color:salmon">사이클이 없는</span> 그래프에서만 사용이 가능하다.<br>
</p>

<br>
<br>

## 위상 정렬 과정

<br>

<img width="100%" alt="Image" src="https://github.com/user-attachments/assets/efb7a481-29d2-4158-9273-6dfcd40f6e93" />

<br>

위와 같은 그래프가 있다고 가정하고 시작한다. (각 노드의 아래에 있는 숫자는 indegree[] 배열에 들어갈 값이다. 해당 노드를 가리키는 간선이 몇 개인지 나타내는 값이다.)

<br>

#### 1. indegree값이 0인 노드를 Queue에 삽입한다.

<br>

위의 그래프에선 가장 처음에 indegree가 0인 노드는 1뿐이다. 그래서 Queue에 1이 먼저 삽입된다.

<br>

<img width="100%" alt="Image" src="https://github.com/user-attachments/assets/150ebd73-c6a5-4204-b02d-b64aa04c089e" />

<br>

#### 2. Queue에서 가장 앞에 있는 노드를 빼내고 해당 노드의 간선이 연결하는 노드들의 indegree 값을 -1 한다.

<br>

노드 1과 연결된 노드는 2와 4이므로 2와 4의 indegree를 -1 한다.<br>
이 과정에서 4의 indegree가 0이 되었다. indegree가 0인 노드를 Queue에 삽입하므로 4를 Queue에 삽입한다.

<br>

<img width="100%" alt="Image" src="https://github.com/user-attachments/assets/32e01c00-0d11-47fd-88c3-7437390688bc" />

<br>
<br>

노드 4와 연결된 노드는 2이므로 2의 indegree를 -1 한다.<br>
이 과정에서 2의 indegree가 0이 되었으므로 2를 Queue에 삽입한다.

<br>

<img width="100%" alt="Image" src="https://github.com/user-attachments/assets/3f949ef9-505c-4c75-a13b-40931b1e7fc1" />

<br>
<br>

노드 2와 연결된 노드는 3과 5이므로 3, 5의 indegree를 -1 한다.<br>
이 과정에서 3의 indegree가 0이 되었으므로 3을 Queue에 삽입한다.

<br>

<img width="100%" alt="Image" src="https://github.com/user-attachments/assets/22b71c89-189c-4500-81a6-a8ec49afe2bf" />

<br>
<br>

노드 3과 연결된 노드는 5이므로 5의 indegree를 -1 한다.<br>
이 과정에서 5의 indegree가 0이 되었으므로 5를 Queue에 삽입한다.

<br>

<img width="100%" alt="Image" src="https://github.com/user-attachments/assets/82d22389-d20b-4fa9-b92b-200283382bbf" />

<br>
<br>

노드 5는 아무런 노드도 가리키지 않기 때문에 아무 일도 일어나지 않는다.

<br>

<img width="100%" alt="Image" src="https://github.com/user-attachments/assets/ac692229-3c5b-45d4-9a6d-42e06ed6d597" />

<br>
<br>

## Java 코드

<br>

```java
package Topology;

import java.io.*;
import java.util.*;

public class prac {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        int N = Integer.parseInt(st.nextToken()); //그래프 노드의 개수
        int M = Integer.parseInt(st.nextToken()); //간선의 개수

        ArrayList<Integer>[] graph = new ArrayList[N+1];
        for(int i=1; i<N; i++) graph[i] = new ArrayList<>();
        int[] indegree = new int[N+1];
        Queue<Integer> q = new LinkedList<>();

        for(int i=0; i<M; i++){ //그래프 입력받기
            st = new StringTokenizer(br.readLine());

            int u = Integer.parseInt(st.nextToken());
            int v = Integer.parseInt(st.nextToken());

            graph[u].add(v);
            indegree[v]++; //정점마다 indegree값 설정
        }

        for(int i=1; i<=N; i++){ //처음에 indegree가 0인 노드들을 모두 Queue에 삽입
            if(indegree[i]==0) q.offer(i); 
        }

        StringBuilder sb = new StringBuilder();

        while(!q.isEmpty()){
            int cur = q.poll();
            sb.append(cur + " ");

            for(int next : graph[cur]){
                indegree[next]--; //연결된 노드들의 indegree 값을 -1
                if(indegree[next]==0) q.offer(next);
            }
        }

        System.out.println(sb);
    }
}

```