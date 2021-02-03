---
title: 프로그래머스 - 다리를 지나는 트럭
date: 2021-01-21 18:23:00 +/-TTTT
categories: [Algorithm, StackQueue]
tags: [programmers, stack, queue, algorithm]     # TAG names should always be lowercase
---
# 다리를 지나는 트럭
### 문제
트럭 여러 대가 강을 가로지르는 일 차선 다리를 정해진 순으로 건너려 합니다. 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 알아내야 합니다. 트럭은 1초에 1만큼 움직이며, 다리 길이는 bridge_length이고 다리는 무게 weight까지 견딥니다.  
※ 트럭이 다리에 완전히 오르지 않은 경우, 이 트럭의 무게는 고려하지 않습니다.

예를 들어, 길이가 2이고 10kg 무게를 견디는 다리가 있습니다. 무게가 [7, 4, 5, 6]kg인 트럭이 순서대로 최단 시간 안에 다리를 건너려면 다음과 같이 건너야 합니다.

|경과 시간	|다리를 지난 트럭	|다리를 건너는 트럭	|대기 트럭|
|:-:|:-:|:-:|:-:|
|0	|[]|	[]|	[7,4,5,6]|
|1~2	|[]|	[7]|	[4,5,6]|
|3|	[7]|	[4]|	[5,6]|
|4|	[7]|	[4,5]|	[6]|
|5|	[7,4]|	[5]|	[6]|
|6~7|	[7,4,5]|	[6]|	[]|
|8|	[7,4,5,6]|	[]|	[]|
  
따라서, 모든 트럭이 다리를 지나려면 최소 8초가 걸립니다.

solution 함수의 매개변수로 다리 길이 bridge_length, 다리가 견딜 수 있는 무게 weight, 트럭별 무게 truck_weights가 주어집니다. 이때 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 return 하도록 solution 함수를 완성하세요.  

### 제한사항
- bridge_length는 1 이상 10,000 이하입니다.
- weight는 1 이상 10,000 이하입니다.
- truck_weights의 길이는 1 이상 10,000 이하입니다.
- 모든 트럭의 무게는 1 이상 weight 이하입니다.


### 입출력 예  

|bridge_length|	weight|	truck_weights|	return|
|:-:|:-:|:-:|:-:|
|2|10|[7,4,5,6]|8|
|100|100|[10]|101|
|100|100|[10,10,10,10,10,10,10,10,10,10]|110|  


# my solution
```javascript
function solution(bridge_length, weight, truck_weights) {
    let answer = 0;
    let bridge = new Array(bridge_length).fill(0);
    const start = truck_weights.reduce((sum, index) => {   
        return sum+=index;
    },0);
    let end = 0;
    while (true){
        //1.초를 센다
        answer++;
        //2. 다리는 움직인다.
        end += bridge.shift();        
        //3. 다리위 무게를 구한다.
        const sum = bridge.reduce((sum, index) => {
            return sum+=index;
        },0);  
        //4. 무게를 비교하여 트럭을 올린다.
        if ( truck_weights[0] !== undefined ) {
            if ( weight >= (sum+truck_weights[0]) ) {
                bridge.push(truck_weights.shift());
            }else {
                bridge.push(0);
            }
        }else {
            bridge.push(0);
        }
        if( start === end ) break;
        
    }
    return answer;
}
```
나는 이 문제를 풀 때 문제를 꼼꼼히 읽지 않아서 시간을 많이 썼다. 괜한 오기가 붙어 4시간 동안 붙잡고 있었는데 다시 한번 문제를 꼼꼼히 읽어야겠다고 느끼는 문제였다.

이 문제는 `Queue`로 접근하여 풀었다. 완료한 트럭(`end`), 다리를 지나는 트럭(`bridge`), 대기 트럭(`start`) 이렇게 3개로 나누어 풀었다.
완료한 트럭과 대기한 트럭을 만든 이유는 `while`문을 `break`하기 위해 만들었다.
4시간 고민한 것치고 문제를 잘 읽어보면 순서는 간단하다.
1. 초(`answer`)를 센다
2. 다리(`bridge`)를 움직인다. (bridge의 맨 앞의 인덱스를 제거)
3. 현재 다리 위의 무게를 구한다. (reduce 함수를 통해 구함)
4. 무게를 비교하여 트럭을 추가하거나 무게 0을 추가한다. (제한 사항에 다리 무게를 초과하면 안 되기 때문, 무게 0을 추가하는 것은 다리길이를 유지하기 위해)
5. 완료한 트럭 무게와 대기 트럭 무게를 비교하여 같으면 `break`
# 결과
![다리위의트럭결과](/assets\img\algorithm\bridge_truck.PNG)  
이 문제를 하면서 가장 어려웠던 것이 while 문을 어떻게 반복 하는것을 많이 고민했다. 항상 그랬지만 문제를 차분하고 꼼꼼하게 읽어보면 반복문 코딩 실수를 덜게 된다는 것을 느꼈다.

>**참조**<br>
><https://programmers.co.kr/learn/courses/30/lessons/42583>