---
title: "2020 카카오 인턴십 : 수식 최대화"
date: 2020-07-03
author: YuJin Kim
categories: [Problem Solving, Programmers, Kakao]
tags: [programmers, level2, algorithm, bruteforce, dfs-bfs, c++]
sitemap:
  changefreq: daily
---

문제... 완전... 못 풀었어...ㅠㅠ 이번 문제는 정말 지저분하게 풀고 알고리즘이 깔끔하지 못하다는 생각이 들었다ㅠㅠ (세상에 3중 for문 이라니..) C++에서 문자열 split 관련 함수를 정식적으로 지원해주지 않는다는 것도 코드가 지저분해진데에 한 몫 하기 했지만, 그래도 제일 큰 문제는 내 알고리즘이 잘못된거겠지...?ㅠㅠ 문제를 봤을때 완전탐색 문제라는 생각은 들었는데 어떻게 풀어야할지는 잘 감이 오지 않았다.. 지저분한 코드로 해결은 했으나, 아직 다른 사람의 풀이도 보지 않은 상태이기 때문에 좀 더 깔끔한 알고리즘을 더 생각해보고 다시 풀어볼 생각이다..!  
<br/>
<br/>

## 1. 문제

IT 벤처 회사를 운영하고 있는 라이언은 매년 사내 해커톤 대회를 개최하여 우승자에게 상금을 지급하고 있습니다.  
이번 대회에서는 우승자에게 지급되는 상금을 이전 대회와는 다르게 다음과 같은 방식으로 결정하려고 합니다.  
해커톤 대회에 참가하는 모든 참가자들에게는 숫자들과 3가지의 연산문자(+, -, \*) 만으로 이루어진 연산 수식이 전달되며, 참가자의 미션은 전달받은 수식에 포함된 연산자의 우선순위를 자유롭게 재정의하여 만들 수 있는 가장 큰 숫자를 제출하는 것입니다.

단, 연산자의 우선순위를 새로 정의할 때, 같은 순위의 연산자는 없어야 합니다.  
즉, + > - > _ 또는 - > _ > + 등과 같이 연산자 우선순위를 정의할 수 있으나 +,_ > - 또는 _ > +,-처럼 2개 이상의 연산자가 동일한 순위를 가지도록 연산자 우선순위를 정의할 수는 없습니다. 수식에 포함된 연산자가 2개라면 정의할 수 있는 연산자 우선순위 조합은 2! = 2가지이며, 연산자가 3개라면 3! = 6가지 조합이 가능합니다. 만약 계산된 결과가 음수라면 해당 숫자의 절댓값으로 변환하여 제출하며 제출한 숫자가 가장 큰 참가자를 우승자로 선정하며, 우승자가 제출한 숫자를 우승상금으로 지급하게 됩니다.

예를 들어, 참가자 중 네오가 아래와 같은 수식을 전달받았다고 가정합니다.

```
"100-200*300-500+20"
```

<br/>
일반적으로 수학 및 전산학에서 약속된 연산자 우선순위에 따르면 더하기와 빼기는 서로 동등하며 곱하기는 더하기, 빼기에 비해 우선순위가 높아 * > +,- 로 우선순위가 정의되어 있습니다. 대회 규칙에 따라 + > - > * 또는 - > * > + 등과 같이 연산자 우선순위를 정의할 수 있으나 +,* > - 또는 * > +,- 처럼 2개 이상의 연산자가 동일한 순위를 가지도록 연산자 우선순위를 정의할 수는 없습니다. 수식에 연산자가 3개 주어졌으므로 가능한 연산자 우선순위 조합은 3! = 6가지이며, 그 중 + > - > * 로 연산자 우선순위를 정한다면 결괏값은 22,000원이 됩니다. 반면에 * > + > - 로 연산자 우선순위를 정한다면 수식의 결괏값은 -60,420 이지만, 규칙에 따라 우승 시 상금은 절댓값인 60,420원이 됩니다.

참가자에게 주어진 연산 수식이 담긴 문자열 expression이 매개변수로 주어질 때, 우승 시 받을 수 있는 가장 큰 상금 금액을 return 하도록 solution 함수를 완성해주세요.

### 제한조건

- expression은 길이가 3 이상 100 이하인 문자열입니다.
- expression은 공백문자, 괄호문자 없이 오로지 숫자와 3가지의 연산자(+, -, \*) 만으로 이루어진 올바른 중위표기법(연산의 두 대상 사이에 연산기호를 사용하는 방식)으로 표현된 연산식입니다. 잘못된 연산식은 입력으로 주어지지 않습니다.
  - 즉, "402+-561\*"처럼 잘못된 수식은 올바른 중위표기법이 아니므로 주어지지 않습니다.
- expression의 피연산자(operand)는 0 이상 999 이하의 숫자입니다.
  - 즉, "100-2145\*458+12"처럼 999를 초과하는 피연산자가 포함된 수식은 입력으로 주어지지 않습니다.
  - "-56+100"처럼 피연산자가 음수인 수식도 입력으로 주어지지 않습니다.
- expression은 적어도 1개 이상의 연산자를 포함하고 있습니다.
- 연산자 우선순위를 어떻게 적용하더라도, expression의 중간 계산값과 최종 결괏값은 절댓값이 263 - 1 이하가 되도록 입력이 주어집니다.
- 같은 연산자끼리는 앞에 있는 것의 우선순위가 더 높습니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

#### 해결은 했으나, 알고리즘이 깔끔하지 못한 풀이 (통과 O)

> `strtok_s` 함수는 C/C++ 언어의 본래 `strtok_s()` 와 동일하며, `permutation` 함수는 아래 참고링크를 달아두었으니 설명 생략한다.

1. 처음에 매개변수로 주어지는 `expression` 문자열을 직접 구현한 `strtok_s` 함수를 사용하여 "\*, +, -" 기준으로 split하고 숫자는 `numbers` 벡터에, 연산기호는 `operands` 벡터에 담는다.
2. `operands_kind` 벡터를 `operands` 벡터를 복사하여 초기화하고, 동일한 연산기호를 지워 사용되는 연산기호의 종류만을 담도록 한다.
3. `operands_kind` 벡터를 매개변수로 넘겨주고 해당 벡터의 가능한 순열을 구하여 (이것이 모든 연산자의 가능한 우선순위가 된다) `operand_priority` 2차원 벡터에 담는다.
4. `operand_priority` 벡터를 반복하며 각 원소의 우선순위에 따라 수식을 계산한다.
5. 수식을 계산한 후, 결과 값의 절대값이 `answer`보다 크면 `answer`를 해당 값으로 바꿔준다.
6. `operand_priority` 벡터의 반복이 끝나면 `answer`를 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

#### 해결은 했으나, 알고리즘이 깔끔하지 못한 풀이 (통과 O)

```c++
#include <string>
#include <vector>
#include <sstream>

using namespace std;

void strtok_s(string str, string delimeter, vector<long long>& numbers, vector<char>& operands) {
    long long number;
    string num = "";
    for(char c : str) {
        bool is_delimit = false;
        for(char d : delimeter) {
            if(c == d) {
                operands.push_back(d);
                istringstream (num) >> number;
                numbers.push_back(number);
                num = "";
                is_delimit = true;
                break;
            }
        }
        if(!is_delimit) num += c;
    }
    istringstream (num) >> number;
    numbers.push_back(number);
}

void permutation(vector<vector<char>>& operand_priority, vector<char>& operands, int start, int end) {
    if (start == end) operand_priority.push_back(operands);
    else {
        for (int i = start; i <= end; i++) {
            swap(operands[start], operands[i]);
            permutation(operand_priority, operands, start + 1, end);
            swap(operands[start], operands[i]);
        }
    }
}

long long solution(string expression) {
    vector<vector<char>> operand_priority;
    vector<char> operands;
    vector<long long> numbers;
    long long answer = 0;

    strtok_s(expression, "*+-", numbers, operands);
    vector<char> operands_kind(operands);

    for(int i = 0; i < operands_kind.size() - 1; i++) {
        for(int j = i + 1; j < operands_kind.size(); j++) {
            if (operands_kind[i] == operands_kind[j]) {
                operands_kind.erase(operands_kind.begin() + j);
                j--;
            }
        }
    }

    permutation(operand_priority, operands_kind, 0, 2);

    for(auto priority : operand_priority) {
        vector<long long> cpNumbers (numbers);
        vector<char> cpOperands (operands);
        for(char c : priority) {
            for(int i = 0; i < cpOperands.size(); i++) {
                if (cpOperands[i] == c) {
                    switch(c) {
                        case '*':
                            cpNumbers[i] *= cpNumbers[i+1];
                            cpOperands.erase(cpOperands.begin() + i);
                            cpNumbers.erase(cpNumbers.begin() + i + 1);
                            i--;
                            break;
                        case '+':
                            cpNumbers[i] += cpNumbers[i+1];
                            cpOperands.erase(cpOperands.begin() + i);
                            cpNumbers.erase(cpNumbers.begin() + i + 1);
                            i--;
                            break;
                        case '-':
                            cpNumbers[i] -= cpNumbers[i+1];
                            cpOperands.erase(cpOperands.begin() + i);
                            cpNumbers.erase(cpNumbers.begin() + i + 1);
                            i--;
                            break;
                        default:
                            ;
                    }
                }
            }
        }
        if(abs(cpNumbers[0]) > answer) answer = abs(cpNumbers[0]);
    }

    return answer;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- 순열을 구하는 방법 (DFS/BFS 적용했다고 보면되지 않을까!)
- 문자열 split하는 함수 생성 (내가 원하는대로 자유롭게 사용할 수 있도록 구현할 정도로 실력 쌓자!)  
  (위의 `strtok_s()`는 본래 C, C++의 `strtok_s()` 기능을 생각해서 내 나름대로 스스로 구현해 보았다)
- 문자열 정수형으로 바꾸기
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- 순열 알고리즘(Permutation Algorithm)  
  <https://minusi.tistory.com/entry/%EC%88%9C%EC%97%B4-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-Permutation-Algorithm>
  > - 재귀함수를 사용해서 순열을 구하는 함수 작성, 결과적으로 DFS의 느낌, 잘 공부해두자!
- [Stack overflow] convert string to int  
  <https://stackoverflow.com/questions/7663709/how-can-i-convert-a-stdstring-to-int>
  > - 문자열을 정수형으로 바꿀때는 `isstream(string) >> 정수형 변수` 으로 초기화와 동시에 정수형 변수에 할당 가능

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
