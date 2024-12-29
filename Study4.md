# Main Dish 
```dart
import 'dart:math';

void main() {
  List<int> numbers = List.generate(20, (index) => Random().nextInt(100));
  print('원본 리스트: $numbers');

  // 짝수만 필터링
  List<int> evenNumbers = numbers.where((num) => num % 2 == 0).toList();
  print('짝수 리스트: $evenNumbers');

  // 모든 요소에 10을 더하기
  List<int> addedNumbers = numbers.map((num) => num + 10).toList();
  print('10을 더한 리스트: $addedNumbers');

  // 리스트 정렬
  numbers.sort();
  print('정렬된 리스트: $numbers');

  // 리스트의 첫 5개 요소
  List<int> firstFive = numbers.take(5).toList();
  print('처음 5개 요소: $firstFive');

  // 리스트의 합계
  int sum = numbers.reduce((value, element) => value + element);
  print('합계: $sum');

  // 리스트에서 가장 큰 수
  int max = numbers.reduce((curr, next) => curr > next ? curr : next);
  print('최대값: $max');

  // 리스트 뒤집기
  List<int> reversedList = numbers.reversed.toList();
  print('뒤집힌 리스트: $reversedList');

  // 중복 제거
  List<int> uniqueNumbers = numbers.toSet().toList();
  print('중복 제거된 리스트: $uniqueNumbers');

  // 특정 값으로 리스트 채우기
  List<String> filledList = List.filled(5, '다트');
  print('채워진 리스트: $filledList');
}
```

## 해석

1. 0부터 99 사이의 랜덤한 정수 20개로 리스트를 생성합니다.
2. 생성된 리스트에서 짝수만 필터링합니다.
3. 원본 리스트의 모든 요소에 10을 더한 새 리스트를 만듭니다.
4. 원본 리스트를 정렬합니다.
5. 정렬된 리스트에서 첫 5개 요소를 추출합니다.
6. 리스트의 모든 요소의 합을 계산합니다.
7. 리스트에서 가장 큰 수를 찾습니다.
8. 리스트를 뒤집습니다.
9. 리스트에서 중복을 제거합니다.
10. 특정 값으로 새 리스트를 생성합니다.

## 문법 설명

### List 생성

- `List.generate()`: 지정된 길이만큼 리스트를 생성하고, 각 요소를 생성 함수로 초기화합니다.

```dart
List<int> numbers = List.generate(20, (index) => Random().nextInt(100));
```

### List 메서드

- `where()`: 조건에 맞는 요소만 필터링합니다. `toList()`와 함께 사용하여 결과를 리스트로 변환합니다.

```dart
List<int> evenNumbers = numbers.where((num) => num % 2 == 0).toList();
```

- `map()`: 리스트의 각 요소를 변환합니다.

```dart
List<int> addedNumbers = numbers.map((num) => num + 10).toList();
```

- `sort()`: 리스트를 정렬합니다.

```dart
numbers.sort();
```

- `take()`: 리스트에서 지정된 개수만큼의 요소를 가져옵니다.

```dart
List<int> firstFive = numbers.take(5).toList();
```

- `reduce()`: 리스트의 요소들을 줄여나가며 단일 값을 생성합니다.

```dart
int sum = numbers.reduce((value, element) => value + element);
```

- `reversed`: 리스트를 뒤집습니다.

```dart
List<int> reversedList = numbers.reversed.toList();
```

- `toSet()`: 리스트를 Set으로 변환하여 중복을 제거합니다.

```dart
List<int> uniqueNumbers = numbers.toSet().toList();
```

- `List.filled()`: 지정된 길이만큼 동일한 값으로 채워진 리스트를 생성합니다.

```dart
List<String> filledList = List.filled(5, '다트');
```

이 코드는 Dart의 List 컬렉션을 다루는 다양한 방법을 보여주며, 학생들이 이를 통해 List의 주요 메서드와 속성을 이해하고 활용할 수 있을 것입니다.

  
# Dessert
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

  ## 해석
## WeatherCondition 클래스

### 전역 변수 선언
- `String description`: 날씨 설명
- `double temperature`: 온도
- `int humidity`: 습도

### 생성자
```dart
WeatherCondition(this.description, this.temperature, this.humidity);
```
- 간단한 생성자 문법을 사용하여 객체 생성 시 속성을 초기화합니다.

### 메서드
```dart
void display()
```
- 날씨 정보를 출력합니다.
- 문자열 보간(`$` 및 `${}`)을 사용하여 속성 값을 출력합니다.
- `toStringAsFixed(1)`를 사용하여 온도를 소수점 첫째 자리까지 표시합니다.

## WeatherForecast 클래스

### 속성
```dart
List<WeatherCondition> forecast = [];
```
- `WeatherCondition` 객체들을 저장하는 리스트입니다.

### 메서드

#### addForecast
```dart
void addForecast(WeatherCondition condition)
```
- 새로운 `WeatherCondition` 객체를 `forecast` 리스트에 추가합니다.
- `List.add()` 메서드를 사용합니다.

#### displayForecast
```dart
void displayForecast()
```
- `forecast` 리스트의 모든 날씨 예보를 출력합니다.
- `isEmpty` 속성을 사용하여 리스트가 비어있는지 확인합니다.
- `for` 루프를 사용하여 리스트의 각 요소에 접근합니다.

#### findHottestDay
```dart
WeatherCondition? findHottestDay()
```
- 가장 높은 온도를 가진 날을 찾습니다.
- 널 안전성(Null safety)을 위해 반환 타입에 `?`를 사용합니다.
- `reduce()` 메서드를 사용하여 최대값을 찾습니다.

#### getAverageTemperature
```dart
double getAverageTemperature()
```
- 평균 온도를 계산합니다.
- `for-in` 루프를 사용하여 모든 온도의 합을 계산합니다.

## main 함수

- `WeatherForecast` 객체를 생성합니다.
- `addForecast()` 메서드를 사용하여 날씨 예보를 추가합니다.
- `displayForecast()`, `findHottestDay()`, `getAverageTemperature()` 메서드를 호출하여 결과를 출력합니다.

## 관련 Dart 문법

1. **클래스 정의**: `class` 키워드를 사용합니다.

2. **생성자**: 클래스 이름과 동일한 메서드로 정의합니다.

3. **리스트**: `List<T>` 형태로 선언하며, `[]`로 초기화합니다.
  - 요소 추가: forecast.add(condition);
  - 인덱스로 접근: forecast[i]
  - 길이: forecast.length
  - 비어있는지 확인: forecast.isEmpty

4. **널 안전성**: `?`를 사용하여 널이 될 수 있는 타입을 표시합니다.

5. **조건문**: `if-else` 구문을 사용합니다.

6. **반복문**: 
   - `for` 루프: `for (초기화; 조건; 증감)`
   - `for-in` 루프: `for (var item in collection)`

7. **람다 표현식**: `(매개변수) => 표현식` 형태로 사용합니다.

8. **메서드 체이닝**: `object.method1().method2()` 형태로 연속적으로 메서드를 호출합니다.

9. **문자열 보간**: `$변수명` 또는 `${표현식}`을 사용합니다.


