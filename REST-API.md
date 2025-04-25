### **1. Setup**
Add the `http` package to your `pubspec.yaml`:
```yaml
dependencies:
  http: ^0.13.5
```
Run `flutter pub get`.

---

### **2. GET Request (Fetch Data)**
```dart
import 'package:http/http.dart' as http;
import 'dart:convert';

Future<void> fetchData() async {
  final url = Uri.parse('https://jsonplaceholder.typicode.com/posts/1');
  final response = await http.get(url);

  if (response.statusCode == 200) {
    final data = jsonDecode(response.body);
    print('Fetched data: $data');
  } else {
    throw Exception('Failed to load data (Status: ${response.statusCode})');
  }
}
```

---

### **3. POST Request (Send Data)**
```dart
Future<void> createPost() async {
  final url = Uri.parse('https://jsonplaceholder.typicode.com/posts');
  final headers = {'Content-Type': 'application/json'};
  final body = jsonEncode({
    'title': 'New Post',
    'body': 'This is a test post.',
    'userId': 1,
  });

  final response = await http.post(url, headers: headers, body: body);

  if (response.statusCode == 201) {
    print('Post created: ${response.body}');
  } else {
    throw Exception('Failed to create post (Status: ${response.statusCode})');
  }
}
```

---

### **4. PUT Request (Update Data)**
```dart
Future<void> updatePost() async {
  final url = Uri.parse('https://jsonplaceholder.typicode.com/posts/1');
  final headers = {'Content-Type': 'application/json'};
  final body = jsonEncode({
    'title': 'Updated Post',
    'body': 'This post has been updated.',
    'userId': 1,
  });

  final response = await http.put(url, headers: headers, body: body);

  if (response.statusCode == 200) {
    print('Updated post: ${response.body}');
  } else {
    throw Exception('Failed to update post (Status: ${response.statusCode})');
  }
}
```

---

### **5. DELETE Request (Remove Data)**
```dart
Future<void> deletePost() async {
  final url = Uri.parse('https://jsonplaceholder.typicode.com/posts/1');
  final response = await http.delete(url);

  if (response.statusCode == 200) {
    print('Post deleted successfully');
  } else {
    throw Exception('Failed to delete post (Status: ${response.statusCode})');
  }
}
```

---

### **6. Handling Authentication (Bearer Token)**
```dart
Future<void> fetchProtectedData() async {
  final url = Uri.parse('https://api.example.com/protected');
  final token = 'YOUR_ACCESS_TOKEN';
  final headers = {'Authorization': 'Bearer $token'};

  final response = await http.get(url, headers: headers);

  if (response.statusCode == 200) {
    print('Protected data: ${response.body}');
  } else {
    throw Exception('Access denied (Status: ${response.statusCode})');
  }
}
```

---

### **Key Notes:**
1. **Error Handling**: Always check `response.statusCode` (e.g., `200` for success, `201` for created).
2. **Headers**: Use `'Content-Type': 'application/json'` for JSON data.
3. **Encoding/Decoding**: Use `jsonEncode()` to send data and `jsonDecode()` to parse responses.
4. **Async/Await**: API calls are asynchronous—use `async/await` or `.then()`.

---

### **Example Usage in a Flutter Widget**
```dart
ElevatedButton(
  onPressed: () async {
    try {
      await fetchData(); // Replace with any method above
    } catch (e) {
      print('Error: $e');
    }
  },
  child: Text('Fetch Data'),
)
```

---
