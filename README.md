# Flutter Chat App

A real-time chat application built with **Flutter** and **Firebase**.
The app allows users to create accounts, sign in, exchange messages in real time, and receive push notifications.

## ✨ Features

* 🔐 **Authentication** — Register and sign in with email and password.
* 💬 **Real-time Chat** — Send and receive messages using Cloud Firestore.
* 👤 **User Profiles** — Store usernames and profile images.
* 🔔 **Push Notifications** — Receive notifications through Firebase Cloud Messaging (FCM).
* 🚪 **Logout** — Securely sign out of the application.
* 📱 **Responsive UI** — Designed for Android mobile devices.

## 🛠️ Technologies

| Technology               | Purpose                      |
| ------------------------ | ---------------------------- |
| Flutter                  | Mobile application framework |
| Dart                     | Programming language         |
| Firebase Authentication  | User authentication          |
| Cloud Firestore          | Real-time chat database      |
| Firebase Cloud Messaging | Push notifications           |
| Node.js & Express        | Notification backend         |
| Firebase Admin SDK       | Server-side FCM integration  |

## 🏗️ Architecture

```text id="7vgcv9"
┌─────────────────────┐
│     Flutter App     │
│                     │
│  Firebase Auth      │
│  Cloud Firestore    │
│  Firebase Messaging │
└──────────┬──────────┘
           │
           │ HTTP
           ▼
┌─────────────────────┐
│   Node.js Backend   │
│                     │
│   Express.js        │
│   Firebase Admin    │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│         FCM         │
└──────────┬──────────┘
           │
           ▼
      User Device
```

## 📁 Project Structure

```text id="md3pii"
lib/
├── main.dart
├── screens/
│   ├── auth.dart
│   └── chat.dart
├── widgets/
│   ├── chat_messages.dart
│   ├── message_bubble.dart
│   └── new_message.dart
└── firebase_options.dart
```

## 🔥 Firebase

The application uses the following Firebase services:

* **Firebase Authentication** — User accounts and authentication.
* **Cloud Firestore** — Users and real-time chat messages.
* **Firebase Cloud Messaging** — Push notifications.

### Firestore Structure

```text id="khw73p"
users/{userId}
├── username
├── userImage
└── fcmToken

chat/{messageId}
├── text
├── createdAt
├── userId
├── username
└── userImage
```

## 🚀 Getting Started

### Prerequisites

Make sure you have installed:

* Flutter SDK
* Dart SDK
* Android Studio or another Flutter-compatible IDE
* A Firebase project

### Installation

Clone the repository:

```bash id="o6zngt"
git clone https://github.com/NTQuyeen/flutter_chat_app.git
cd flutter_chat_app
```

Install dependencies:

```bash id="zntp7j"
flutter pub get
```

Configure Firebase:

```bash id="q4yqv1"
flutterfire configure
```

Enable the following Firebase services:

```text id="69vkul"
Authentication → Email/Password
Cloud Firestore
Cloud Messaging
```

Run the application:

```bash id="dn69s6"
flutter run
```

## 🔔 Notification Backend

Push notifications are handled through a separate **Node.js backend** using Firebase Admin SDK.

**Backend Repository:**
https://github.com/NTQuyeen/chat_backend

The overall system consists of:

```text
Flutter Chat App
       │
       ▼
Firebase / Firestore
       │
       ▼
Node.js Backend
       │
       ▼
Firebase Cloud Messaging
       │
       ▼
User Device
```

## 🔒 Security

Do not commit sensitive Firebase credentials or service account files to GitHub.

Make sure files containing private keys or secrets are included in `.gitignore`.

## 👨‍💻 Author

**NTQuyeen**

Flutter Chat App developed for learning and educational purposes.
