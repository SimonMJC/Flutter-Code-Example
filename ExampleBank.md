# 난이도 중하

## 1

```dart
import 'dart:async';

Future<String> fetchUserData(String userId) async {
  await Future.delayed(Duration(seconds: 2));
  if (userId == "123") {
    return "John Doe";
  } else {
    throw Exception("User not found");
  }
}

void main() async {
  try {
    print("Fetching user data...");
    String userData = await fetchUserData("123");
    print("User data: $userData");
    
    print("Fetching invalid user data...");
    String invalidUserData = await fetchUserData("456");
    print("Invalid user data: $invalidUserData");
  } catch (e) {
    print("Error occurred: $e");
  } finally {
    print("Operation completed");
  }
}
```

## 2 
```dart
class BankAccount {
  String accountHolder;
  double balance;

  BankAccount(this.accountHolder, this.balance);

  void deposit(double amount) {
    balance += amount;
    print('$amount원이 입금되었습니다. 현재 잔액: $balance원');
  }

  void withdraw(double amount) {
    if (amount > balance) {
      print('잔액이 부족합니다. 현재 잔액: $balance원');
    } else {
      balance -= amount;
      print('$amount원이 출금되었습니다. 현재 잔액: $balance원');
    }
  }

  void displayBalance() {
    print('$accountHolder님의 현재 잔액은 $balance원입니다.');
  }
}

void main() {
  var account = BankAccount('홍길동', 10000);

  account.displayBalance();
  account.deposit(5000);
  account.withdraw(3000);
  account.withdraw(15000);
}
```

## 3
```dart
import 'dart:collection';

class Product {
  String name;
  double price;

  Product(this.name, this.price);

  @override
  String toString() => '$name: \$${price.toStringAsFixed(2)}';
}

class ShoppingCart {
  final Map<Product, int> _items = LinkedHashMap<Product, int>();

  void addItem(Product product, [int quantity = 1]) {
    _items.update(product, (value) => value + quantity, ifAbsent: () => quantity);
  }

  void removeItem(Product product, [int quantity = 1]) {
    if (!_items.containsKey(product)) {
      print('${product.name} is not in the cart.');
      return;
    }
    
    _items.update(product, (value) {
      if (value <= quantity) {
        return 0;
      }
      return value - quantity;
    });
    
    _items.removeWhere((key, value) => value == 0);
  }

  double get totalPrice {
    return _items.entries.fold(0, (total, entry) => total + (entry.key.price * entry.value));
  }

  void displayCart() {
    if (_items.isEmpty) {
      print('Your cart is empty.');
    } else {
      print('Your shopping cart:');
      _items.forEach((product, quantity) {
        print('  ${product.name} x $quantity = \$${(product.price * quantity).toStringAsFixed(2)}');
      });
      print('Total: \$${totalPrice.toStringAsFixed(2)}');
    }
  }
}

void main() {
  var cart = ShoppingCart();
  var apple = Product('Apple', 0.5);
  var banana = Product('Banana', 0.3);
  var orange = Product('Orange', 0.6);

  cart.addItem(apple, 3);
  cart.addItem(banana, 2);
  cart.addItem(orange);
  cart.displayCart();

  print('\nRemoving 1 Apple and 2 Bananas:');
  cart.removeItem(apple);
  cart.removeItem(banana, 2);
  cart.displayCart();

  print('\nAdding more items:');
  cart.addItem(orange, 2);
  cart.displayCart();
}
```

## 4
```dart
import 'dart:io';

class Book {
  String title;
  String author;
  String isbn;
  bool isCheckedOut;

  Book(this.title, this.author, this.isbn, {this.isCheckedOut = false});

  void displayInfo() {
    print("제목: $title");
    print("저자: $author");
    print("ISBN: $isbn");
    print("대출 상태: ${isCheckedOut ? '대출 중' : '대출 가능'}");
  }
}

class Library {
  List<Book> books = [];

  void addBook(Book book) {
    books.add(book);
    print("'${book.title}' 도서가 추가되었습니다.");
  }

  void displayAllBooks() {
    if (books.isEmpty) {
      print("도서관에 책이 없습니다.");
    } else {
      print("\n도서 목록:");
      for (var i = 0; i < books.length; i++) {
        print("\n${i + 1}번 도서:");
        books[i].displayInfo();
      }
    }
  }

  void checkOutBook(int index) {
    if (index >= 0 && index < books.length) {
      if (!books[index].isCheckedOut) {
        books[index].isCheckedOut = true;
        print("'${books[index].title}' 도서가 대출되었습니다.");
      } else {
        print("이미 대출 중인 도서입니다.");
      }
    } else {
      print("잘못된 도서 번호입니다.");
    }
  }

  void returnBook(int index) {
    if (index >= 0 && index < books.length) {
      if (books[index].isCheckedOut) {
        books[index].isCheckedOut = false;
        print("'${books[index].title}' 도서가 반납되었습니다.");
      } else {
        print("이미 반납된 도서입니다.");
      }
    } else {
      print("잘못된 도서 번호입니다.");
    }
  }
}

void main() {
  var library = Library();

  library.addBook(Book("해리 포터와 마법사의 돌", "J.K. 롤링", "9788983920997"));
  library.addBook(Book("1984", "조지 오웰", "9788937460777"));
  library.addBook(Book("어린 왕자", "생텍쥐페리", "9788932917245"));

  while (true) {
    print("\n도서관 관리 시스템");
    print("1. 모든 도서 보기");
    print("2. 도서 대출");
    print("3. 도서 반납");
    print("4. 종료");
    stdout.write("선택: ");

    var choice = int.tryParse(stdin.readLineSync() ?? "");

    switch (choice) {
      case 1:
        library.displayAllBooks();
        break;
      case 2:
        stdout.write("대출할 도서 번호: ");
        var bookIndex = int.tryParse(stdin.readLineSync() ?? "") ?? -1;
        library.checkOutBook(bookIndex - 1);
        break;
      case 3:
        stdout.write("반납할 도서 번호: ");
        var bookIndex = int.tryParse(stdin.readLineSync() ?? "") ?? -1;
        library.returnBook(bookIndex - 1);
        break;
      case 4:
        print("프로그램을 종료합니다.");
        return;
      default:
        print("잘못된 선택입니다. 다시 선택해주세요.");
    }
  }
}
```

## 5
```dart
import 'dart:io';

class BankAccount {
  String accountNumber;
  String ownerName;
  double balance;

  BankAccount(this.accountNumber, this.ownerName, this.balance);

  void deposit(double amount) {
    if (amount > 0) {
      balance += amount;
      print("$amount원이 입금되었습니다. 현재 잔액: $balance원");
    } else {
      print("유효하지 않은 금액입니다.");
    }
  }

  bool withdraw(double amount) {
    if (amount > 0 && balance >= amount) {
      balance -= amount;
      print("$amount원이 출금되었습니다. 현재 잔액: $balance원");
      return true;
    } else {
      print("출금할 수 없습니다. 잔액 부족 또는 유효하지 않은 금액입니다.");
      return false;
    }
  }

  void displayInfo() {
    print("계좌번호: $accountNumber");
    print("예금주: $ownerName");
    print("잔액: $balance원");
  }
}

class Bank {
  List<BankAccount> accounts = [];

  void addAccount(BankAccount account) {
    accounts.add(account);
    print("새 계좌가 생성되었습니다.");
  }

  BankAccount? findAccount(String accountNumber) {
    return accounts.firstWhere(
      (account) => account.accountNumber == accountNumber,
      orElse: () => BankAccount("", "", 0)  // 더미 계좌 반환
    );
  }

  void transfer(String fromAccountNumber, String toAccountNumber, double amount) {
    var fromAccount = findAccount(fromAccountNumber);
    var toAccount = findAccount(toAccountNumber);

    if (fromAccount.accountNumber.isEmpty || toAccount.accountNumber.isEmpty) {
      print("계좌를 찾을 수 없습니다.");
      return;
    }

    if (fromAccount.withdraw(amount)) {
      toAccount.deposit(amount);
      print("이체가 완료되었습니다.");
    }
  }
}

void main() {
  var bank = Bank();

  bank.addAccount(BankAccount("1001", "홍길동", 10000));
  bank.addAccount(BankAccount("1002", "김철수", 20000));

  while (true) {
    print("\n은행 계좌 관리 시스템");
    print("1. 계좌 정보 조회");
    print("2. 입금");
    print("3. 출금");
    print("4. 계좌 이체");
    print("5. 종료");
    stdout.write("선택: ");

    var choice = int.tryParse(stdin.readLineSync() ?? "");

    switch (choice) {
      case 1:
        stdout.write("계좌번호: ");
        var accountNumber = stdin.readLineSync() ?? "";
        var account = bank.findAccount(accountNumber);
        if (account.accountNumber.isNotEmpty) {
          account.displayInfo();
        } else {
          print("계좌를 찾을 수 없습니다.");
        }
        break;
      case 2:
        stdout.write("계좌번호: ");
        var accountNumber = stdin.readLineSync() ?? "";
        stdout.write("입금액: ");
        var amount = double.tryParse(stdin.readLineSync() ?? "") ?? 0;
        var account = bank.findAccount(accountNumber);
        if (account.accountNumber.isNotEmpty) {
          account.deposit(amount);
        } else {
          print("계좌를 찾을 수 없습니다.");
        }
        break;
      case 3:
        stdout.write("계좌번호: ");
        var accountNumber = stdin.readLineSync() ?? "";
        stdout.write("출금액: ");
        var amount = double.tryParse(stdin.readLineSync() ?? "") ?? 0;
        var account = bank.findAccount(accountNumber);
        if (account.accountNumber.isNotEmpty) {
          account.withdraw(amount);
        } else {
          print("계좌를 찾을 수 없습니다.");
        }
        break;
      case 4:
        stdout.write("출금 계좌번호: ");
        var fromAccountNumber = stdin.readLineSync() ?? "";
        stdout.write("입금 계좌번호: ");
        var toAccountNumber = stdin.readLineSync() ?? "";
        stdout.write("이체액: ");
        var amount = double.tryParse(stdin.readLineSync() ?? "") ?? 0;
        bank.transfer(fromAccountNumber, toAccountNumber, amount);
        break;
      case 5:
        print("프로그램을 종료합니다.");
        return;
      default:
        print("잘못된 선택입니다. 다시 선택해주세요.");
    }
  }
}
```

## 6 
```dart
import 'dart:io';

class Question {
  String question;
  List<String> options;
  int correctAnswer;

  Question(this.question, this.options, this.correctAnswer);

  bool checkAnswer(int userAnswer) {
    return userAnswer == correctAnswer;
  }
}

class Quiz {
  List<Question> questions = [];
  int score = 0;

  void addQuestion(Question question) {
    questions.add(question);
  }

  void startQuiz() {
    for (var i = 0; i < questions.length; i++) {
      print("\n질문 ${i + 1}: ${questions[i].question}");
      for (var j = 0; j < questions[i].options.length; j++) {
        print("${j + 1}. ${questions[i].options[j]}");
      }

      stdout.write("답변 선택 (1-${questions[i].options.length}): ");
      var userAnswer = int.tryParse(stdin.readLineSync() ?? "") ?? 0;

      if (questions[i].checkAnswer(userAnswer)) {
        print("정답입니다!");
        score++;
      } else {
        print("틀렸습니다. 정답은 ${questions[i].correctAnswer}번입니다.");
      }
    }

    print("\n퀴즈 종료! 당신의 점수: $score / ${questions.length}");
  }
}

void main() {
  var quiz = Quiz();

  quiz.addQuestion(Question(
    "다트(Dart)의 개발사는?",
    ["Apple", "Google", "Microsoft", "Facebook"],
    2
  ));

  quiz.addQuestion(Question(
    "다트의 주요 용도는?",
    ["웹 개발", "모바일 앱 개발", "데스크톱 앱 개발", "모두"],
    4
  ));

  quiz.addQuestion(Question(
    "다트에서 'final'과 'const'의 차이점은?",
    ["차이 없음", "final은 런타임에, const는 컴파일 타임에 값이 결정됨", "const는 런타임에, final은 컴파일 타임에 값이 결정됨", "final은 변경 가능, const는 변경 불가능"],
    2
  ));

  print("간단한 퀴즈 게임을 시작합니다!");
  quiz.startQuiz();
}
```

## 7
- 해당코드는 실행해보면서 해석해도 좋을 듯
```dart
import 'dart:io';

class MenuItem {
  String name;
  double price;

  MenuItem(this.name, this.price);
}

class Order {
  List<MenuItem> items = [];

  void addItem(MenuItem item) {
    items.add(item);
    print("${item.name}이(가) 주문에 추가되었습니다.");
  }

  double getTotalPrice() {
    return items.fold(0, (sum, item) => sum + item.price);
  }

  void displayOrder() {
    if (items.isEmpty) {
      print("주문 내역이 없습니다.");
    } else {
      print("주문 내역:");
      for (var item in items) {
        print("${item.name}: \$${item.price}");
      }
      print("총 금액: \$${getTotalPrice()}");
    }
  }
}

class Restaurant {
  List<MenuItem> menu = [
    MenuItem("햄버거", 5.99),
    MenuItem("피자", 8.99),
    MenuItem("샐러드", 4.99),
    MenuItem("음료", 1.99)
  ];

  void displayMenu() {
    print("메뉴:");
    for (var i = 0; i < menu.length; i++) {
      print("${i + 1}. ${menu[i].name}: \$${menu[i].price}");
    }
  }
}

void main() {
  var restaurant = Restaurant();
  var order = Order();

  while (true) {
    print("\n음식 주문 시스템");
    print("1. 메뉴 보기");
    print("2. 주문하기");
    print("3. 주문 확인");
    print("4. 종료");
    stdout.write("선택: ");

    var choice = int.tryParse(stdin.readLineSync() ?? "");

    switch (choice) {
      case 1:
        restaurant.displayMenu();
        break;
      case 2:
        restaurant.displayMenu();
        stdout.write("주문할 메뉴 번호: ");
        var menuIndex = int.tryParse(stdin.readLineSync() ?? "") ?? 0;
        if (menuIndex > 0 && menuIndex <= restaurant.menu.length) {
          order.addItem(restaurant.menu[menuIndex - 1]);
        } else {
          print("잘못된 메뉴 번호입니다.");
        }
        break;
      case 3:
        order.displayOrder();
        break;
      case 4:
        print("프로그램을 종료합니다.");
        return;
      default:
        print("잘못된 선택입니다.");
    }
  }
}

```

# Collection Example

## 8
```dart
class Student {
  String name;
  List<int> scores;

  Student(this.name, this.scores);

  double get average => scores.isEmpty ? 0 : scores.reduce((a, b) => a + b) / scores.length;
}

void main() {
  var students = [
    Student('Alice', [85, 90, 78]),
    Student('Bob', [92, 88, 95]),
    Student('Charlie', [76, 80, 85])
  ];

  students.sort((a, b) => b.average.compareTo(a.average));

  print('학생 성적 순위:');
  for (var student in students) {
    print('${student.name}: 평균 ${student.average.toStringAsFixed(2)}');
  }

  var topStudent = students.first;
  print('\n최고 성적 학생: ${topStudent.name}, 평균: ${topStudent.average.toStringAsFixed(2)}');
}
```

## 9
```
class Book {
  String title;
  String author;
  int year;

  Book(this.title, this.author, this.year);
}

void main() {
  var books = [
    Book('1984', 'George Orwell', 1949),
    Book('To Kill a Mockingbird', 'Harper Lee', 1960),
    Book('The Great Gatsby', 'F. Scott Fitzgerald', 1925)
  ];

  var recentBooks = books.where((book) => book.year > 1950).toList();

  print('1950년 이후 출판된 책:');
  for (var book in recentBooks) {
    print('${book.title} by ${book.author} (${book.year})');
  }

  var oldestBook = books.reduce((a, b) => a.year < b.year ? a : b);
  print('\n가장 오래된 책: ${oldestBook.title} (${oldestBook.year})');
}
```

## 10
```dart
class Item {
  String name;
  double price;

  Item(this.name, this.price);
}

void main() {
  var shoppingCart = [
    Item('Apple', 0.5),
    Item('Banana', 0.3),
    Item('Orange', 0.6),
    Item('Milk', 2.5)
  ];

  var totalPrice = shoppingCart.fold(0.0, (sum, item) => sum + item.price);

  print('장바구니 내역:');
  for (var item in shoppingCart) {
    print('${item.name}: \$${item.price}');
  }

  print('\n총 가격: \$${totalPrice.toStringAsFixed(2)}');

  var mostExpensiveItem = shoppingCart.reduce((a, b) => a.price > b.price ? a : b);
  print('가장 비싼 물품: ${mostExpensiveItem.name} (\$${mostExpensiveItem.price})');
}
```

## 11
```dart
class Song {
  String title;
  String artist;
  int duration; // 초 단위

  Song(this.title, this.artist, this.duration);

  @override
  String toString() => '$title by $artist';
}

class Playlist {
  String name;
  List<Song> songs = [];

  Playlist(this.name);

  void addSong(Song song) {
    songs.add(song);
  }

  void removeSong(Song song) {
    songs.remove(song);
  }

  int get totalDuration => songs.fold(0, (sum, song) => sum + song.duration);

  void shuffle() {
    songs.shuffle();
  }

  List<Song> searchByArtist(String artist) {
    return songs.where((song) => song.artist.toLowerCase().contains(artist.toLowerCase())).toList();
  }

  void displayPlaylist() {
    print('Playlist: $name');
    for (var i = 0; i < songs.length; i++) {
      print('${i + 1}. ${songs[i]}');
    }
    print('Total duration: ${totalDuration ~/ 60} minutes ${totalDuration % 60} seconds');
  }
}

void main() {
  var myPlaylist = Playlist('My Favorite Songs');

  myPlaylist.addSong(Song('Shape of You', 'Ed Sheeran', 235));
  myPlaylist.addSong(Song('Blinding Lights', 'The Weeknd', 200));
  myPlaylist.addSong(Song('Dance Monkey', 'Tones and I', 209));
  myPlaylist.addSong(Song('Someone You Loved', 'Lewis Capaldi', 182));
  myPlaylist.addSong(Song('Watermelon Sugar', 'Harry Styles', 174));

  myPlaylist.displayPlaylist();

  print('\nSearching for songs by "The Weeknd":');
  var weekndSongs = myPlaylist.searchByArtist('The Weeknd');
  weekndSongs.forEach(print);

  myPlaylist.shuffle();
  print('\nAfter shuffling:');
  myPlaylist.displayPlaylist();
}
```


## 12
```dart
class Student {
  String name;
  int grade;
  List<int> scores;

  Student(this.name, this.grade, this.scores);

  double get average => scores.isEmpty ? 0 : scores.reduce((a, b) => a + b) / scores.length;
}

class School {
  String name;
  Map<int, List<Student>> studentsByGrade = {};

  School(this.name);

  void addStudent(Student student) {
    studentsByGrade.putIfAbsent(student.grade, () => []).add(student);
  }

  List<Student> getStudentsByGrade(int grade) {
    return studentsByGrade[grade] ?? [];
  }

  Student? getTopStudent() {
    return studentsByGrade.values
        .expand((students) => students)
        .reduce((a, b) => a.average > b.average ? a : b);
  }

  Map<int, double> getAverageScoresByGrade() {
    return studentsByGrade.map((grade, students) {
      var averageScore = students.isEmpty
          ? 0.0
          : students.map((s) => s.average).reduce((a, b) => a + b) / students.length;
      return MapEntry(grade, averageScore);
    });
  }

  void displaySchoolStats() {
    print('School: $name');
    studentsByGrade.forEach((grade, students) {
      print('Grade $grade: ${students.length} students');
    });
    print('Total students: ${studentsByGrade.values.expand((s) => s).length}');
  }
}

void main() {
  var mySchool = School('Springfield Elementary');

  mySchool.addStudent(Student('Bart Simpson', 4, [65, 70, 60]));
  mySchool.addStudent(Student('Lisa Simpson', 2, [95, 98, 97]));
  mySchool.addStudent(Student('Milhouse Van Houten', 4, [72, 78, 75]));
  mySchool.addStudent(Student('Ralph Wiggum', 2, [55, 60, 52]));
  mySchool.addStudent(Student('Martin Prince', 4, [98, 99, 97]));

  mySchool.displaySchoolStats();

  print('\nTop student: ${mySchool.getTopStudent()?.name}');

  print('\nAverage scores by grade:');
  mySchool.getAverageScoresByGrade().forEach((grade, average) {
    print('Grade $grade: ${average.toStringAsFixed(2)}');
  });
}
```


## 13
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

# 난이도 중

## 14
```dart
class WeatherCondition {
  String description;
  double temperature;
  int humidity;

  WeatherCondition(this.description, this.temperature, this.humidity);

  void display() {
    print('날씨: $description');
    print('온도: ${temperature.toStringAsFixed(1)}°C');
    print('습도: $humidity%');
  }
}

class WeatherForecast {
  List<WeatherCondition> forecast = [];

  void addForecast(WeatherCondition condition) {
    forecast.add(condition);
    print('날씨 예보가 추가되었습니다.');
  }

  void displayForecast() {
    if (forecast.isEmpty) {
      print('예보 정보가 없습니다.');
    } else {
      for (var i = 0; i < forecast.length; i++) {
        print('\n${i + 1}일 후 날씨:');
        forecast[i].display();
      }
    }
  }

  WeatherCondition? findHottestDay() {
    if (forecast.isEmpty) return null;
    return forecast.reduce((curr, next) => 
        curr.temperature > next.temperature ? curr : next);
  }

  double getAverageTemperature() {
    if (forecast.isEmpty) return 0;
    var sum = 0.0;
    for (var condition in forecast) {
      sum += condition.temperature;
    }
    return sum / forecast.length;
  }
}

void main() {
  var weatherSystem = WeatherForecast();

  weatherSystem.addForecast(WeatherCondition('맑음', 28.5, 65));
  weatherSystem.addForecast(WeatherCondition('흐림', 25.0, 80));
  weatherSystem.addForecast(WeatherCondition('비', 22.8, 90));

  weatherSystem.displayForecast();

  var hottestDay = weatherSystem.findHottestDay();
  if (hottestDay != null) {
    print('\n가장 더운 날:');
    hottestDay.display();
  }

  print('\n평균 기온: ${weatherSystem.getAverageTemperature().toStringAsFixed(1)}°C');
}
```

## 15
```dart
class Ingredient {
  String name;
  double amount;
  String unit;

  Ingredient(this.name, this.amount, this.unit);

  @override
  String toString() => '$amount $unit의 $name';
}

class Recipe {
  String name;
  List<Ingredient> ingredients;
  List<String> steps;

  Recipe(this.name, this.ingredients, this.steps);

  void displayRecipe() {
    print('\n=== $name 레시피 ===');
    print('재료:');
    for (var ingredient in ingredients) {
      print('- $ingredient');
    }
    print('\n조리 단계:');
    for (var i = 0; i < steps.length; i++) {
      print('${i + 1}. ${steps[i]}');
    }
  }

  void scaleRecipe(double factor) {
    for (var ingredient in ingredients) {
      ingredient.amount *= factor;
    }
    print('\n$name 레시피의 양을 ${factor}배로 조정했습니다.');
  }
}

class Cookbook {
  List<Recipe> recipes = [];

  void addRecipe(Recipe recipe) {
    recipes.add(recipe);
    print('${recipe.name} 레시피가 요리책에 추가되었습니다.');
  }

  void displayAllRecipes() {
    print('\n=== 요리책 내용 ===');
    for (var i = 0; i < recipes.length; i++) {
      print('${i + 1}. ${recipes[i].name}');
    }
  }

  Recipe? findRecipe(String name) {
    return recipes.firstWhere(
      (recipe) => recipe.name.toLowerCase() == name.toLowerCase(),
      orElse: () => null as Recipe
    );
  }
}

void main() {
  var cookbook = Cookbook();

  var pancakeRecipe = Recipe(
    '팬케이크',
    [
      Ingredient('밀가루', 200, '그램'),
      Ingredient('우유', 300, '밀리리터'),
      Ingredient('달걀', 2, '개'),
    ],
    [
      '모든 재료를 섞어 반죽을 만듭니다.',
      '팬을 달구고 기름을 두릅니다.',
      '반죽을 팬에 부어 노릇해질 때까지 굽습니다.',
    ]
  );

  cookbook.addRecipe(pancakeRecipe);
  cookbook.displayAllRecipes();

  var recipe = cookbook.findRecipe('팬케이크');
  if (recipe != null) {
    recipe.displayRecipe();
    recipe.scaleRecipe(2);
    recipe.displayRecipe();
  } else {
    print('레시피를 찾을 수 없습니다.');
  }
}
```

# 비동기

네, 이전에 제공한 전체 코드, 주요 기능, 상세한 설명에 비동기 관련 문법 설명을 덧붙여 마크다운 형식으로 정리해드리겠습니다.

## 1. 비동기적으로 숫자 리스트 처리하기

### 전체 코드
```dart
import 'dart:async';

Future<int> processNumber(int num) async {
  await Future.delayed(Duration(seconds: 1));
  return num * 2;
}

void main() async {
  final numbers = [1, 2, 3, 4, 5];
  
  print('Processing numbers...');
  final results = await Future.wait(numbers.map(processNumber));
  
  print('Original numbers: $numbers');
  print('Processed numbers: $results');
  
  final sum = results.reduce((a, b) => a + b);
  print('Sum of processed numbers: $sum');
}
```

### 주요 기능

1. 비동기 함수 정의:
   ```dart
   Future<int> processNumber(int num) async {
     await Future.delayed(Duration(seconds: 1));
     return num * 2;
   }
   ```

2. 리스트 매핑과 비동기 처리:
   ```dart
   final results = await Future.wait(numbers.map(processNumber));
   ```

3. 리스트 축소:
   ```dart
   final sum = results.reduce((a, b) => a + b);
   ```

### 상세 설명

1. `processNumber` 함수는 입력 숫자를 1초 지연 후 2배로 만듭니다:
   ```dart
   Future<int> processNumber(int num) async {
     await Future.delayed(Duration(seconds: 1));
     return num * 2;
   }
   ```

2. `main` 함수에서 숫자 리스트를 정의하고 처리합니다:
   ```dart
   final numbers = [1, 2, 3, 4, 5];
   final results = await Future.wait(numbers.map(processNumber));
   ```

3. 처리된 결과의 합을 계산합니다:
   ```dart
   final sum = results.reduce((a, b) => a + b);
   ```

### 비동기 관련 문법 설명

1. `async` 키워드:
   ```dart
   Future<int> processNumber(int num) async {
     // ...
   }
   ```
   - `async` 키워드는 함수가 비동기적으로 동작함을 나타냅니다.
   - 이 함수는 `Future<int>`를 반환합니다.

2. `await` 키워드:
   ```dart
   await Future.delayed(Duration(seconds: 1));
   ```
   - `await`는 `Future`가 완료될 때까지 실행을 일시 중지합니다.
   - 여기서는 1초간 지연을 기다립니다.

3. `Future.wait`:
   ```dart
   final results = await Future.wait(numbers.map(processNumber));
   ```
   - `Future.wait`는 여러 `Future`를 동시에 실행하고 모든 결과를 기다립니다.
   - `numbers.map(processNumber)`는 각 숫자에 대해 `processNumber` 함수를 호출하여 `Future<int>` 리스트를 생성합니다.
   - `await`를 사용하여 모든 `Future`가 완료될 때까지 기다립니다.

## 2. 비동기 필터링 및 매핑

### 전체 코드
```dart
Future<String> fetchUserName(int id) async {
  await Future.delayed(Duration(milliseconds: 500));
  return 'User$id';
}

void main() async {
  final userIds = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
  
  final evenUserIds = userIds.where((id) => id.isEven);
  
  print('Fetching user names for even IDs...');
  final userNames = await Future.wait(evenUserIds.map(fetchUserName));
  
  print('Even user IDs: $evenUserIds');
  print('Fetched user names: $userNames');
  
  final userMap = Map.fromIterables(evenUserIds, userNames);
  userMap.forEach((id, name) => print('ID: $id, Name: $name'));
}
```

### 주요 기능

1. 리스트 필터링:
   ```dart
   final evenUserIds = userIds.where((id) => id.isEven);
   ```

2. 비동기 매핑:
   ```dart
   final userNames = await Future.wait(evenUserIds.map(fetchUserName));
   ```

3. 맵 생성:
   ```dart
   final userMap = Map.fromIterables(evenUserIds, userNames);
   ```

### 상세 설명

1. 짝수 ID만 필터링합니다:
   ```dart
   final evenUserIds = userIds.where((id) => id.isEven);
   ```

2. 필터링된 ID에 대해 사용자 이름을 비동기적으로 가져옵니다:
   ```dart
   final userNames = await Future.wait(evenUserIds.map(fetchUserName));
   ```

3. ID와 이름으로 맵을 생성하고 출력합니다:
   ```dart
   final userMap = Map.fromIterables(evenUserIds, userNames);
   userMap.forEach((id, name) => print('ID: $id, Name: $name'));
   ```

### 비동기 관련 문법 설명

1. `async` 함수:
   ```dart
   Future<String> fetchUserName(int id) async {
     // ...
   }
   ```
   - 이 함수는 `Future<String>`을 반환하는 비동기 함수입니다.

2. `Future.delayed`:
   ```dart
   await Future.delayed(Duration(milliseconds: 500));
   ```
   - 네트워크 요청을 시뮬레이션하기 위해 500밀리초 지연을 생성합니다.

3. `Future.wait`와 `map`:
   ```dart
   final userNames = await Future.wait(evenUserIds.map(fetchUserName));
   ```
   - `evenUserIds.map(fetchUserName)`은 각 ID에 대해 `fetchUserName`을 호출하여 `Future<String>` 리스트를 생성합니다.
   - `Future.wait`는 모든 `Future`가 완료될 때까지 기다린 후, 결과를 리스트로 반환합니다.

## 3. 비동기 리스트 변환 및 필터링

### 전체 코드
```dart
Future<Map<String, int>> fetchWordCount(String word) async {
  await Future.delayed(Duration(milliseconds: 300));
  return {word: word.length};
}

void main() async {
  final words = ['apple', 'banana', 'cherry', 'date', 'elderberry'];
  
  print('Fetching word counts...');
  final wordCounts = await Future.wait(words.map(fetchWordCount));
  
  final flattenedCounts = Map.fromEntries(wordCounts.expand((map) => map.entries));
  print('Word counts: $flattenedCounts');
  
  final longWords = flattenedCounts.entries
      .where((entry) => entry.value > 5)
      .map((entry) => entry.key)
      .toList();
  
  print('Words with more than 5 characters: $longWords');
}
```

### 주요 기능

1. 비동기 매핑:
   ```dart
   final wordCounts = await Future.wait(words.map(fetchWordCount));
   ```

2. 맵 평탄화:
   ```dart
   final flattenedCounts = Map.fromEntries(wordCounts.expand((map) => map.entries));
   ```

3. 필터링 및 변환:
   ```dart
   final longWords = flattenedCounts.entries
       .where((entry) => entry.value > 5)
       .map((entry) => entry.key)
       .toList();
   ```

### 상세 설명

1. 각 단어의 길이를 비동기적으로 가져옵니다:
   ```dart
   final wordCounts = await Future.wait(words.map(fetchWordCount));
   ```

2. 결과를 하나의 맵으로 평탄화합니다:
   ```dart
   final flattenedCounts = Map.fromEntries(wordCounts.expand((map) => map.entries));
   ```

3. 5글자 초과 단어만 필터링하여 새 리스트를 만듭니다:
   ```dart
   final longWords = flattenedCounts.entries
       .where((entry) => entry.value > 5)
       .map((entry) => entry.key)
       .toList();
   ```

### 비동기 관련 문법 설명

1. 비동기 함수 정의:
   ```dart
   Future<Map<String, int>> fetchWordCount(String word) async {
     // ...
   }
   ```
   - 이 함수는 `Future<Map<String, int>>`를 반환합니다.

2. `Future.wait`와 `map` 조합:
   ```dart
   final wordCounts = await Future.wait(words.map(fetchWordCount));
   ```
   - `words.map(fetchWordCount)`는 각 단어에 대해 `fetchWordCount`를 호출하여 `Future<Map<String, int>>` 리스트를 생성합니다.
   - `Future.wait`는 모든 비동기 작업이 완료될 때까지 기다립니다.

3. 비동기 결과 처리:
   ```dart
   final flattenedCounts = Map.fromEntries(wordCounts.expand((map) => map.entries));
   ```
   - 비동기 작업의 결과를 동기적으로 처리합니다.
   - `expand`를 사용하여 중첩된 맵 엔트리를 평탄화합니다.

## 4. 비동기 리스트 정렬

### 전체 코드
```dart
Future<double> fetchPrice(String item) async {
  await Future.delayed(Duration(milliseconds: 200));
  return {'apple': 0.5, 'banana': 0.3, 'cherry': 0.8}[item] ?? 0.0;
}

void main() async {
  final fruits = ['banana', 'cherry', 'apple', 'date', 'elderberry'];
  
  print('Fetching fruit prices...');
  final prices = await Future.wait(fruits.map(fetchPrice));
  
  final fruitPrices = List.generate(fruits.length, (index) => 
      {'fruit': fruits[index], 'price': prices[index]});
  
  fruitPrices.sort((a, b) => a['price']!.compareTo(b['price']!));
  
  print('Fruits sorted by price:');
  fruitPrices.forEach((item) => 
      print('${item['fruit']}: \$${item['price']!.toStringAsFixed(2)}'));
}
```

### 주요 기능

1. 비동기 데이터 가져오기:
   ```dart
   final prices = await Future.wait(fruits.map(fetchPrice));
   ```

2. 리스트 생성:
   ```dart
   final fruitPrices = List.generate(fruits.length, (index) => 
       {'fruit': fruits[index], 'price': prices[index]});
   ```

3. 리스트 정렬:
   ```dart
   fruitPrices.sort((a, b) => a['price']!.compareTo(b['price']!));
   ```

### 상세 설명

1. 과일 가격을 비동기적으로 가져옵니다:
   ```dart
   final prices = await Future.wait(fruits.map(fetchPrice));
   ```

2. 과일과 가격을 포함하는 맵 리스트를 생성합니다:
   ```dart
   final fruitPrices = List.generate(fruits.length, (index) => 
       {'fruit': fruits[index], 'price': prices[index]});
   ```

3. 가격을 기준으로 리스트를 정렬하고 출력합니다:
   ```dart
   fruitPrices.sort((a, b) => a['price']!.compareTo(b['price']!));
   fruitPrices.forEach((item) => 
       print('${item['fruit']}: \$${item['price']!.toStringAsFixed(2)}'));
   ```

### 비동기 관련 문법 설명

1. 비동기 함수 정의:
   ```dart
   Future<double> fetchPrice(String item) async {
     // ...
   }
   ```
   - 이 함수는 `Future<double>`을 반환합니다.

2. `Future.wait`를 사용한 병렬 처리:
   ```dart
   final prices = await Future.wait(fruits.map(fetchPrice));
   ```
   - 모든 과일 가격을 동시에 비동기적으로 가져옵니다.
   - `fruits.map(fetchPrice)`는 각 과일에 대해 `fetchPrice`를 호출하여 `Future<double>` 리스트를 생성합니다.

3. 비동기 결과 처리:
   ```dart
   final fruitPrices = List.generate(fruits.length, (index) => 
       {'fruit': fruits[index], 'price': prices[index]});
   ```
   - 비동기적으로 가져온 가격 정보를 동기적으로 처리하여 새로운 리스트를 생성합니다.


## 5. 비동기 리스트 그룹화

### 전체 코드
```dart
Future<String> fetchCategory(String item) async {
  await Future.delayed(Duration(milliseconds: 150));
  final categories = {
    'apple': 'fruit', 'carrot': 'vegetable', 'chicken': 'meat',
    'broccoli': 'vegetable', 'banana': 'fruit', 'beef': 'meat'
  };
  return categories[item] ?? 'unknown';
}

void main() async {
  final items = ['apple', 'carrot', 'chicken', 'broccoli', 'banana', 'beef'];
  
  print('Fetching item categories...');
  final categories = await Future.wait(items.map(fetchCategory));
  
  final groupedItems = <String, List<String>>{};
  for (var i = 0; i < items.length; i++) {
    groupedItems.putIfAbsent(categories[i], () => []).add(items[i]);
  }
  
  print('Grouped items by category:');
  groupedItems.forEach((category, items) {
    print('$category: ${items.join(', ')}');
  });
}
```

### 주요 기능

1. 비동기 데이터 가져오기:
   ```dart
   final categories = await Future.wait(items.map(fetchCategory));
   ```

2. 맵을 사용한 그룹화:
   ```dart
   final groupedItems = <String, List<String>>{};
   for (var i = 0; i < items.length; i++) {
     groupedItems.putIfAbsent(categories[i], () => []).add(items[i]);
   }
   ```

3. 그룹화된 결과 출력:
   ```dart
   groupedItems.forEach((category, items) {
     print('$category: ${items.join(', ')}');
   });
   ```

### 상세 설명

1. 각 아이템의 카테고리를 비동기적으로 가져옵니다:
   ```dart
   final categories = await Future.wait(items.map(fetchCategory));
   ```

2. 카테고리별로 아이템을 그룹화합니다:
   ```dart
   final groupedItems = <String, List<String>>{};
   for (var i = 0; i < items.length; i++) {
     groupedItems.putIfAbsent(categories[i], () => []).add(items[i]);
   }
   ```

3. 그룹화된 결과를 출력합니다:
   ```dart
   groupedItems.forEach((category, items) {
     print('$category: ${items.join(', ')}');
   });
   ```

### 비동기 관련 문법 설명

1. 비동기 함수 정의:
   ```dart
   Future<String> fetchCategory(String item) async {
     // ...
   }
   ```
   - 이 함수는 `Future<String>`을 반환합니다.
   - `async` 키워드는 이 함수가 비동기적으로 동작함을 나타냅니다.

2. `Future.delayed`:
   ```dart
   await Future.delayed(Duration(milliseconds: 150));
   ```
   - 네트워크 요청을 시뮬레이션하기 위해 150밀리초 지연을 생성합니다.
   - `await`는 이 지연이 완료될 때까지 함수의 실행을 일시 중지합니다.

3. `Future.wait`를 사용한 병렬 처리:
   ```dart
   final categories = await Future.wait(items.map(fetchCategory));
   ```
   - `items.map(fetchCategory)`는 각 아이템에 대해 `fetchCategory`를 호출하여 `Future<String>` 리스트를 생성합니다.
   - `Future.wait`는 모든 `Future`가 완료될 때까지 기다린 후, 결과를 리스트로 반환합니다.
   - `await`를 사용하여 모든 카테고리 정보가 준비될 때까지 기다립니다.

4. 비동기 결과 처리:
   ```dart
   for (var i = 0; i < items.length; i++) {
     groupedItems.putIfAbsent(categories[i], () => []).add(items[i]);
   }
   ```
   - 비동기적으로 가져온 카테고리 정보를 사용하여 동기적으로 아이템을 그룹화합니다.
   - `putIfAbsent`를 사용하여 새 카테고리를 만들거나 기존 카테고리에 아이템을 추가합니다.

이 예제는 비동기 작업의 결과를 효율적으로 처리하고 구조화하는 방법을 보여줍니다. `Future.wait`를 사용하여 여러 비동기 작업을 병렬로 처리하고, 그 결과를 동기적으로 정리하여 의미 있는 데이터 구조를 만듭니다.
