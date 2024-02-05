# Baekjoon 13460

[Link](https://www.acmicpc.net/problem/13460)  

## First Try

Vertex : Board  (n,m)

Edge : vertex 사이의 통로  

Source : Red  

Dest : Hole   

1. SSSP 문제라 정의하고 시작.  

2. Source에서 최단경로를 찾는 문제로 해결중

3. 최단경로로 움직이지 않고 최단 시간안에 도달할 수 있는 경로 밝견


## Second Try

Vertex : Board의 state

Edge : 각 Board에서 기울이는 4가지 방향.  
    Edge는 Blue 가 hole에 들어가거나 Red가 Hole에 들어간 vertex엔 존재하지 않는다.  !!!!    

Source : 초기의 Red, Blue의 위치

Dest : Red만이 Hole에 들어간 상황


Upper Bound : 81 C 2 (vetex)   
            81 C 2 * 4  (edge)  


BFS를 사용시 O(V+E) 임으로 괜찮은 upper bound 이다.  


1. SSSP문제로 정의하지만 Vertex,Edge를 바꿔준다.  

2.  Source에서 특정 state로의 최단경로를 찾는다.  


3.  level를 순차적으로 조회하면서 solution을 방문했는지 확인한다. 

4.  10 level 이내에 방문하지 못했을 경우 -1을 return 한다.



