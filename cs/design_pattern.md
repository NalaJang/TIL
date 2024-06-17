## 디자인 패턴이란?
- 프로그램을 설계할 때 발생했던 문제점들을 객체 간의 상호 관계 등을 이용하여 해결할 수 있도록 하나의 '규약' 형태로 만들어 놓은 것
=> 비슷한 문제에 대해 해결한 방법들을 보니 자주 사용되는 공통된 패턴이 나타났다. 이 패턴을 모은 것이 desgin pattern이다.

* 재사용성 : 반복적인 문제에 대한 일반적인 해결책을 제공하므로, 이를 재사용하여 유사한 상황에서 코드를 더 쉽게 작성할 수 있다.
* 가독성
* 유지보수성 : 코드를 쉽게 모듈화 할 수 있으며, 변경이 필요한 경우 해당 모듈만 수정하여 유지보수가 쉬워진다.
* 확장성
* 이미 검증되고 테스트된 구조이기 때문에 설계 과정의 속도를 높일 수 있다.

### 디자인 패턴이 중요할까?
- 중요하다고 생각한다.  
  디자인 패턴을 배우게 되면 객체 지향 디자인 원칙들을 사용해 많은 종류의 문제를 해결하는 방법들을 배울 수 있고  
  패턴 자체만을 말함으로써 팀원들과 더 효율적인 의사소통이 가능해지기 때문이다.

<br></br>

* Singleton 패턴이란?
[Singleton 패턴](https://github.com/NalaJang/TIL/blob/main/cs/desgin_pattern/Singleton%20Pattern.md)

* 😵 Factory 패턴이란?
[Factory 패턴](https://github.com/NalaJang/TIL/blob/main/cs/desgin_pattern/Factory%20Pattern.md)

* Iterator 패턴이란?
[Iterator 패턴](https://github.com/NalaJang/TIL/blob/main/cs/desgin_pattern/Iterator%20Pattern.md)

* MVC,MVP,MVVM 패턴이란?
[MVC,MVP,MVVM 패턴](https://github.com/NalaJang/TIL/blob/main/cs/desgin_pattern/MVC%2CMVP%2CMVVM%20Pattern.md)

* Observer 패턴이란?
[Observer 패턴](https://github.com/NalaJang/TIL/blob/main/cs/desgin_pattern/Observer%20Pattern.md)


- [ ]  ~란? = 개념 + 존재이유/목적 + 동작원리/구조/구현방법 + 사용예시
- [ ]  Facotry 패턴이란?
- [ ]  (추상 Factory  패턴이란?)
- [ ]  Strategy(전략) 패턴이란?

- [ ]  Proxy 패턴이란?

- [ ]  Command 패턴이란?

- [ ]  최근 사용해 본 디자인 패턴에 대한 설명과 사용한 이유

### 연관 내용 질문 리스트

- [ ]  라이브러리란?
- [ ]  프레임워크란?
- [ ]  라이브러리와 프레임워크의 차이
- [ ]  의존성이란?
- [ ]  응집도와 결합도
- [ ]  (Service Locator 패턴이란?)
- [ ]  (DI와 서비스 로케이터 비교)
- [ ]  프록시 서버란?
- [ ]  (포워드 프록시와 리버스 프록시 비교)
- [ ]  Adapter 패턴이란?
<br></br>

## 기타
### 의존성 주입(DI)이란?
- 메인 모듈이 '직접' 다른 하위 모듈에 대한 의존성을 주기보다는 중간에 의존성 주입자(dependency injector)를 놓아 메인 모듈이 '간접'적으로 의존성을 주입하는 방식
