---
title: "프로그래머스 고득점 Kit : 큰 수 만들기"
date: 2020-03-22
author: YuJin Kim
categories: [Problem Solving, Programmers, Highscore Kit]
tags: [programmers, highscore kit, level2, algorithm, greedy, c++]
sitemap:
  changefreq: daily
---

본 문제는 생각보다 빨리 푼 문제였다. 예외 케이스를 질문하기에서 찾아볼 수 있어서 그런지 모르겠지만 처음에 바로 떠올랐던 알고리즘대로 쉽게 풀 수 있었고, 효율성도 나름 괜찮게 풀어서 기분이 좋았다. 근데 string에서 erase() 함수를 어떻게 쓰는지 까먹어서 다시 찾아보았다ㅋㅋ 까먹지 않으려고 항상 블로그에 정리하고 하는건데... 앞으로 더 정신 차리고 열심히 정리해야지!  
<br/>
<br/>

## 1. 문제

어떤 숫자에서 k개의 수를 제거했을 때 얻을 수 있는 가장 큰 숫자를 구하려 합니다.

예를 들어, 숫자 1924에서 수 두 개를 제거하면 [19, 12, 14, 92, 94, 24] 를 만들 수 있습니다.  
이 중 가장 큰 숫자는 94 입니다.

문자열 형식으로 숫자 number와 제거할 수의 개수 k가 solution 함수의 매개변수로 주어집니다.  
number에서 k 개의 수를 제거했을 때 만들 수 있는 수 중 가장 큰 숫자를 문자열 형태로 return 하도록 solution 함수를 완성하세요.

### 제한조건

- number는 1자리 이상, 1,000,000자리 이하인 숫자입니다.
- k는 1 이상 `number의 자릿수` 미만인 자연수입니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. `k` 값이 0이 될 때까지 다음을 반복한다.  
   (다음 반복 과정에서 `k`값을 감소시키면서 제거할 수의 개수가 0이 될 때까지 반복하는 것이다)
2. 해당 문자가 마지막 원소이거나, 뒤의 문자보다 작으면 지우고 `k` 값을 감소시킨다.  
   (`break`를 하는 이유는 한 번 비교하면서 제거했으니 다시 처음부터 비교해야하기 때문)
3. 반복이 끝나면 `number`를 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <string>
#include <vector>

using namespace std;

string solution(string number, int k) {

    while (k) {
        for (int i = 0; i < number.length(); i++) {
            if (i == number.length() - 1
                || number[i] < number[i+1]) {
                number.erase(i, 1);
                k--;
                break;
            }
        }
    }

    return number;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- `string`의 문자 지우는 방법
- 연속적인 같은 숫자가 들어왔을 경우 고려
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- C++ 레퍼런스 - string 의 erase 함수 <https://modoocode.com/240>
  > - `string`의 문자를 삭제할 때는 `erase()` 사용, 파라미터로 위치와 갯수가 할당

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
