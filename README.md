cd NetworkMonitorAndroid
git init
git add .
git commit -m "Initial commit network monitor app"
git branch -M main
git remote add origin https://github.com/NetworkMonitorAndroid/NetworkMonitorAndroid.git
git push -u origin main
.github/workflows/android-build.yml
name: Build Android APK

on:
  push:
    branches: [ main ]
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Set up JDK
        uses: actions/setup-java@v4
        with:
          distribution: 'temurin'
          java-version: '17'

      - name: Grant execute permission
        run: chmod +x gradlew

      - name: Build Debug APK
        run: ./gradlew assembleDebug

      - name: Upload APK
        uses: actions/upload-artifact@v4
        with:
          name: NetworkMonitor-debug-apk
          path: app/build/outputs/apk/debug/*.apk
git add .github/workflows/android-build.yml
git commit -m "Add GitHub Actions APK build"
git push
