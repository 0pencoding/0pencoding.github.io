---
title: "프로그래머스 고득점 Kit : 타겟 넘버"
date: 2020-03-11
author: YuJin Kim
categories: [Problem Solving, Programmers, Highscore Kit]
tags: [programmers, highscore kit, level2, algorithm, dfs-bfs, c++]
sitemap:
  changefreq: daily
---

본 문제는 처음에 접근을 어떻게 해야할지 잘 모르겠어서 언니와 의논을 한 뒤에 풀기 시작했다. 확실히 한 번 의논을 한 뒤에 문제에 접근하면 훨씬 쉽게 접근 할 수 있는 것 같다. 완전히 혼자의 힘으로 풀지는 못했지만, 문제를 푸는 방향을 옳게 갔다는 데에는 확실히 좋은 방법이라고 생각이 든다. 그래도 다음부터는 최대한 혼자의 힘으로 풀도록 노력해야지 (๑و•̀Δ•́)و  
<br/>
<br/>

## 1. 문제

n개의 음이 아닌 정수가 있습니다.  
이 수를 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다.  
예를 들어 [1, 1, 1, 1, 1]로 숫자 3을 만들려면 다음 다섯 방법을 쓸 수 있습니다.

```md
-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3
```

사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return 하도록 solution 함수를 작성해주세요.

### 제한조건

- 주어지는 숫자의 개수는 2개 이상 20개 이하입니다.
- 각 숫자는 1 이상 50 이하인 자연수입니다.
- 타겟 넘버는 1 이상 1000 이하인 자연수입니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. `recursive`를 사용해서 풀어보자.
2. parameter로 받은 `numbers` 벡터의 길이에 따라서 길이가 0일 때와 나머지의 경우로 나눈다.
3. `vector`의 길이가 0일 경우 `sum`이 `target`과 같으면 1을 반환하고, 아니라면 0을 반환한다.  
   (`vector`의 길이가 0: 벡터 안의 수를 전부 더하거나 뺐다,  
   `sum`: 벡터안의 수를 더하거나 뺀 값,  
   `sum`이 `target`과 같다: 벡터 안의 수를 더하거나 빼서 타겟 넘버를 만들 수 있는 방법의 수 중 한 개이므로 1 반환,  
   `sum`이 `target`과 다르다: 타겟 넘버를 만들 수 없기 때문에 0 반환)
4. 벡터의 길이가 0이 아니면 더하거나 빼야할 수가 더 있다는 말이므로,  
   `sum`에 벡터 첫번째 원소를 각각 더한 경우와 뺀 경우를 해당 함수의 파라미터로 넣어 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <string>
#include <vector>

using namespace std;

int find_answer(vector<int> numbers, int target, int sum) {
    if (numbers.size() == 0) {
        if (sum == target) return 1;
        return 0;
    } else {
        vector<int> numbers_cp;
        numbers_cp.assign(numbers.begin() + 1, numbers.end());

        return find_answer(numbers_cp, target, sum + numbers[0])
        + find_answer(numbers_cp, target, sum - numbers[0]);
    }

}

int solution(vector<int> numbers, int target) {
    return find_answer(numbers, target, 0);
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- recursive는 비효율적이라는 고정관념에 빠져 recursive 사용하기를 꺼려했는데 그러지 말아야겠다
- `vector`의 첫 원소만 제외하고 `vector`를 만들어줄 때 `assign()` 함수를 사용하는건 메모리 측면에서 너무 비효율 적인 것 같은데 방법이 없을까?
- 파라미터를 한 개 더 추가해서 현재 더하거나 빼고자하는 수의 위치를 담으면 된다
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- [C++ 공식문서] std:vector:assign <http://www.cplusplus.com/reference/vector/vector/assign/>

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
