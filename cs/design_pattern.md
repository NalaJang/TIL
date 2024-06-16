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

## Singleton 패턴이란?
- 하나의 클래스에 오직 하나의 인스턴스만 가지는 패턴
- 하나의 인스턴스를 만들어 놓고 해당 인스턴스를 공유하며 사용하기 때문에 인스턴스 생성할 때 드는 비용이 줄어드는 장점이 있다.
- 보통 데이터베이스 연결 모듈에 많이 사용한다.

### 단점
- TDD(Test Driven Development)의 걸림돌이 된다. 단위 테스트는 테스트가 서로 독립적이어야 하며 어떤 순서로든 실행할 수 있어햐 한다.  
하지만 싱글통 패턴은 미리 생성된 하나의 인스턴스를 기반으로 구현하는 패턴이므로 각 테스트마다 '독립적인' 인스턴스를 만들기 어렵다.
- 모듈 간의 결합을 강하게 만들어 의존성이 높다. -> 의존성 주입(DI)을 통해 모듈 간의 결합을 느슨하게 만들 수 있다.

### Dart에서의 싱글톤
```dart
class Singleton {
  // Dart에선 생성자가 없을 경우 자동으로 public 한 생성자를 만든다.
  // 이를 막기 위해 빈 private 생성자를 만든다.
  Singleton._privateConstructor();

  // 생성자를 호출하고 반환된 Singleton 인스턴스를 _instance 변수에 할당
  static final Singleton _instance = Singleton._privateConstructor();

  // Singleton() 호출 시에 _instance 변수를 반환
  factory Singleton() {
    return _instance;
  }
}

// _privateConstructor : 이름은 상관없다.

```

<br></br>

## 😵 Factory 패턴이란?
- 객체 생성을 위한 인터페이스를 정의하고, 하위 클래스에서 객체 생성에 관한 구체적인 내용을 결정하는 패턴
- 상위 클래스와 하위 클래스가 분리되기 때문에 느슨한 결합을 가진다.
- 객체 생성 로직을 캡슐화하여 코드의 가독성을 높이고 리팩터링 시에도 한 곳만 고칠 수 있어서 유지 보수가 용이하다.

[팩토리 패턴](https://velog.io/@broccolism/%EB%82%B4%EA%B0%80-%EC%95%8C%EA%B3%A0-%EC%9E%88%EB%8D%98%EA%B2%8C-%EA%B0%80%EC%A7%9C-%ED%8C%A9%ED%86%A0%EB%A6%AC-%ED%8C%A8%ED%84%B4%EC%9D%B4%EC%97%88%EB%8D%98-%EC%8D%B0)

<br></br>

## Iterator 패턴이란?
- 이터레이터(iterator)를 사용하여 복잡하게 얽혀있는 자료 컬렉션(collection)의 요소들에 접근하는 방식을 공통화 하는 패턴
- 컬렉션에 상관없이 하나의 인터페이스로 순회가 가능하다.
- 컬렉션을 순회하는 다양한 방법을 지원할 수 있다.
- 컬렉션의 복잡한 내부 구조를 클라이언트로부터 숨길 수 있다.
- 클래스가 늘어나고 복잡도가 증가한다.

[이터레이터 패턴](https://inpa.tistory.com/entry/GOF-%F0%9F%92%A0-%EB%B0%98%EB%B3%B5%EC%9E%90Iterator-%ED%8C%A8%ED%84%B4-%EC%99%84%EB%B2%BD-%EB%A7%88%EC%8A%A4%ED%84%B0%ED%95%98%EA%B8%B0)

```dart
import 'dart:collection';

class Post {
  String title; // 게시글 제목
  DateTime date; // 게시글 발행일

  Post(this.title, this.date);
}

class Board {
  // 게시글을 리스트 집합 객체로 저장 관리
  List<Post> posts = [];

  void addPost(String title, DateTime date) {
    posts.add(Post(title, date));
  }

  List<Post> getPosts() {
    return posts;
  }
}

void main() {
  // 1. 게시판 생성
  Board board = Board();

  // 2. 게시판에 게시글을 포스팅
  board.addPost("디자인 패턴 강의 리뷰", DateTime(2020, 8, 30));
  board.addPost("게임 하실분", DateTime(2020, 2, 6));
  board.addPost("이거 어떻게 하나요?", DateTime(2020, 6, 1));
  board.addPost("이거 어떻게 하나요?", DateTime(2021, 12, 22));

  List<Post> posts = board.getPosts();

  // 3. 게시글 발행 순서대로 조회하기
  for (var post in posts) {
    print('${post.title} / ${post.date}');
  }

  // 4. 게시글 날짜별로 조회하기
  posts.sort((p1, p2) => p1.date.compareTo(p2.date)); // 집합체를 날짜별로 정렬
  for (var post in posts) {
    print('${post.title} / ${post.date}');
  }
}
```



- [ ]  ~란? = 개념 + 존재이유/목적 + 동작원리/구조/구현방법 + 사용예시
- [ ]  Facotry 패턴이란?
- [ ]  (추상 Factory  패턴이란?)
- [ ]  Strategy(전략) 패턴이란?
- [ ]  Observer(관찰자) 패턴이란?
- [ ]  Proxy 패턴이란?
- [ ]  Iterator 란?
- [ ]  Iterable 이란?
- [ ]  MVC 패턴이란?
- [ ]  MVP 패턴이란?
- [ ]  MVVM 패턴이란?
- [ ]  DataBinding이란?
- [ ]  Flutter에서 DataBinding
- [ ]  Command 패턴이란?
- [ ]  MVC, MVP, MVVM 비교 및 나오게 된 흐름
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
### 의존성 주입(DI) 패턴이란?
- 메인 모듈이 '직접' 다른 하위 모듈에 대한 의존성을 주기보다는 중간에 의존성 주입자(dependency injector)를 놓아 메인 모듈이 '간접'적으로 의존성을 주입하는 방식
