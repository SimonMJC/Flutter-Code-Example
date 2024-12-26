# Main Dish

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


## 클래스 구조

### MenuItem 클래스
```dart
class MenuItem {
  String name;
  double price;

  MenuItem(this.name, this.price);
}
```
- 메뉴 항목을 나타내는 클래스입니다.
- `name`(음식 이름)과 `price`(가격) 두 가지 속성을 가집니다.

### Order 클래스
```dart
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
    // 주문 내역 표시 로직
  }
}
```
- 주문을 관리하는 클래스입니다.
- `addItem()`: 주문에 항목을 추가합니다.
- `getTotalPrice()`: 총 주문 금액을 계산합니다.
- `displayOrder()`: 주문 내역을 표시합니다.

### Restaurant 클래스
```dart
class Restaurant {
  List<MenuItem> menu = [
    MenuItem("햄버거", 5.99),
    MenuItem("피자", 8.99),
    MenuItem("샐러드", 4.99),
    MenuItem("음료", 1.99)
  ];

  void displayMenu() {
    // 메뉴 표시 로직
  }
}
```
- 레스토랑의 메뉴를 관리하는 클래스입니다.
- 미리 정의된 메뉴 항목들을 포함합니다.
- `displayMenu()`: 메뉴를 표시합니다.

## 메인 로직

```dart
void main() {
  var restaurant = Restaurant();
  var order = Order();

  while (true) {
    // 메인 메뉴 표시 및 사용자 입력 처리
  }
}
```

메인 함수에서는 무한 루프를 통해 사용자 인터페이스를 제공합니다:

1. 메뉴 보기
2. 주문하기
3. 주문 확인
4. 종료

사용자의 선택에 따라 `switch` 문을 사용하여 적절한 동작을 수행합니다.

## 주요 기능

- **메뉴 표시**: `restaurant.displayMenu()` 메서드를 호출하여 메뉴를 보여줍니다.
- **주문 추가**: 사용자가 선택한 메뉴 항목을 `order.addItem()` 메서드를 통해 주문에 추가합니다.
- **주문 확인**: `order.displayOrder()` 메서드를 호출하여 현재 주문 내역과 총 금액을 표시합니다.
- **프로그램 종료**: 사용자가 '4'를 선택하면 프로그램이 종료됩니다.

# Dessert

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

## 클래스 구조

### Item 클래스
```dart
class Item {
  String name;
  double price;

  Item(this.name, this.price);
}
```
- 쇼핑 아이템을 나타내는 클래스입니다.
- `name`(상품명)과 `price`(가격) 두 가지 속성을 가집니다.

## 메인 함수

```dart
void main() {
  // 메인 로직
}
```

메인 함수에서는 다음과 같은 작업을 수행합니다:

1. 쇼핑 카트 생성
2. 총 가격 계산
3. 장바구니 내역 출력
4. 가장 비싼 물품 찾기

## 주요 기능

### 쇼핑 카트 생성
```dart
var shoppingCart = [
  Item('Apple', 0.5),
  Item('Banana', 0.3),
  Item('Orange', 0.6),
  Item('Milk', 2.5)
];
```
- `Item` 객체들로 구성된 리스트를 생성하여 쇼핑 카트를 표현합니다.

### 총 가격 계산
```dart
var totalPrice = shoppingCart.fold(0.0, (sum, item) => sum + item.price);
```
- `fold` 메서드를 사용하여 모든 아이템의 가격을 합산합니다.

### 장바구니 내역 출력
```dart
print('장바구니 내역:');
for (var item in shoppingCart) {
  print('${item.name}: \$${item.price}');
}
```
- 반복문을 사용하여 각 아이템의 이름과 가격을 출력합니다.

### 총 가격 출력
```dart
print('\n총 가격: \$${totalPrice.toStringAsFixed(2)}');
```
- 계산된 총 가격을 소수점 둘째 자리까지 출력합니다.

### 가장 비싼 물품 찾기
```dart
var mostExpensiveItem = shoppingCart.reduce((a, b) => a.price > b.price ? a : b);
print('가장 비싼 물품: ${mostExpensiveItem.name} (\$${mostExpensiveItem.price})');
```
- `reduce` 메서드를 사용하여 가장 높은 가격의 아이템을 찾습니다.
- 찾은 아이템의 이름과 가격을 출력합니다.

이 프로그램은 간단한 쇼핑 카트 시스템을 구현하여, 아이템 목록을 생성하고, 총 가격을 계산하며, 가장 비싼 물품을 찾는 기능을 제공합니다. Dart의 리스트 조작 메서드들(`fold`, `reduce`)을 효과적으로 활용하고 있습니다.
