---
layout: post
title: "[Compiler] Java로 Scanner 만들기"
date: 2020-04-19
categories: Compiler
tags: compiler java scanner
sitemap:
    changefreq: daily
---


<br/>

<br/>
### ⏰ 기간 ⏰ㅤ3일
<br/>

## 1. 기능
* 계산: 덧셈, 뺄셈, 곱셈, 나눗셈, 결과(=)
* 버튼: 0 부터 9까지의 숫자, 초기화, 지우기
* 이외에 자유롭게 자신이 선보이고 싶은 기능, 있으면 좋겠다 싶은 기능 추가 (필수 1개)
<br/><br/><br/>

## 2. 시작!
내가 할 일은 여기에서 끝이지만, 그래도 검색을 좀 더 수월하게 하기위해 약간의 Reference를 제공할 생각이다.  
하지만 내가 제공하는 자료는 정말 한정적이기 때문에 필요한 자료는 더 열심히 찾고 공부해야한다.  
그리고 Reference 아래로는 나의 결과물과 설명이 이어진다.  
꼭 3일 후에 본 프로젝트를 마무리하고 확인하길 바란다.  
그냥 내 코드와 결과물을 보고 공부한다면 그것도 물론 공부가 되겠지만 자신이 직접 찾아가며 한 공부보다는 훨씬 못할 것이다.  
그리고 그 당시에는 몰랐지만 지금보면 내 코드도 잘 짜여진 코드는 아니다 (-﹏-。;)  

### Reference
- [Java GUI - AWT 와 Swing](https://docsplayer.org/84194920-Microsoft-powerpoint-java%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-9%EC%9E%A5gui.html)
- [Java GUI 로 프로그램 만들어보기](https://brian-s.tistory.com/97)
<br/><br/><br/>

## 3. 결과물
<br/>
![calculator](/assets/img/post/About_me/JavaCamp/calculator.png){:width="300px"}  

### 구현 기능
- 계산: 덧셈, 뺄셈, 곱셈, 나눗셈, 결과(=)
- 버튼: 0 부터 9까지의 숫자, 초기화, 지우기
- 나만의 기능: 키보드 모드, 최근 계산 목록

### 보완 해야할 부분
- 숫자가 길어질 때 뒷 부분이 "..." 으로 표시 → 숫자가 뒤로 밀어지게 보이게
- 나만의 기능 아이콘 표시 → 어떤 기능인지 직관적으로 알 수 있게 표시
- 소수점 아래 숫자가 0일 때는 소수점 아래로 숫자 보여지지 않게
- 아무 숫자도 입력하지 않고 '=' 버튼을 눌렀을 때 오류가 나지 않게
- 계산 버튼을 눌렀을 때 기존에 입력되었던 숫자가 지워지게 (이 부분은 좀 더 고민)
<br/><br/><br/>

## 4. 세부 기능 캡쳐
<br/>
ㅤ![calculator_detail](/assets/img/post/About_me/JavaCamp/calculator_detail.png){:width="700px"}
<br/><br/><br/>

## 5. 코드 세부 설명
<br/>
![calculator_uml](/assets/img/post/About_me/JavaCamp/calculator_uml.gif){:width="250px"}  

위 사진은 내 코드를 UML Diagram으로 나타낸 것이다.  
이 때 Java로 GUI를 처음 만들어 본 것이고 OODP이니, 객체 지향이니 하나도 모르고 만들어서 class 하나에 다 때려 넣었다.  
지금 생각하면 정말... 부끄러운 코드이다.  

코드를 세부적으로 설명하면 아래와 같다.
- **`main()`** : Calculator 객체를 만들어 `displayFrame()` 실행
- **`displayFrame()`** : 계산기 Frame을 보여주고 닫기 버튼을 누르면 닫아주는 역할
- **`Calculator()`** : `createFrame()`, `setButton()`, `setEvent()`, `setPnl()`, `addFrame()` 실행
- **`createFrame()`** : Frame들 (계산기, 키보드 모드 알림, 최근 계산 목록)의 크기, 위치를 설정하고 계산 결과 영역과 copyright 설정
- **`setButton()`** : 각 버튼들의 색상, 글자 설정해서 만드는 역할
- **`setEvent()`** : 각 버튼들을 눌렀을 때의 event 와 키보드 모드에서 키보드를 눌렀을 때의 event 설정
- **`setPnl()`** : 각 버튼들을 역할에 맞게 Panel에 나누어 담는 역할
- **`addFrame()`** : 위에서 만들었던 계산 결과 영역과 버튼, copyright를 Frame에 추가하는 역할
- **`clear()`** : 계산 결과 영역을 clear 해주는 역할
- **`calculateAddSbtr(), calculateMltpDivs`** : 덧셈, 뺄셈, 곱셈, 나눗셈을 계산해주는 역할

UML Diagram을 보면 알겠지만, 다른 함수들도 있지만 크게 중요하지 않아 주요 함수들만 설명했다.  
혹시 코드를 보고 궁금한 점이나 문의할 내용이 있으면 댓글로 남겨주세요!
<br/><br/><br/>

## 6. GitHub
제 코드는 아래 GitHub에서 확인 가능합니다 :)  
<https://github.com/0pencoding/JavaCamp-Round1-Calculator>
<br/><br/><br/>

## [[Round 2] 그림판 구현 ➜ ](https://0pencoding.github.io/javacamp/2020/03/13/JavaCamp_Round2_%EA%B7%B8%EB%A6%BC%ED%8C%90.html)
{: style="text-align: right;"}
<br/>