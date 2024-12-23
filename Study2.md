# MainDish

```dart
class Book {
  String title;
  String author;
  bool isCheckedOut;

  Book(this.title, this.author, {this.isCheckedOut = false});

  @override
  String toString() => '$title by $author';
}

class Library {
  String name;
  List<Book> books = [];
  Map<String, List<Book>> booksByAuthor = {};

  Library(this.name);

  void addBook(Book book) {
    books.add(book);
    booksByAuthor.putIfAbsent(book.author, () => []).add(book);
  }

  bool checkOutBook(String title) {
    var book = books.firstWhere((b) => b.title == title, orElse: () => Book('', ''));
    if (book.title.isNotEmpty && !book.isCheckedOut) {
      book.isCheckedOut = true;
      return true;
    }
    return false;
  }

  bool returnBook(String title) {
    var book = books.firstWhere((b) => b.title == title, orElse: () => Book('', ''));
    if (book.title.isNotEmpty && book.isCheckedOut) {
      book.isCheckedOut = false;
      return true;
    }
    return false;
  }

  List<Book> getBooksByAuthor(String author) {
    return booksByAuthor[author] ?? [];
  }

  List<Book> getAvailableBooks() {
    return books.where((book) => !book.isCheckedOut).toList();
  }

  void displayLibraryStats() {
    print('Library: $name');
    print('Total books: ${books.length}');
    print('Checked out books: ${books.where((b) => b.isCheckedOut).length}');
    print('Available books: ${books.where((b) => !b.isCheckedOut).length}');
  }
}

void main() {
  var library = Library('City Central Library');

  library.addBook(Book('1984', 'George Orwell'));
  library.addBook(Book('To Kill a Mockingbird', 'Harper Lee'));
  library.addBook(Book('Pride and Prejudice', 'Jane Austen'));
  library.addBook(Book('The Great Gatsby', 'F. Scott Fitzgerald'));
  library.addBook(Book('Animal Farm', 'George Orwell'));

  library.displayLibraryStats();

  print('\nChecking out "1984"...');
  if (library.checkOutBook('1984')) {
    print('Successfully checked out "1984"');
  }

  print('\nBooks by George Orwell:');
  library.getBooksByAuthor('George Orwell').forEach(print);

  print('\nAvailable books:');
  library.getAvailableBooks().forEach(print);

  library.displayLibraryStats();
}
```

# Dart 도서관 관리 시스템 코드 해석

이 코드는 간단한 도서관 관리 시스템을 구현한 Dart 프로그램입니다. 주요 구성 요소와 문법을 설명하겠습니다.

## 1. Book 클래스

```dart
class Book {
  String title;
  String author;
  bool isCheckedOut;

  Book(this.title, this.author, {this.isCheckedOut = false});

  @override
  String toString() => '$title by $author';
}
```

- **생성자**: `Book(this.title, this.author, {this.isCheckedOut = false});`
  - 중괄호 `{}` 로 묶인 매개변수는 선택적 매개변수입니다.
  - `this.isCheckedOut = false` 는 기본값을 설정합니다.
- **`@override` 어노테이션**: 상위 클래스의 메서드를 재정의함을 나타냅니다.
- **`toString()` 메서드**: 화살표 함수 구문 `=>` 을 사용하여 간단히 표현했습니다.

## 2. Library 클래스

```dart
class Library {
  String name;
  List<Book> books = [];
  Map<String, List<Book>> booksByAuthor = {};

  Library(this.name);

  // 메서드들...
}
```

- `List<Book> books = [];`: Book 객체들의 리스트를 초기화합니다.
- `Map<String, List<Book>> booksByAuthor = {};`: 저자별로 책을 그룹화하는 맵을 초기화합니다.

### 주요 메서드

#### addBook 메서드

```dart
void addBook(Book book) {
  books.add(book);
  booksByAuthor.putIfAbsent(book.author, () => []).add(book);
}
```

- `books.add(book);`: 리스트에 책을 추가합니다.
- `booksByAuthor.putIfAbsent(book.author, () => []).add(book);`: 
  맵에 저자가 없으면 새 리스트를 생성하고, 책을 추가합니다.

#### checkOutBook 과 returnBook 메서드

```dart
bool checkOutBook(String title) {
  var book = books.firstWhere((b) => b.title == title, orElse: () => Book('', ''));
  if (book.title.isNotEmpty && !book.isCheckedOut) {
    book.isCheckedOut = true;
    return true;
  }
  return false;
}
```

- `firstWhere` 메서드로 책을 찾고, 없으면 빈 Book 객체를 반환합니다.
- 조건문으로 책의 상태를 확인하고 변경합니다.

#### getBooksByAuthor 메서드

```dart
List<Book> getBooksByAuthor(String author) {
  return booksByAuthor[author] ?? [];
}
```

- `??` 연산자는 null 안전성을 위해 사용됩니다. 왼쪽 값이 null이면 오른쪽 값을 반환합니다.

#### getAvailableBooks 메서드

```dart
List<Book> getAvailableBooks() {
  return books.where((book) => !book.isCheckedOut).toList();
}
```

- `where` 메서드로 조건에 맞는 책들을 필터링합니다.

## 3. main 함수

```dart
void main() {
  var library = Library('City Central Library');

  // 책 추가, 대출, 반납 등의 작업 수행
  // ...

  library.displayLibraryStats();
}
```

- 객체 생성, 메서드 호출, 결과 출력 등의 작업을 수행합니다.
- `forEach` 메서드로 리스트의 각 요소에 대해 작업을 수행합니다.

### @override toString()이 어디에서 쓰이고 있는지?
  - 객체를 문자열로 변환할 때:
    Dart에서는 객체를 문자열 컨텍스트에서 사용할 때 자동으로 toString() 메서드를 호출합니다.
  - print() 함수 사용 시:
    print() 함수에 객체를 전달하면, 해당 객체의 toString() 메서드가 자동으로 호출됩니다.
  - 문자열 보간에서:
    문자열 내에 $object나 ${object} 형태로 객체를 포함시킬 때 toString() 메서드가 호출됩니다.
  - example
    ```dart
    print('\nBooks by George Orwell:');
    library.getBooksByAuthor('George Orwell').forEach(print);
    
    print('\nAvailable books:');
    library.getAvailableBooks().forEach(print);
    ```
    - 여기서 forEach(print)를 사용할 때, 각 Book 객체가 print() 함수에 전달되면서 암시적으로 toString() 메서드가 호출됩니다.
    - 따라서, 직접적인 toString() 호출은 없지만, 이 메서드는 객체를 출력하거나 문자열로 표현해야 할 때 자동으로 사용됩니다.
