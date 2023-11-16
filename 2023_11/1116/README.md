# Mini-batch shuffle implementation


## First Solution

mini-batch size만큼의 array를 memory 에 allocation 후 이 array가 input을 pointing 하게 함.

## Inefficiency

매번 memory를 할당 하므로 memory 활용에 있어서 비효율 적이다. 왜냐하면, 이미 input에 대한 memory가 할당되어 있기 때문이다.

## Improved Solution

mini-batch size만큼의 permutation index list를 생성후 , 이러한 index순서를 가진 input의 view를 생성한다.
그리고, mini_batch name들이 이를 pointing 하게 한다.

이렇게 하면 , 새로운 memory를 추가적으로 할당하지 않는다.

![image](https://github.com/woongjoonchoi/woongjoonchoi.github.io/assets/50165842/f386f0a0-8798-4dbd-b761-7f6befef690b)


![image](https://github.com/woongjoonchoi/woongjoonchoi.github.io/assets/50165842/94cebda6-959e-40c7-b927-650b71533b23)




