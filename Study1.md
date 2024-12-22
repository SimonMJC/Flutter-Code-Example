- # appetizer
    
    ```jsx
    void main() {
      List<int> numbers = [1, 2, 3, 4, 5];
      int sum = 0;
      
      for (var number in numbers) {
        sum += number;
      }
      
      print('합계: $sum');
      
      numbers.forEach((number) {
        if (number % 2 == 0) {
          print('$number는 짝수입니다.');
        } else {
          print('$number는 홀수입니다.');
        }
      });
      
      var doubledNumbers = numbers.map((number) => number * 2).toList();
      print('두 배로 증가된 숫자들: $doubledNumbers');
    }
    ```
    
    - 해석
        
        ## **코드 해석**
        
        1. **`main()`** 함수:
            - Dart 프로그램의 진입점입니다.
        2. **`List<int> numbers = [1, 2, 3, 4, 5];`**:
            - 정수형 리스트를 선언하고 초기화합니다.
        3. **`int sum = 0;`**:
            - 합계를 저장할 변수를 초기화합니다.
        4. **`for`** 루프:
            - 리스트의 모든 요소를 순회하며 합계를 계산합니다.
        5. **`print('합계: $sum');`**:
            - 계산된 합계를 출력합니다. 문자열 보간법을 사용합니다.
        6. **`numbers.forEach()`** 메서드:
            - 리스트의 각 요소에 대해 함수를 실행합니다.
            - 각 숫자가 짝수인지 홀수인지 판별하여 출력합니다.
        7. **`numbers.map()`** 메서드:
            - 리스트의 각 요소를 변환하여 새로운 리스트를 생성합니다.
            - 여기서는 각 숫자를 2배로 증가시킵니다.
        8. **`toList()`**:
            - map()의 결과를 리스트로 변환합니다.
        9. 마지막 **`print`** 문:
            - 변환된 리스트를 출력합니다.
        
        이 코드는 리스트 조작, 반복문, 조건문, 그리고 함수형 프로그래밍 기법을 보여줍니다. 학생들은 이 코드를 분석하면서 Dart의 다양한 기능과 문법을 이해할 수 있습니다.
        
- # main dish
    
    ```dart
    class Student {
      String name;
      int age;
      List<int> grades;
    
      Student(this.name, this.age, this.grades);
    }
    
    List<Student> students = [];
    
    void addStudent(String name, int age, List<int> grades) {
      students.add(Student(name, age, grades));
      print('$name 학생이 추가되었습니다.');
    }
    
    double calculateAverage(List<int> grades) {
      if (grades.isEmpty) return 0;
      return grades.reduce((a, b) => a + b) / grades.length;
    }
    
    void printStudentInfo(Student student) {
      print('이름: ${student.name}, 나이: ${student.age}');
      print('평균 점수: ${calculateAverage(student.grades).toStringAsFixed(2)}');
    }
    
    Student? findTopStudent() {
      if (students.isEmpty) return null;
      return students.reduce((a, b) => 
        calculateAverage(a.grades) > calculateAverage(b.grades) ? a : b);
    }
    
    void main() {
      addStudent('김철수', 20, [85, 90, 78]);
      addStudent('이영희', 22, [92, 88, 95]);
      addStudent('박민수', 21, [76, 85, 90]);
    
      print('\n모든 학생 정보:');
      students.forEach(printStudentInfo);
    
      print('\n최고 성적 학생:');
      Student? topStudent = findTopStudent();
      if (topStudent != null) {
        printStudentInfo(topStudent);
      } else {
        print('학생이 없습니다.');
      }
    }
    ```
    
    - 해석
        
        ## **클래스 정의**
        
        - `Student` 클래스를 정의합니다.
        - 각 학생은 이름(`name`), 나이(`age`), 성적 리스트(`grades`)를 가집니다.
        - 생성자를 통해 객체 생성 시 이 값들을 초기화할 수 있습니다.
        
        ## **전역 변수**
        
        `dartList<Student> students = [];`
        
        - 학생들의 정보를 저장할 전역 리스트를 선언합니다.
        
        ## **함수 정의**
        
        1. 학생 추가 함수 `addStudent`
            - 새로운 학생을 `students` 리스트에 추가하는 함수입니다.
            - 학생 추가 후 확인 메시지를 출력합니다.
        2. 평균 계산 함수 `calculateAverage`
            - 주어진 성적 리스트의 평균을 계산합니다.
            - `reduce` 메서드를 사용하여 모든 성적을 합산한 후, 개수로 나눕니다.
            - 성적이 없는 경우 0을 반환합니다.
        3. 학생 정보 출력 함수 `printStudentInfo`
            - 학생의 이름, 나이, 평균 점수를 출력합니다.
            - `calculateAverage` 함수를 호출하여 평균을 계산합니다.
            - `toStringAsFixed(2)`를 사용하여 소수점 둘째 자리까지 표시합니다.
        4. 최고 성적 학생 찾기 함수 `findTopStudent`
            - 가장 높은 평균 점수를 가진 학생을 찾습니다.
            - `reduce` 메서드를 사용하여 모든 학생을 비교합니다.
            - 학생이 없는 경우 `null`을 반환합니다.
        5. 메인 함수
        - 세 명의 학생을 추가합니다.
        - 모든 학생의 정보를 출력합니다.
        - 최고 성적을 받은 학생을 찾아 그 정보를 출력합니다.
        - Null 안전성을 고려하여 `topStudent`가 `null`이 아닌 경우에만 정보를 출력합니다.
- dessert Code(homework)
    
    ```dart
    import 'dart:async';
    
    class Todo {
      String id;
      String title;
      bool isCompleted;
    
      Todo(this.id, this.title, this.isCompleted);
    }
    
    class TodoService {
      final List<Todo> _todos = [];
      final _todoController = StreamController<List<Todo>>.broadcast();
    
      Stream<List<Todo>> get todos => _todoController.stream;
    
      void addTodo(String title) {
        final todo = Todo(DateTime.now().toString(), title, false);
        _todos.add(todo);
        _todoController.add(_todos);
      }
    
      void toggleTodo(String id) {
        final todo = _todos.firstWhere((todo) => todo.id == id);
        todo.isCompleted = !todo.isCompleted;
        _todoController.add(_todos);
      }
    
      void removeTodo(String id) {
        _todos.removeWhere((todo) => todo.id == id);
        _todoController.add(_todos);
      }
    
      void dispose() {
        _todoController.close();
      }
    }
    
    void main() {
      final todoService = TodoService();
    
      todoService.todos.listen((todos) {
        print('할 일 목록 업데이트:');
        for (var todo in todos) {
          print('${todo.title} - ${todo.isCompleted ? "완료" : "미완료"}');
        }
        print('---');
      });
    
      todoService.addTodo('Flutter 공부하기');
      todoService.addTodo('Dart 코드 작성하기');
      todoService.toggleTodo(todoService._todos[0].id);
      todoService.removeTodo(todoService._todos[1].id);
    
      todoService.dispose();
    }
    ```
    
    - 해석
        1. **`Todo` 클래스**
            - `Todo` 클래스는 각 할 일 항목을 표현합니다.
            - `id`: 각 할 일의 고유 식별자입니다.
            - `title`: 할 일의 제목 또는 내용입니다.
            - `isCompleted`: 할 일의 완료 여부를 나타내는 불리언 값입니다.
            - 생성자는 이 세 가지 속성을 초기화합니다.
        2. **`TodoService` 클래스**
            - `_todos`: 할 일 목록을 저장하는 private 리스트입니다.
            - `_todoController`: `StreamController`를 사용하여 할 일 목록의 변경사항을 방출합니다.
            - `todos`: 외부에서 할 일 목록의 변경을 구독할 수 있는 `Stream`을 제공합니다.
        3. `addTodo` 메서드
            - 새로운 `Todo` 객체를 생성합니다. `id`**는** 현재 시간을 문자열로 변환하여 사용합니다.
            - 생성된 `Todo`를 `_todos` 리스트에 추가합니다.
            - `_todoController`를 통해 업데이트된 전체 목록을 방출합니다.
        4. `toggleTodo` 메서드
            - 주어진 `id`와 일치하는 `Todo` 객체를 찾습니다.
            - 해당 `Todo`의 `isCompleted` 상태를 반전시킵니다.
            - 변경된 목록을 다시 방출합니다.
        5. `removeTodo` 메서드
            - 주어진 `id`와 일치하는 `Todo` 객체를 목록에서 제거합니다.
            - 변경된 목록을 다시 방출합니다.
        6. `dispose` 메서드
            - `StreamController`를 닫아 리소스를 정리합니다.
        7. `main` 메서드
            - `TodoService` 인스턴스를 생성합니다.
            - `todos` 스트림을 구독하여 목록이 변경될 때마다 콘솔에 출력합니다.
            - 할 일을 추가, 상태 변경, 삭제하는 작업을 수행하여 서비스의 기능을 테스트합니다.
            - 마지막으로 `dispose`를 호출하여 리소스를 정리합니다.
    - 주요 개념
        1. **클래스 (Class)**
            - `class Todo`와 `class TodoService`는 객체 지향 프로그래밍의 기본 개념입니다.
            - 생성자 사용법: `Todo(this.id, this.title, this.isCompleted);`
        2. **private 멤버**
            - `_todos`와 `_todoController`처럼 변수명 앞에 언더스코어(_)를 붙여 private 멤버를 선언합니다.
        3. **Getter 메서드**
            - `Stream<List<Todo>> get todos => _todoController.stream;`는 getter 메서드의 간단한 형태입니다.
        4. **제네릭 (Generics)**
            - `List<Todo>`, `Stream<List<Todo>>`에서 사용된 `<>`는 제네릭을 나타냅니다.
        5. **비동기 프로그래밍**
            - `StreamController`와 `Stream`은 Dart의 비동기 프로그래밍 도구입니다.
        6. **람다 함수 (Lambda Functions)**
            - `_todos.firstWhere((todo) => todo.id == id);`에서 `(todo) => todo.id == id`는 람다 함수입니다.
        7. **널 안전성 (Null Safety)**
            - Dart 2.12 이후 버전에서는 널 안전성이 기본입니다. 이 코드에서는 명시적으로 사용되지 않았지만, 중요한 개념입니다.
        8. **리스트 조작**
            - `_todos.add(todo);`, `_todos.removeWhere((todo) => todo.id == id);` 등 리스트 메서드 사용법을 보여줍니다.
        9. **문자열 보간 (String Interpolation)**
            - `'${todo.title} - ${todo.isCompleted ? "완료" : "미완료"}'`에서 `${}` 형식으로 사용됩니다.
        10. **삼항 연산자**
            - `todo.isCompleted ? "완료" : "미완료"`는 조건 ? 참일 때 값 : 거짓일 때 값 형식의 삼항 연산자입니다.
        11. **final 키워드**
            - `final todoService = TodoService();`에서 `final`은 한 번 할당되면 변경할 수 없는 변수를 선언합니다.
        12. **메서드 체이닝 (Method Chaining)**
            - `todoService.todos.listen((todos) { ... });`에서 메서드 체이닝을 볼 수 있습니다.
        13. **익명 함수 (Anonymous Functions)**
            - `listen((todos) { ... })`에서 사용된 함수는 익명 함수의 예입니다.
        14. **DateTime 클래스**
            - `DateTime.now().toString()`은 현재 시간을 문자열로 변환하는 방법을 보여줍니다.
