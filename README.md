# Flutter CI/CD with Fastlane and GitHub Actions

This repository demonstrates the integration of **Fastlane** for Firebase App Distribution and a **GitHub Actions** CI/CD pipeline to automate the process of building, testing, and deploying a **Flutter app** for **Android** and **iOS** platforms.

## Features
- **CI/CD Pipeline**: Automates the build, test, and deploy processes for both Android and iOS platforms using **GitHub Actions**.
- **Fastlane Integration**: Uses **Fastlane** to automate the deployment of APKs to **Firebase App Distribution**.
- **Cross-platform Support**: Supports both **Android** (via Gradle) and **iOS** (via Xcode) builds.

## Workflow Overview
The CI/CD pipeline is triggered on:
- **Push** to the `main` branch
- **Pull Requests** targeting the `main` branch

### Jobs:
1. **Android Build**:
   - Checkout code from GitHub
   - Set up Java 17
   - Set up Flutter
   - Install dependencies using `flutter pub get`
   - Run unit tests using `flutter test`
   - Build the APK using `flutter build apk --release`
   - Upload the APK as an artifact for later download

2. **iOS Build** (runs on `macos-latest`):
   - Checkout code from GitHub
   - Set up Flutter
   - Install dependencies using `flutter pub get` and `cocoapods`
   - Build the iOS app using `flutter build ios --release --no-codesign`
   - List files in the iOS build directory
   - Upload the IPA file as an artifact for later download

### Firebase App Distribution:
Once the Android APK is built, **Fastlane** is used to upload it to **Firebase App Distribution** for testing.

## Files & Directories
- **`ci.yml`**: GitHub Actions workflow file for Android and iOS builds.
- **`Fastfile`**: Fastlane configuration file for automating the upload of APKs to Firebase App Distribution.

## Setup

### Requirements:
- **Flutter**: Ensure you have Flutter installed on your local machine for testing.
- **Firebase**: Set up a Firebase project and generate your Firebase app ID for the Android app.
- **Fastlane**: Install Fastlane for automating the upload process.

### Firebase Setup:
1. Follow [Firebase's documentation](https://firebase.google.com/docs/app-distribution) to create a Firebase project and app.
2. Generate your Firebase app ID and configure Fastlane to use it.

### GitHub Actions Setup:
1. Fork this repository or clone it to your GitHub account.
2. Ensure your repository contains a valid Flutter project and `Fastfile` configured for Firebase.
3. Set up Firebase credentials (if needed) as GitHub secrets to allow Fastlane to interact with Firebase.

## Running Locally
To test locally, run the following Flutter commands:
- **Android**:
  ```bash
  flutter build apk --release
