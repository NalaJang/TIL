## 프로그래밍 패러다임이란?

<div align = "center"><img width = "30%" src = "https://github.com/NalaJang/TIL/assets/73895803/e20c2262-0bca-4384-a78d-13cea3adb99f"/></div>

* 프로그래머에게 프로그래머에게 프로그래밍의 관점을 갖게 해주는 역할을 하는 개발 방법론
* 어떤 언어는 특정한 패러다임(방법론)을 지원한다. ex)jdk1.8이전 버전은 객체지향, 하스켈은 함수형 프로그래밍을 지원
* 예를 들어 객체지향 프로그래밍은 프로그래머들이 프로그램을 상호 작용하는 객체들의 집합으로 볼 수 있게 한다.
* 반면에, 함수형 프로그래밍은 상태 값을 지니지 않는 함수 값들의 연속으로 생각할 수 있게 해준다.
* 각 패러다임은 명확한 구분이 없고 섞이기도 한다.(언어가 패러다임에 종속되지 않는다.)

<br>

### 패러다임 흐름
순차적 + 비구조적 / goto문이 문제  
⬇️  
절자척 + 구조적 / 데이터와 행위의 분리가 문제  
⬇️  
객체지향 / 부수효과가 문제  
⬇️  
함수형(변수를 할당하고 나면 바꾸지 못하도록 제한한다.)

<br>

## 명령형 프로그래밍이란?
* '어떻게' 풀어내는가에 집중하는 패러다임

[🔗 명령형 프로그래밍](https://github.com/NalaJang/TIL/blob/main/cs/programming_paradigm/%EB%AA%85%EB%A0%B9%ED%98%95%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D.md)

(HOW) : 주차장 북쪽 출구를 나와 왼쪽으로 가세요. 12번 출구에 도착할 때까지 15번 북쪽 도로를 타세요.  
이케아를 끼고 우회전하세요. 
직진하여 첫 번째 신호등에서 우회전 하세요. 다음 신호등을 지나 좌회전을 하세요.  
예시: Flutter에서 UI는 선언형, 이 외 dataSource 같은 것들은 명령형

- 객체지향 프로그래밍
- 절차지향형 프로그래밍
- 객체지향과 절차지향형의 장단점

<br></br>

## 선언형 프로그래밍이란?
* '무엇을' 풀어내는가에 집중하는 패러다임

[🔗 선언형 프로그래밍](https://github.com/NalaJang/TIL/blob/main/cs/programming_paradigm/%EC%84%A0%EC%96%B8%ED%98%95%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D.md)

(WHAT) : 내 주소는 00시 Xx로99 입니다.

- 함수형 프로그래밍