# RotationArry

rotation array는 array의 element를 왼쪽으로 d만큼 움직이는 solution을 구하는 과정이다.   
이 문제만 놓고 보면 매우 단순하지만, 이를 일반적인 문제 S를 구하는 과정으로 치환하여 해결해볼려 한다.  
매우 어려운 문제를 풀듯이 문제를 풀어보면서 general 한 problem solving skill을 기르리라 예상된다.  

## Problem

정수 n과 정수 d가 길이 n의 array를 임의의 동작 S를 통해 길의 n의 array가 output으로 리턴된다. S를 구하여라. 

n=4 , d=1  $$ \rightarrow $$ [2,3,4,1]  

n=4 , d=2 $$ \rightarrow $$ [3,4,1,2]  

n=4 , d=3 $$ \rightarrow $$ [4,1,2,3]  

n=4 , d=4 $$ \rightarrow $$ [1,2,3,4]  

## Sol1
d=1일 떄 input에 동작 S를 통해 output이 도출된다. 
d=2의  solution은 d=1의 solution에 동작 S(d=1)를 적용하였고, d=3의 solution은 d=2이 solution에 동작 S(d=1)를 적용하였음을 관찰할 수 있다.  S(d=1) 을 f라 표기하겠다.  
즉, 동작 S는 recursive한 procedure이고 아래와 같이 정의될 수 있다.   
```
def S (array,steps)

    out = f(array)
    if steps == d:
        return out
    return S(out,steps+1)

```
S의 solution을 recursive한 solution이므로 iterative하게 바꿔 쓸 수 있다.

```

for i in range(d) :
    array= f(array)

```

Time Complexity : $$ O(N * D) $$  
Auxiliary Space Complexity : $$ O(1) $$
## Sol2 

Sol1을 최적화 해보도록 하겠다.  
Sol1은 f라는 동작을 계속 반복하는데 f라는 동작을 관찰하면 element과 왼쪽으로 1칸이 움직임을 알 수 있다.  
따라서, f라는 동작을 d번하면, element과 왼쪽으로 d만큼 움직이게 된다.  
```
array[x-d] = array[x]
```
위와 같은 관계가 성립하게 된다.  따라서, 각 원소를 위의 관계식에 대입하면 되지만 , 프로그래밍 언어상 앞의 d개의 element의 원소를 미리 copy해놓아야 d개의 state가 보존이 된다. 

Time Complexity : $$ O(N) $$  
Auxiliary Space Complexity : $$ O(D) $$


## sol3 

Sol2를 최적화 해보도록 하겠다.  
Sol2는 복원해야할 state가 d개가 되어 추가적인 space가 발생한다.  
```
array[x-d] = array[x]
```
array의 elemet를 이동시킬 때 추가적인 space가 발생하지 않으려면 array의 element를 1개만 이동시키면서 새로운 위치의 element를 기억해야한다.   
이를 잘 관찰하면, x에서 왼쪽으로 계속 d만큼 가게 되면 언젠가는 다시x의 위치에 도달하게 된다. 따라서, array의 element 1개를 계속 d만큼 이동하게 되면, 언젠간 제자리에 도달하게 된다. 즉, kd = mN이 된다면 , N칸 이동을 m번 반복하기에 제자리에 오게 된다.   단순하게 ,n번 반복해도 되겠지만, d,n의 lcm은 N,d를 약수로 가지는 가장 작은 수이므로 lcm을 구해주면 된다.  

Time Complexity : $$ O(N) $$  
Auxiliary Space Complexity : $$ O(1) $$


## Sol4 

n이 크다면 array는 엄청나게 긴 시퀸스가 될 것이다.  
긴 시퀸스를 해석하는 방법중 하나로 array를 두개의 큰 chunk로 이루어져 있다고 치환하여 단순하게 해석하는 것이다. 

output과 array의 공통된 부분을 각각 AB라 하겠다.  
array = AB 로 치환을 하겠다.  

AB를 BA로 바꾸는 S를 찾는게 문제이다. 시퀸스의 A,B를 각각 reverse시키면 Ar,Br이라 하자.   
(Ar)r = A , (Br)r = B라는 관계식이 성립하게 된다.  
(AB)r = BrAr 이 성립하게 된다.  
따라서, (ArBr)r = BA가 성립하는 시퀸스 opeartion을 얻게 된다.  

Time Complexity : $$ O(N) $$  
Auxiliary Space Complexity : $$ O(1) $$



