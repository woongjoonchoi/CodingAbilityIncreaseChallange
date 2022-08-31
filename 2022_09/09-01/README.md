# 프로그래머스-고득점 kit (아이템줍기)

Implementation - https://github.com/woongjoonchoi/CodingTest/blob/main/programeers/Programmers/%EC%95%84%EC%9D%B4%ED%85%9C%EC%A4%8D%EA%B8%B0.py

## Problem Definition
 Single Source Shortest Path  

## Solution

문제를 풀기위해선 graph path 알고리즘을 사용해야하는데, undirected, unweighted graph이므로 BFS 알고리즘을 적용해도 괜찮다.   

이 때 , node랑 edge를 정의해야하는데 , node는 물리적인 위치정보인 2d-grid로 정의하고 , edge는 외곽 선으로 정의한다.  



## Question

### 1 . Node를 2d-grid위의 모든  점이 아닌, edge의 꼭지점들로 정의하면 더 효율적인 알고리즘을 짤 수 있는것이 아닌가?

### A.  
맞는 말이다. 하지만, 어떤 node가 인접 노드인지 따로 matrix나 list를 만들어주어야 하는 불편함이 있다. 


### 2. 간격이 1인 node 가 있으면, 인접 node는 연결이 되어있을수도 아닐수 도 있다.하지만, 2d array상에서는 edge가 있다고 표현이 된다.  어떻게 처리하는가?

### A . 
grid를 2배  확장하는 선형변환을 적용하여 , 실제로 간격이 있도록 적용해준다.