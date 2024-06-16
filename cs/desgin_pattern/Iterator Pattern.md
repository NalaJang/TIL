## Iterator 패턴이란?
- 이터레이터(iterator)를 사용하여 복잡하게 얽혀있는 자료 컬렉션(collection)의 요소들에 접근하는 방식을 공통화 하는 패턴
- 컬렉션에 상관없이 하나의 인터페이스로 순회가 가능하다.
- 컬렉션을 순회하는 다양한 방법을 지원할 수 있다.
- 컬렉션의 복잡한 내부 구조를 클라이언트로부터 숨길 수 있다.
- 클래스가 늘어나고 복잡도가 증가한다.

<br>

[🔗 이터레이터 패턴](https://inpa.tistory.com/entry/GOF-%F0%9F%92%A0-%EB%B0%98%EB%B3%B5%EC%9E%90Iterator-%ED%8C%A8%ED%84%B4-%EC%99%84%EB%B2%BD-%EB%A7%88%EC%8A%A4%ED%84%B0%ED%95%98%EA%B8%B0)

### 문제의 코드

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

* 반복적으로 for문을 돌려 집합체의 요소들을 순회하였다.
* 그러나 이러한 구성 방식은 Board에 들어간 Post를 순회할 때, Board가 어떠한 구조로 게시글을 저장하고 관리하는지를 클라이언트에 노출된다.
* 클라이언트는 'getPosts()' 메서드를 통해 직접 'List<Post>'에 접근할 수 있다.
* 이 방식은 Board 내부 구현 사항을 클라이언트에 공개하는 것이며, 캡슐화 원칙에 위반된다.
* 'List'를 사용한 구현 방식이 변경되면 클라이언트 코드도 영향 받는다.

<br>

### ✅ 이터레이터 패턴을 적용한 코드

<details>
  <summary><b>Iterator를 직접 구현한 코드</b></summary>

```dart
import 'package:intl/intl.dart';

class Post {
  String title; // 게시글 제목
  DateTime date; // 게시글 발행일

  Post(this.title, this.date);
}

class ListPostIterator implements Iterator<Post> {
  final Iterator<Post> _iterator;

  ListPostIterator(List<Post> posts) : _iterator = posts.iterator;

  @override
  bool moveNext() => _iterator.moveNext();

  @override
  Post get current => _iterator.current;
}

class DatePostIterator implements Iterator<Post> {
  final Iterator<Post> _iterator;

  DatePostIterator(List<Post> posts)
      : _iterator = (List<Post>.from(posts)
          ..sort((p1, p2) => p1.date.compareTo(p2.date)))
          .iterator;

  @override
  bool moveNext() => _iterator.moveNext();

  @override
  Post get current => _iterator.current;
}

class Board {
  final List<Post> _posts = [];

  void addPost(String title, DateTime date) {
    _posts.add(Post(title, date));
  }

  List<Post> get posts => _posts;

  Iterator<Post> getListPostIterator() => ListPostIterator(_posts);

  Iterator<Post> getDatePostIterator() => DatePostIterator(_posts);
}

void main() {
  // 1. 게시판 생성
  final board = Board();

  // 2. 게시판에 게시글을 포스팅
  board.addPost("디자인 패턴 강의 리뷰", DateTime(2020, 8, 30));
  board.addPost("게임 하실분", DateTime(2020, 2, 6));
  board.addPost("이거 어떻게 하나요?", DateTime(2020, 6, 1));
  board.addPost("이거 어떻게 하나요?", DateTime(2021, 12, 22));

  // 게시글 발행 순서대로 조회하기
  printPosts(board.getListPostIterator());

  // 게시글 날짜별로 조회하기
  printPosts(board.getDatePostIterator());
}

void printPosts(Iterator<Post> iterator) {
  final DateFormat formatter = DateFormat('yyyy-MM-dd');
  while (iterator.moveNext()) {
    final post = iterator.current;
    print('${post.title} / ${formatter.format(post.date)}');
  }
}
```
</details>

<details>
  <summary><b>Iterable 클래스와 Iterator를 직접 사용한 코드</b></summary>

```dart
import 'package:intl/intl.dart';

class Post {
  String title; // 게시글 제목
  DateTime date; // 게시글 발행일

  Post(this.title, this.date);
}

class Board {
  final List<Post> _posts = [];

  void addPost(String title, DateTime date) {
    _posts.add(Post(title, date));
  }

  List<Post> get posts => _posts;

  // ListPostIterable을 반환
  Iterable<Post> get listPosts => _posts;

  // DatePostIterable을 반환
  Iterable<Post> get datePosts => List<Post>.from(_posts)
    ..sort((p1, p2) => p1.date.compareTo(p2.date));
}

void main() {
  // 1. 게시판 생성
  final board = Board();

  // 2. 게시판에 게시글을 포스팅
  board.addPost("디자인 패턴 강의 리뷰", DateTime(2020, 8, 30));
  board.addPost("게임 하실분", DateTime(2020, 2, 6));
  board.addPost("이거 어떻게 하나요?", DateTime(2020, 6, 1));
  board.addPost("이거 어떻게 하나요?", DateTime(2021, 12, 22));

  // 게시글 발행 순서대로 조회하기
  printPosts(board.listPosts);

  // 게시글 날짜별로 조회하기
  printPosts(board.datePosts);
}

void printPosts(Iterable<Post> posts) {
  final DateFormat formatter = DateFormat('yyyy-MM-dd');
  for (var post in posts) {
    print('${post.title} / ${formatter.format(post.date)}');
  }
}
```
</details>

* Board 클래스의 내부 구현을 클라이언트로부터 숨기고 있다. 객체 지향 프로그래밍의 ***정보 은닉*** 원칙

#### 내부 구조 변경의 용이성
* Board 클래스의 내부 구조나 리스트의 형식이 바뀌어도 클라이언트 코드는 영향을 받지 않는다.
#### 캡슐화
* 리스트의 직접적인 노출을 막았다.
#### 유연성
* 순회 전략을 각 객체로 나눔으로써 다양한 순서로 데이터를 접근할 수 있다.

<br></br>

## Iterable 이란?
- 반복 가능한, 순회 가능한 컬렉션을 나타내는 추상 클래스 또는 인터페이스를 말한다.
- 'map', 'where', 'forEach', 'reduce'등의 고차함수 메서드를 제공한다.
- 'iterator' getter를 제공한다.
- 'iterator'의 'hasNext'와 'next'로 컬렉션의 요소에 접근할 수 있다.
