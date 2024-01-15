# Special Stack

special stack의 solution을 scratch부터 구현하는 과정을 설명해보이겠다. 

## Problem Definition

어떤 data structure를 구현하라 한다. 이 data structure는 Stack이라는 DataStructure의 모든 operation을 지원하면서, min이라는 operation을  time upperbound가 O(1)이 되도록 구현한다.   

## From Scratch 

이는 Stack이랑은 다른 operation이 존재하므로 stack이 아닌다. 따라서, 임의의 data structure라고 설정하겠다.  

원소가 1개 4가 저장된다면, 

DS :  4  
최솟값: 4

원소가 또 이어서 5가 저장된다면 , 

DS : 4 5
최솟값 : 5

원소가 또 이어서 2이 저장된다면

DS: 4 2 5
최솟값 : 2  

위와 같은 식으로 전개가 된다. Stack의 operation을 지원해야 하므로 stack의 data structure를 그대로 차용해본다.  
만약에 , 원소가 삭제된다면 최솟값의변경이 생길 수 있다. 이 때마다 최솟값을 다시 찾아서 설정해야 한다면, 다른 operation의 UpperBound가 늘어날 것이다.따라서, 각 element에 min값이 1대1로 mapping이 되어있다면, 1대1 function의 return의 upperbound는  O(1) 이므로, min operation의 upperbound는 O(1)이 된다. 하지만, Auxiliary Space의 upperbound는 O(n)이 된다.  

## Little Optimization

1 대1 mapping 관계가 N개가 존재하는데, 이를 약간 줄여보도록 한다. N개의 mapping을 관찰하면 min 값이 변하는 순간은 element가 min값과 같은 순간이다. 이는 새로운 element가 min이 되거나 기존의 min element가 나가는 순간이다.  
element가 min과 같아지는 순간을 기준으로 1:1 mapping에서 N:1 mapping으로변화한다면 치역의 갯수를 줄일 수 있다.  UpperBound는 O(n)이지만 average는 충분히 감소할 것이다.   


## Space Optimization

여전히 space의 upperbound가 O(N)이다.  이를 O(1)으로 줄일려면  치역을 할당하면 안된다. mapping관계를 유지하면서 치역을 없애야 하는데,  즉, 추가적인 space의 upperbound가 mapping관계의 치역, 즉 min값에 할당되서는 안된다.하지만, min operation의 time upperbound는 O(1)이라는 것은 mapping관계가 유지가 된다, 즉  치역이 존재한다는 뜻이다.  추가적인 space upperbound에  치역을 할당하지 않으면서, 치역이 존재하기 위해서는 기존의 stack element가 치역이 되어야한다.   

여태 까지는 stack의 element를 함수의 parameter(or key)로 사용하여 특정 value를 return 시켰는데, 이제는 stack의 element가 함수의 return값이 되어야 한다.  
우리가 알아야 하는 값은 stack의 element와 바뀌게 되는 min_value이다.   
이에 대해서는 두 가지 방법이 잇다.  

### Return element, min_value 

우리는 2가지 value를 return하는 function을 이미 하나 알고있다. 바로 나누기 함수이다. 이는 몫,나머지를 반환한다.  제수를 stack의 element 범위보다 크거나 작게 설정한다면 모든 stack의 element 범위의 값을 return할 수 있을 것이다.  
```
f() = ele *d + min
```
하지만, 이는 element의 범위에 따라 bit수가 초과할 수 있다. 파이썬의 경우는 arbitary precision을 지원하지만,다른 language의 경우  지원하지 않을 수도 있다. 좀 더 넓은 범위의 precision을 지원하는 방법을 간구하는게 편하다. 

### return element 

key값으로 min값을 사용하면 min 값 하나에 대해서 element를 return하는 function을 만들면 됩니다. 하지만, min값이랑 element가 같아지는 순간 바뀌는 min을 알아야 하므로 아래와 같이 function을 조건을 나누면 될거 같습니다. 
```
f(min)  = element   ( element >min)
        = ??        (?? )
```

단순히 element를 return하게 되면 새로바 뀌는 min값에 대한 정보가 없으므로 , 이전 min에 대한 정보가 있으면 좋을거 같습니다. 이전 min을 min_p라 하겠습니다.  
만약에 ele-min_p라는 return값을 사용한다 하겠습니다. ele-min_p는 min-min_p와 동일하므로 0보다 작은 값이 나옵니다. 하지만, 이는 element가 마이너스인 순간을 filtering 하지 못하므로 사용할 수 없습니다.  
따라서, 좀 더 명확하게 , ele - (min_p-ele) 라는 값을 사용한다면 이는 항상 min값보다 작을 것입니다. 이는 min값에 대하여 항상 유일한 경우입니다. 
min값이랑 element가 같아지는 순간에 min_p를 return할 수 있고, ele 는 min이므로 min을 return하면 됩니다. 
이러한 경우 , 2**30의 범위내의 숫자들은 overflow가 발생하지 않을 것입니다. 
