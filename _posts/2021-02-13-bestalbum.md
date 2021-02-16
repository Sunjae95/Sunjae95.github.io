---
title: 프로그래머스 - 베스트앨범
date: 2021-02-13 13:23:00 +/-TTTT
categories: [Algorithm, Hash]
tags: [programmers, Hash, algorithm]     # TAG names should always be lowercase
---
# 베스트 앨범

## 문제
스트리밍 사이트에서 장르 별로 가장 많이 재생된 노래를 두 개씩 모아 베스트 앨범을 출시하려 합니다. 노래는 고유 번호로 구분하며, 노래를 수록하는 기준은 다음과 같습니다.

1. 속한 노래가 많이 재생된 장르를 먼저 수록합니다.
2. 장르 내에서 많이 재생된 노래를 먼저 수록합니다.
3. 장르 내에서 재생 횟수가 같은 노래 중에서는 고유 번호가 낮은 노래를 먼저 수록합니다.  

노래의 장르를 나타내는 문자열 배열 genres와 노래별 재생 횟수를 나타내는 정수 배열 plays가 주어질 때, 베스트 앨범에 들어갈 노래의 고유 번호를 순서대로 return 하도록 solution 함수를 완성하세요.

### 제한사항
- genres[i]는 고유번호가 i인 노래의 장르입니다.
- plays[i]는 고유번호가 i인 노래가 재생된 횟수입니다.
- genres와 plays의 길이는 같으며, 이는 1 이상 10,000 이하입니다.
- 장르 종류는 100개 미만입니다.
- 장르에 속한 곡이 하나라면, 하나의 곡만 선택합니다.
- 모든 장르는 재생된 횟수가 다릅니다.

### 입출력 예
|**genres**|**plays**|**return**|
|:-:|:-:|:-:|
|	["classic", "pop", "classic", "classic", "pop"]|[500, 600, 150, 800, 2500]|	[4, 1, 3, 0]|  
  

### 입출력 설명
classic 장르는 1,450회 재생되었으며, classic 노래는 다음과 같습니다.

고유 번호 3: 800회 재생
고유 번호 0: 500회 재생
고유 번호 2: 150회 재생
pop 장르는 3,100회 재생되었으며, pop 노래는 다음과 같습니다.

고유 번호 4: 2,500회 재생
고유 번호 1: 600회 재생
따라서 pop 장르의 [4, 1]번 노래를 먼저, classic 장르의 [3, 0]번 노래를 그다음에 수록합니다.
# my solution
```javascript
function solution(genres, plays) {
    let answer = [];
    const arr = best(genres, plays);
    
    for(let i=0; i<arr.length; i++){        //각 장르별 1,2순위 앨범 등록하기
        const tmp = gSort(arr[i], genres, plays);
        answer = answer.concat(tmp);
    }

    return answer;
}

function best(genres, plays) {  //장르 순서정하기
    const g_arr = genres.filter((item, index) => {      //중복제거
        return genres.indexOf(item) === index;
    });
    let p_arr = new Array(g_arr.length).fill(0);

    for(let i=0; i<genres.length; i++){
        const tmp =g_arr.findIndex((item) => {      //인덱스
            return item === genres[i];
        });
        p_arr[tmp] += plays[i];
    }
    let arr =[];
    for(let i=0; i<g_arr.length; i++){              //가장 많이 조회된 순서대로 arr에 등록
        const max = Math.max.apply(null, p_arr);
        const max_index = p_arr.indexOf(max);
        p_arr[max_index] = 0;
        arr.push(g_arr[max_index]);    
    }

   
    return arr;     
}

function gSort(title, genres, plays){       //장르내 음악 앨범 순서 정하기
    let arr = [];
    genres.forEach((item, index) => {   //인덱스 모아 놓기
        if( item === title ){
            arr.push(index);
        }        
    });
    
    if(arr.length === 1 ) {
        return arr;
    }
    for(let i=0; i<arr.length; i++){        //정렬 높은순에서 적은순으로 
        for(let j=0; j<arr.length-i; j++){
            if( plays[arr[j]] > plays[arr[j-1]]){
                const tmp = arr[j-1];
                arr[j-1] = arr[j];
                arr[j] = tmp;
            }
        }
    }
    arr = arr.slice(0,2);       //가장 첫번째 두번째 앨범 등록
    return arr;
}
```
나는 이 문제를 7시간동안 붙잡고 있었다. 남들한테는 쉬운 문제일 수 있지만 나에게는 나의 진로에 대한 고민이 많이드는 문제였다. 이 문제를 못 풀면 나는 개발자가 맞지 않을것이다 등.. 많은 생각이 오갔으며 그만큼 포기하기가 싫었다.  
  
처음에는 이 문제를 모든 장르중 가장 많이 플레이된 2개의 장르를 뽑아 순서를 정하고 순서에 맞춰 그 장르중 플레이 순으로 나열하라고 생각했다.  
그렇게만 생각하고 문제를 풀었지만 `Object`를 사용하여 장르와 순서를 정하여 크기를 비교해 정렬하여 `answer`배열에 추가하여 뽑는 방식을 했지만 `Object`를 배열 처럼 사용하기가 많이 어렵다는 것을 알게되어 포기하고 오직 `배열`을 사용하여 문제를 풀었다.  

그렇게 문제를 풀어보니 1,2,15번 말고는 다 틀렸다. 그래서 다른 사람들의 질문을 보니 장르를 두개를 순서를 정하는것이 아니라 모든 장르의 순서를 정하여 각각 순서대로 2개씩 나열하는 것이었다.  

### 정리  
1. 가장많이 플레이된 장르부터 적은 장르까지 순서를 정한다.
2. for문을 돌려 각 장르의 플레이가 많이 된 첫번째 두번째 인덱스를 구한다.
3. 순서대로 for문을 돌려 `answer`에 2번에서 계산된 결과를 추가시킨다.

> **참조**<br>
><https://programmers.co.kr/learn/courses/30/lessons/42579>
