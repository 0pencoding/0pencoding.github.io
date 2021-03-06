---
title: "프로그래머스 고득점 Kit : 정수 삼각형"
date: 2020-08-06
author: YuJin Kim
categories: [Problem Solving, Programmers, Highscore Kit]
tags: [programmers, highscore kit, level3, algorithm, dynamic programming, c++]
sitemap:
  changefreq: daily
---

이 문제를 푼지는 꽤 됐는데, 요즘 이래저래 정신이 없다보니까 문제를 풀기만하고 블로그에 정리를 못했다. 덕분에 정리할 문제가 밀린 상태..😅 문제를 풀고 그때그때 정리해야 기억에도 더 오래 남고 공부가 제대로 될텐데 요즘 조금씩 지친건지, 나태해진건지... 다시 한 번 마음을 다잡고 열심히 해야겠다는 생각이 든다. 이 문제는 동적 계획법 문제를 처음 푸는거라 조금 헤맸었는데, 계속해서 알고리즘을 생각해보면서 효율성 좋게 알고리즘을 탄탄히 세워갈 수 있었다. 문제를 풀고 나서는 꽤 뿌듯-(ღ˘⌣˘ღ)  
<br/>
<br/>

## 1. 문제

![정수_삼각형](https://grepp-programmers.s3.amazonaws.com/files/production/97ec02cc39/296a0863-a418-431d-9e8c-e57f7a9722ac.png){: width="300" class="normal"}

위와 같은 삼각형의 꼭대기에서 바닥까지 이어지는 경로 중, 거쳐간 숫자의 합이 가장 큰 경우를 찾아보려고 합니다.  
아래 칸으로 이동할 때는 대각선 방향으로 한 칸 오른쪽 또는 왼쪽으로만 이동 가능합니다.  
예를 들어 3에서는 그 아래칸의 8 또는 1로만 이동이 가능합니다.

삼각형의 정보가 담긴 배열 triangle이 매개변수로 주어질 때,  
거쳐간 숫자의 최댓값을 return 하도록 solution 함수를 완성하세요.

### 제한조건

- 삼각형의 높이는 1 이상 500 이하입니다.
- 삼각형을 이루고 있는 숫자는 0 이상 9,999 이하의 정수입니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. 테스트 케이스에서 2차원 배열의 행 사이즈가 같기 때문에, 첫 번째 행의 사이즈를 이용해서 삼각형의 아래에서 두번째 줄의 실질적인 사이즈를 구해 `count` 변수를 생성하고 해당 값으로 초기화한다.
2. 아래에서 두번째 줄부터 시작해서 원소를 한 개씩 돌면서, 아랫줄의 오른쪽/왼쪽 값 중 더 큰 수를 골라 더한다.  
   (아래에서 위로 올라오면서 오른쪽/왼쪽 값 중 한 개의 값을 받는데, 최댓값을 구해야하기 때문에 큰 수를 더하는 것)
3. 첫 번째 줄까지 올라와 반복이 끝나면, 꼭대기(첫번째 줄, 첫번째 값) 값을 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <vector>

using namespace std;

int solution(vector<vector<int>> triangle) {
    int count = triangle[0].size()-1;

    for(int i = triangle.size()-2; i >= 0; i--) {
        for(int j = 0; j < count; j++) {
            triangle[i][j] += max(triangle[i+1][j], triangle[i+1][j+1]);
        }
        count--;
    }

    return triangle[0][0];
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- Java는 안그런데 C++ 테스트 케이스는 2차원 배열에서 모든 행이 갖는 배열 사이즈가 모두 똑같더라, 유의할 것!
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- 없다 (◞ꈍ∇ꈍ)◞

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
