# MainDish - 비동기 리스트 변환 및 필터링
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


# Dessert - 비동기 리스트 정렬
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
