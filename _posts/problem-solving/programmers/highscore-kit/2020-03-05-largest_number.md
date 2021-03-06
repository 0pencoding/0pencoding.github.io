---
title: "프로그래머스 고득점 Kit : 가장 큰 수"
date: 2020-03-05
author: YuJin Kim
categories: [Problem Solving, Programmers, Highscore Kit]
tags: [programmers, highscore kit, level2, algorithm, sorting, c++, javascript]
sitemap:
  changefreq: daily
---

본 문제는 푸는데 시간이 정말 오래걸렸던 문제이다. 하지만 알고리즘 문제 풀기의 정석대로 단계를 거쳤던 것 같아 문제를 풀고나서는 뿌듯하고 내 자신이 자랑스러웠다. 처음에 잘못된 방향으로 고민하다가 점점 정답에 가깝게 생각했다는 것이 정말 기분좋다 :)  
<br/>
<br/>

## 1. 문제

0 또는 양의 정수가 주어졌을 때, 정수를 이어 붙여 만들 수 있는 가장 큰 수를 알아내 주세요.  
예를 들어, 주어진 정수가 [6, 10, 2]라면 [6102, 6210, 1062, 1026, 2610, 2106]를 만들 수 있고, 이중 가장 큰 수는 6210입니다.
0 또는 양의 정수가 담긴 배열 numbers가 매개변수로 주어질 때, 순서를 재배치하여 만들 수 있는 가장 큰 수를 문자열로 바꾸어 return 하도록 solution 함수를 작성해주세요.

### 제한조건

- numbers의 길이는 1 이상 100,000 이하입니다.
- numbers의 원소는 0 이상 1,000 이하입니다.
- 정답이 너무 클 수 있으니 문자열로 바꾸어 return 합니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. `numbers`를 문제에 맞게 정렬하기위해 어떻게 정렬할지 정하는 `compare` 함수를 만든다.
2. `compare` 함수는 두 수를 `string`으로 변환한 후, 각 수의 순서를 반대로 합친 문자열을 비교한다.  
   (문제에 맞는 정렬은 이어 붙여 만들 수 있는 가장 큰 수이기 때문에 이어 붙였을 때를 기준으로 비교)
3. 정렬된 벡터를 그대로 이어붙여 문자열을 만든다.
4. 벡터에 맨 앞에 0이 들어갔을 경우(모든 원소가 0으로 이루어져있는 경우)를 고려하여 첫 숫자가 0이면 "0"을 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

bool compare(int i, int j) {
    string a = to_string(i);
    string b = to_string(j);

    return a+b > b+a;
}

string solution(vector<int> numbers) {
    string answer = "";

    sort(numbers.begin(), numbers.end(), compare);
    for (auto n : numbers)
        answer += to_string(n);

    if (answer.at(0) == '0') return "0";
    return answer;
}
```

<br/>

### [Javascript]

```javascript
function solution(numbers) {
  var answer = "";

  numbers.sort(function (a, b) {
    var ab = String(a) + String(b);
    var ba = String(b) + String(a);
    return ba - ab;
  });

  for (var i = 0; i < numbers.length; i++) answer += String(numbers[i]);

  if (answer.startsWith("0")) return "0";
  return answer;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- 푸는데 시간 오래걸림
- 각 문자열의 길이를 같게하는게 key point!
- 0일 경우는 생각 못함...(마지막 테스트 케이스...)
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- [C++] sort algorithm 정리 및 예시 <https://blockdmask.tistory.com/178>
  > - 사용자 정의 함수를 사용한 sorting을 위해서는 `sort()` 함수의 3번째 인자에 사용자 정의 함수를 assign
- [C++] string 클래스, 문자열에 대해서 (총정리) <https://blockdmask.tistory.com/338>
  > - `string`에서 index로 접근하기 위해서는 `string.at()` 함수를 사용하며 char형태가 반환

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
