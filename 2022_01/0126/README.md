## Baekjoon 7490

구현링크 : [CodingTest/Baekjoon/7490 at main · woongjoonchoi/CodingTest (github.com)](https://github.com/woongjoonchoi/CodingTest/tree/main/Baekjoon/7490)

### 1.Solution

매 iteration 마다 식을 직접 계산

![image](https://user-images.githubusercontent.com/50165842/151153108-e531cd00-d835-427a-8856-4893afb19b34.png)

### 2.Solution

매 iteration 마다 식을 구성

식을 전부 구성 후 계산



![image](https://user-images.githubusercontent.com/50165842/151153410-4e6167e2-6946-43cc-b456-02b6b3de09bf.png)





## 1 vs 2

1 번과 2번의 차이는 Tail Call Optimization 이라 보면 된다. 

1번은 iteration 마다 operation 한 value를 다음 iteration 에 넘겨주지만

2 번은 iteration 을 base case 가 될 때 까지 진행한후 다시 돌아 오는 과정을 거치는 것과 유사하기에  optimization 이 되지못한

recursion이다.