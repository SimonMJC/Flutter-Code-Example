# MainDish - 비동기적으로 숫자 리스트 처리하기
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

# Dessert - 비동기 필터링 및 매핑
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
