# Flutter Chat App

A real-time chat application built with **Flutter** and **Firebase**.

The application allows users to create accounts, sign in, exchange messages in real time, and receive push notifications when new messages arrive.

---

## 📱 Overview

Flutter Chat App is a mobile messaging application developed using Flutter and Firebase.

The application provides:

* User registration and login
* User authentication with Firebase Authentication
* Real-time messaging with Cloud Firestore
* User profiles and avatars
* Push notifications using Firebase Cloud Messaging (FCM)
* A separate Node.js backend for sending notifications

---

## ✨ Features

### 🔐 Authentication

Users can:

* Create a new account
* Sign in with email and password
* Sign out
* Maintain authentication state between screens

Authentication is handled by **Firebase Authentication**.

---

### 💬 Real-time Chat

Users can send and receive messages in real time.

Each message contains information such as:

```text
text
createdAt
userId
username
userImage
```

Messages are stored in **Cloud Firestore**.

Example:

```text
chat/
 ├── messageId
 │    ├── text
 │    ├── createdAt
 │    ├── userId
 │    ├── username
 │    └── userImage
```

---

### 🔔 Push Notifications

The application uses **Firebase Cloud Messaging (FCM)** to receive push notifications.

The FCM token of each user is stored in Firestore:

```text
users/{userId}

{
  username: "...",
  userImage: "...",
  fcmToken: "..."
}
```

When a new message is sent, the notification system can send a push notification to the recipient's device.

The project uses a separate **Node.js backend with Firebase Admin SDK** for notification delivery.

Architecture:

```text
┌───────────────────┐
│   Flutter App     │
│                   │
│ Authentication    │
│ Firestore         │
│ FCM               │
└─────────┬─────────┘
          │
          │ HTTP Request
          ▼
┌───────────────────┐
│  Node.js Backend  │
│                   │
│ Express.js        │
│ Firebase Admin    │
└─────────┬─────────┘
          │
          │ FCM
          ▼
┌───────────────────┐
│ Firebase Cloud    │
│ Messaging         │
└─────────┬─────────┘
          │
          ▼
┌───────────────────┐
│ Recipient Device  │
└───────────────────┘
```

---

## 🛠️ Technologies

| Technology               | Purpose                          |
| ------------------------ | -------------------------------- |
| Flutter                  | Mobile application framework     |
| Dart                     | Programming language             |
| Firebase Authentication  | User authentication              |
| Cloud Firestore          | Real-time database               |
| Firebase Cloud Messaging | Push notifications               |
| Node.js                  | Notification backend             |
| Express.js               | Backend REST API                 |
| Firebase Admin SDK       | Server-side Firebase integration |

---

## 📦 Dependencies

Main Flutter packages used in the project:

```yaml
dependencies:
  flutter:
    sdk: flutter

  firebase_core:
  firebase_auth:
  cloud_firestore:
  firebase_messaging:
  image_picker:
```

The exact versions can be found in:

```text
pubspec.yaml
```

---

## 📁 Project Structure

```text
flutter_chat_app/
│
├── android/
├── ios/
├── lib/
│   │
│   ├── screens/
│   │   ├── auth.dart
│   │   └── chat.dart
│   │
│   ├── widgets/
│   │   ├── auth.dart
│   │   ├── chat_messages.dart
│   │   ├── message_bubble.dart
│   │   └── new_message.dart
│   │
│   ├── firebase_options.dart
│   └── main.dart
│
├── assets/
│
├── pubspec.yaml
├── pubspec.lock
├── .gitignore
└── README.md
```

> The exact folder structure may change as the application is developed.

---

# 🔥 Firebase Configuration

This project uses Firebase as its backend services.

Firebase services currently used:

```text
Firebase
├── Authentication
├── Cloud Firestore
└── Cloud Messaging
```

---

## 🔐 Firebase Authentication

Email/Password authentication is enabled in Firebase Authentication.

The application uses:

```dart
FirebaseAuth.instance.signInWithEmailAndPassword(...)
```

for login and:

```dart
FirebaseAuth.instance.createUserWithEmailAndPassword(...)
```

for registration.

---

## 🗄️ Cloud Firestore

Firestore stores user information and chat messages.

### Users

```text
users/{userId}
```

Example:

```json
{
  "username": "John",
  "userImage": "...",
  "fcmToken": "..."
}
```

### Chat Messages

```text
chat/{messageId}
```

Example:

```json
{
  "text": "Hello!",
  "createdAt": "Timestamp",
  "userId": "...",
  "username": "John",
  "userImage": "..."
}
```

---

# 🔔 Firebase Cloud Messaging

The application obtains an FCM token from the device:

```dart
final token = await FirebaseMessaging.instance.getToken();
```

The token is stored in the user's Firestore document.

The application also subscribes to the `chat` topic:

```dart
FirebaseMessaging.instance.subscribeToTopic('chat');
```

This allows the notification system to send messages through FCM.

---

# 🧩 Authentication Flow

The authentication state is monitored using Firebase Auth:

```text
                Firebase.initializeApp()
                         │
                         ▼
                FirebaseAuth
                         │
                         ▼
                 authStateChanges()
                    /          \
                   /            \
             Logged out       Logged in
                 │                │
                 ▼                ▼
            Auth Screen       Chat Screen
```

The application automatically displays the appropriate screen depending on the user's authentication state.

---

# 💬 Messaging Flow

When a user sends a message:

```text
User enters message
        │
        ▼
NewMessage widget
        │
        ▼
Cloud Firestore
        │
        ▼
chat/{messageId}
        │
        ▼
ChatMessages
        │
        ▼
MessageBubble
```

Because Firestore provides real-time streams, new messages can appear in the chat interface without manually refreshing the application.

---

# 🖼️ User Profile

During registration, users can provide:

* Username
* Profile image
* Email
* Password

User information is stored in Firestore.

The profile image is associated with the user's Firestore document through the `userImage` field.

---

# 🚀 Getting Started

## 1. Clone the Repository

```bash
git clone https://github.com/NTQuyeen/flutter_chat_app.git
```

Navigate to the project:

```bash
cd flutter_chat_app
```

---

## 2. Install Flutter Dependencies

Run:

```bash
flutter pub get
```

---

## 3. Configure Firebase

Create a Firebase project and configure the Flutter application using FlutterFire.

Install FlutterFire CLI if necessary:

```bash
dart pub global activate flutterfire_cli
```

Then configure Firebase:

```bash
flutterfire configure
```

Select the platforms you want to support.

This generates:

```text
lib/firebase_options.dart
```

---

## 4. Enable Firebase Authentication

In Firebase Console:

```text
Authentication
    ↓
Sign-in method
    ↓
Email/Password
    ↓
Enable
```

---

## 5. Create Firestore Database

In Firebase Console:

```text
Firestore Database
    ↓
Create database
```

Configure the appropriate Firestore security rules for your application.

---

## 6. Run the Application

Check connected devices:

```bash
flutter devices
```

Then run:

```bash
flutter run
```

---

# 🧪 Development

Check Flutter installation:

```bash
flutter doctor
```

Analyze the project:

```bash
flutter analyze
```

Run tests:

```bash
flutter test
```

---

# 🔒 Security

Do not commit sensitive credentials to GitHub.

Important files and credentials should be protected, especially:

* Firebase service account private keys
* API keys with elevated privileges
* Database credentials
* Backend environment variables

The Firebase Admin SDK service account used by the notification backend should **not** be included in this repository.

---

# 🏗️ Overall Architecture

The complete system consists of three main components:

```text
                    ┌─────────────────────┐
                    │    Flutter App      │
                    │                     │
                    │ Firebase Auth       │
                    │ Firestore           │
                    │ Firebase Messaging  │
                    └──────────┬──────────┘
                               │
                               │
                    ┌──────────▼──────────┐
                    │      Firebase       │
                    │                     │
                    │ Authentication      │
                    │ Cloud Firestore     │
                    │ Cloud Messaging     │
                    └──────────┬──────────┘
                               │
                               │
                    ┌──────────▼──────────┐
                    │   Node.js Backend   │
                    │                     │
                    │ Express.js          │
                    │ Firebase Admin SDK  │
                    └─────────────────────┘
```

---

# 📌 Future Improvements

Possible future features include:

* [ ] Private conversations
* [ ] Multiple chat rooms
* [ ] Online/offline status
* [ ] Typing indicators
* [ ] Message timestamps
* [ ] Message read status
* [ ] Message deletion
* [ ] Image messages
* [ ] File sharing
* [ ] User search
* [ ] Friend system
* [ ] Improved push notification handling
* [ ] Notification history
* [ ] Backend authentication
* [ ] Production deployment

---

# 👨‍💻 Author

**NTQuyeen**

GitHub:

https://github.com/NTQuyeen

---

# 📄 License

This project was developed for learning and educational purposes.
