## Singleton 패턴이란?
- 하나의 클래스에 오직 하나의 인스턴스만 가지는 패턴
- 보통 데이터베이스 연결 모듈에 많이 사용한다.

### 장점
- 하나의 인스턴스를 만들어 놓고 해당 인스턴스를 공유하며 사용하기 때문에 인스턴스 생성할 때 드는 비용이 줄어드는 장점이 있다.

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
