# WidgetPager

This repository contains an Android app that provides a home-screen placeholder widget. Tapping it opens a full-screen Activity that hosts up to 6 third-party widgets in a swipeable ViewPager.

This README lists the exact steps to create the GitHub repo, push the files, and build a debug APK with GitHub Actions.

Steps to publish and build (copy-paste)

1) Create a new public repository on GitHub, name it `widgetpager`.

2) Clone the empty repo locally:
   git clone https://github.com/YOUR_GITHUB_USERNAME/widgetpager.git
   cd widgetpager

3) Copy the project files into the repo directory exactly as shown in this chat (preserve paths). Then commit:
   git add .
   git commit -m "Initial commit: WidgetPager project + CI"

4) Generate Gradle wrapper (recommended) locally so CI uses deterministic Gradle:
   - If you already have gradle installed locally:
     gradle wrapper --gradle-version 8.3
   - If you don't have gradle installed, you can skip this step — the workflow will try to use system gradle. Generating the wrapper is recommended.

   After generating wrapper, add wrapper files:
   git add gradlew gradlew.bat gradle/wrapper/gradle-wrapper.jar gradle/wrapper/gradle-wrapper.properties
   git commit -m "Add Gradle wrapper"

5) Push to GitHub:
   git push origin main

6) On GitHub go to Actions → select "Build APK" workflow run. Wait for it to finish.

7) When the run finishes open the run and download the artifact named `widgetpager-apk` → `app-debug.apk`.

8) Transfer the APK to your Android device and install (allow installs from unknown sources if needed).

If you want me to review the workflow run logs or fix build errors, paste the run URL or the logs here and I’ll help.

Notes
- The first time you add a third-party widget from the app it will trigger the system "bind widget" flow where you will need to give permission for the widget to be bound to this app's AppWidgetHost.
- This approach uses a home-screen placeholder widget that opens the Activity; embedding multiple external AppWidgetHostViews directly into a single RemoteViews shown on the home screen is not possible with the platform constraints, so the placeholder + Activity approach is the reliable cross-device solution.