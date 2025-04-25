# Firebase Realtime Database Code Snippets for Flutter

Here are essential code snippets for working with Firebase Realtime Database in Flutter:

## 1. Setup and Initialization

First, add dependencies to `pubspec.yaml`:
```yaml
dependencies:
  firebase_core: ^2.24.0
  firebase_database: ^10.4.0
```

Initialize Firebase in your main.dart:
```dart
import 'package:firebase_core/firebase_core.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  runApp(MyApp());
}
```

## 2. Basic Write Operations

### Writing data:
```dart
import 'package:firebase_database/firebase_database.dart';

final databaseRef = FirebaseDatabase.instance.ref();

// Set data at a specific path
void writeData() {
  databaseRef.child('users/user1').set({
    'name': 'John Doe',
    'email': 'john@example.com',
    'age': 30
  });
}

// Push data to generate unique ID
void pushData() {
  databaseRef.child('posts').push().set({
    'title': 'New Post',
    'content': 'This is a new post',
    'timestamp': ServerValue.timestamp
  });
}
```

## 3. Basic Read Operations

### Reading data once:
```dart
void readDataOnce() async {
  DataSnapshot snapshot = await databaseRef.child('users/user1').get();
  if (snapshot.exists) {
    print(snapshot.value);
  } else {
    print('No data available');
  }
}
```

### Listening for realtime updates:
```dart
void listenForUpdates() {
  databaseRef.child('posts').onValue.listen((event) {
    DataSnapshot snapshot = event.snapshot;
    if (snapshot.exists) {
      print('Posts updated: ${snapshot.value}');
    }
  });
}
```

## 4. Update and Delete Operations

### Updating specific fields:
```dart
void updateData() {
  databaseRef.child('users/user1').update({
    'age': 31,
    'last_updated': ServerValue.timestamp
  });
}
```

### Deleting data:
```dart
void deleteData() {
  databaseRef.child('users/user1').remove();
}
```
