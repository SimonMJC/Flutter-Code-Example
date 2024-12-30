# MainDish
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
## 해석

## Song 클래스

```dart
class Song {
  String title;
  String artist;
  int duration; // 초 단위

  Song(this.title, this.artist, this.duration);

  @override
  String toString() => '$title by $artist';
}
```

### 생성자

```dart
Song(this.title, this.artist, this.duration);
```

- 간결한 생성자 문법을 사용합니다.
- `this.title`, `this.artist`, `this.duration`은 각각 클래스의 속성에 직접 매개변수 값을 할당합니다.

### toString() 메소드

```dart
@override
String toString() => '$title by $artist';
```

- `Object` 클래스의 `toString()` 메소드를 오버라이드합니다.
- 화살표 함수 문법을 사용하여 간결하게 표현합니다.
- 문자열 보간(`$title`, `$artist`)을 사용하여 노래 정보를 반환합니다.

## Playlist 클래스

```dart
class Playlist {
  String name;
  List<Song> songs = [];

  Playlist(this.name);

  // ... 메소드들 ...
}
```

### 생성자

```dart
Playlist(this.name);
```

- `name` 매개변수를 받아 클래스의 `name` 속성을 초기화합니다.

### addSong 메소드

```dart
void addSong(Song song) {
  songs.add(song);
}
```

- `Song` 객체를 매개변수로 받아 `songs` 리스트에 추가합니다.

### removeSong 메소드

```dart
void removeSong(Song song) {
  songs.remove(song);
}
```

- `Song` 객체를 매개변수로 받아 `songs` 리스트에서 제거합니다.

### totalDuration getter

```dart
int get totalDuration => songs.fold(0, (sum, song) => sum + song.duration);
```

- `fold` 메소드를 사용하여 모든 노래의 `duration`을 합산합니다.
- 초기값 0에서 시작하여 각 노래의 `duration`을 더합니다.

### shuffle 메소드

```dart
void shuffle() {
  songs.shuffle();
}
```

- `List` 클래스의 `shuffle()` 메소드를 사용하여 `songs` 리스트의 순서를 무작위로 섞습니다.

### searchByArtist 메소드

```dart
List<Song> searchByArtist(String artist) {
  return songs.where((song) => song.artist.toLowerCase().contains(artist.toLowerCase())).toList();
}
```

- `where` 메소드를 사용하여 주어진 `artist` 이름을 포함하는 노래들을 필터링합니다.
- 대소문자 구분 없이 검색하기 위해 `toLowerCase()`를 사용합니다.
- 결과를 리스트로 변환하여 반환합니다.

### displayPlaylist 메소드

```dart
void displayPlaylist() {
  print('Playlist: $name');
  for (var i = 0; i < songs.length; i++) {
    print('${i + 1}. ${songs[i]}');
  }
  print('Total duration: ${totalDuration ~/ 60} minutes ${totalDuration % 60} seconds');
}
```

- 플레이리스트 이름을 출력합니다.
- `for` 루프를 사용하여 각 노래를 번호와 함께 출력합니다.
- 총 재생 시간을 분과 초로 변환하여 출력합니다.
  - `~/` 연산자는 정수 나눗셈을 수행합니다.
  - `%` 연산자는 나머지를 계산합니다.

### main 함수
```dart
void main() {
  // ... 코드 ...
}
```

- Playlist 객체를 생성합니다.
- 여러 Song 객체를 생성하여 플레이리스트에 추가합니다.
- 플레이리스트의 내용을 출력합니다.
- 특정 아티스트("The Weeknd")의 노래를 검색하고 결과를 출력합니다.
- 플레이리스트를 섞은 후 다시 출력합니다.

# Dessert
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

## 해석

## Student 클래스

```dart
class Student {
  String name;
  List<int> scores;

  Student(this.name, this.scores);

  double get average => scores.isEmpty ? 0 : scores.reduce((a, b) => a + b) / scores.length;
}
```

### 속성
- `name`: 학생의 이름을 저장하는 String 타입 변수
- `scores`: 학생의 점수들을 저장하는 List<int> 타입 변수

### 생성자

```dart
Student(this.name, this.scores);
```

- 간결한 생성자 문법을 사용하여 `name`과 `scores`를 초기화합니다.

### average getter

```dart
double get average => scores.isEmpty ? 0 : scores.reduce((a, b) => a + b) / scores.length;
```

- 학생의 평균 점수를 계산하여 반환합니다.
- 삼항 연산자를 사용하여 `scores`가 비어있는 경우를 처리합니다.
- `reduce` 메소드를 사용하여 모든 점수의 합을 계산합니다.
- 점수의 합을 점수 개수로 나누어 평균을 구합니다.

## main 함수

```dart
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

### 학생 목록 생성

```dart
var students = [
  Student('Alice', [85, 90, 78]),
  Student('Bob', [92, 88, 95]),
  Student('Charlie', [76, 80, 85])
];
```

- `Student` 객체들을 포함하는 리스트를 생성합니다.

### 학생 정렬

```dart
students.sort((a, b) => b.average.compareTo(a.average));
```

- `sort` 메소드를 사용하여 학생들을 평균 점수 기준으로 내림차순 정렬합니다.
- 람다 함수를 사용하여 비교 로직을 정의합니다.

### 결과 출력

```dart
print('학생 성적 순위:');
for (var student in students) {
  print('${student.name}: 평균 ${student.average.toStringAsFixed(2)}');
}
```

- `for-in` 루프를 사용하여 각 학생의 이름과 평균 점수를 출력합니다.
- `toStringAsFixed(2)`를 사용하여 평균 점수를 소수점 둘째 자리까지 표시합니다.

### 최고 성적 학생 출력

```dart
var topStudent = students.first;
print('\n최고 성적 학생: ${topStudent.name}, 평균: ${topStudent.average.toStringAsFixed(2)}');
```

- 정렬된 리스트의 첫 번째 학생을 최고 성적 학생으로 선택합니다.
- 최고 성적 학생의 이름과 평균 점수를 출력합니다.
