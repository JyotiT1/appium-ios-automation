echo "# appium-ios-automation" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/JyotiT1/appium-ios-automation.git
git push -u origin main



# iOS Automation Demo

A simple SwiftUI iOS application created specifically for learning and demonstrating **iOS UI automation**.

The project is designed to be used with:

- Swift
- SwiftUI
- Xcode
- iOS Simulator
- Appium
- XCUITest
- WebdriverIO
- TypeScript
- Allure Report

The application is intentionally small so that anyone can build it from scratch, generate a simulator `.app`, install it on an iOS Simulator, and automate the main user journeys.

## 1. Project Overview

The application contains a simple login flow followed by a task-management screen.

```text
                AutomationDemo
                      |
                      v
                   Login
                      |
              Username / Password
                      |
                      v
                    Home
                      |
                +-----+-----+
                |           |
             Add Task    Clear All
                |
                v
             Task List
```

The main purpose is **automation practice**, not production business functionality.

## 2. Technology Stack

| Area | Technology |
|---|---|
| Language | Swift |
| UI | SwiftUI |
| IDE | Xcode |
| Platform | iOS |
| Test Device | iOS Simulator |
| UI Automation | Appium |
| Automation Driver | XCUITest |
| Automation Framework | WebdriverIO |
| Automation Language | TypeScript |
| Reporting | Allure |
| Version Control | Git / GitHub |

## 3. Prerequisites

- Mac
- Xcode
- iOS Simulator runtime
- Apple ID (required when signing/deploying to a physical device; not required for basic Simulator development)
- Git

Verify:

```bash
xcodebuild -version
swift --version
git --version
xcrun simctl list runtimes
xcrun simctl list devices
```

## 4. Create the Project in Xcode

Open:

```text
File → New → Project
```

Select:

```text
iOS → App
```

Use:

```text
Product Name: AutomationDemo
Organization Identifier: com.demo
Interface: SwiftUI
Language: Swift
Storage: None
```

Recommended Bundle Identifier:

```text
com.demo.AutomationDemo
```

Make sure the **Debug** configuration also uses this Bundle ID.

Verify under:

```text
Target → AutomationDemo → Build Settings
→ Product Bundle Identifier
```

## 5. Application Structure

```text
AutomationDemo
├── AutomationDemoApp.swift
├── ContentView.swift
├── HomeView.swift
└── Assets.xcassets
```

`ContentView.swift` contains the login screen.

`HomeView.swift` contains the home screen and task functionality.

`AutomationDemoApp.swift` is the application entry point.

## 6. Application Features

### Login

The login screen contains:

- Username
- Password
- Login button

For demo purposes, the application only checks that username and password are not empty.

Example:

```text
Username: testuser
Password: password123
```

### Task Management

The Home screen contains:

- Task input
- Add Task button
- Task list
- Clear All button

## 7. Accessibility Identifiers

The application uses `accessibilityIdentifier` values specifically for automation.

| UI Element | Identifier |
|---|---|
| App title | `appTitle` |
| Username | `usernameField` |
| Password | `passwordField` |
| Login | `loginButton` |
| Home title | `homeTitle` |
| Task input | `taskInput` |
| Add Task | `addTaskButton` |
| Clear All | `clearAllButton` |

Example:

```swift
TextField("Username", text: $username)
    .textFieldStyle(.roundedBorder)
    .accessibilityIdentifier("usernameField")
```

## 8. Run the Application

Select an iOS Simulator from the Xcode Run Destination.

Example:

```text
AutomationDemo → iPhone 17
```

Press:

```text
Command + R
```

Xcode will:

```text
Compile
   ↓
Build
   ↓
Create AutomationDemo.app
   ↓
Install on Simulator
   ↓
Launch application
```

## 9. Generate the Simulator `.app`

For Appium automation, build the application for the iOS Simulator.

From Xcode:

```text
Product → Build
```

or:

```text
Command + B
```

Terminal:

```bash
xcodebuild \
-project AutomationDemo.xcodeproj \
-scheme AutomationDemo \
-sdk iphonesimulator \
-configuration Debug \
build
```

Find the generated `.app`:

```bash
find ~/Library/Developer/Xcode/DerivedData \
-path "*/Build/Products/Debug-iphonesimulator/AutomationDemo.app" \
-type d
```

The correct path should contain:

```text
Build/Products/Debug-iphonesimulator/
```

Avoid using an `.app` under:

```text
Index.noindex
```

because that may be an indexing/build artifact rather than the proper simulator product.

## 10. Verify the Bundle Identifier

After finding the correct `.app`:

```bash
plutil -p "/path/to/AutomationDemo.app/Info.plist" | grep CFBundleIdentifier
```

Expected:

```text
"CFBundleIdentifier" => "com.demo.AutomationDemo"
```

If the Bundle ID is missing, check:

```text
Xcode
→ Target
→ AutomationDemo
→ General
→ Identity
→ Bundle Identifier
```

Also verify:

```text
Build Settings
→ Product Bundle Identifier
```

for the Debug configuration.

## 11. Install the `.app` on Simulator

Check the simulator:

```bash
xcrun simctl list devices
```

Look for:

```text
iPhone 17 (...) (Booted)
```

Then:

```bash
xcrun simctl install booted "/path/to/AutomationDemo.app"
```

Launch:

```bash
xcrun simctl launch booted com.demo.AutomationDemo
```

## 12. Appium Setup

Install Node.js and verify:

```bash
node -v
npm -v
```

Install Appium:

```bash
npm install -g appium
```

Install the iOS XCUITest driver:

```bash
appium driver install xcuitest
```

Verify:

```bash
appium driver list
```

Start Appium:

```bash
appium
```

## 13. Automation Architecture

```text
WebdriverIO + TypeScript
          |
          v
       Appium
          |
          v
      XCUITest
          |
          v
   iOS Simulator
          |
          v
 AutomationDemo.app
```

## 14. Suggested Automation Test Cases

### TC01 - Valid Login

```text
Launch application
Enter username
Enter password
Click Login
Verify Home screen
```

### TC02 - Empty Login

```text
Launch application
Leave username/password empty
Click Login
Verify user remains on Login screen
```

### TC03 - Add Task

```text
Login
Enter "Learn Appium"
Click Add Task
Verify "Learn Appium"
```

### TC04 - Add Multiple Tasks

```text
Login
Add "Learn Swift"
Add "Learn Appium"
Add "Learn WebdriverIO"
Verify all tasks
```

### TC05 - Clear Tasks

```text
Login
Add a task
Click Clear All
Verify task is removed
```

## 15. Future Project Structure

```text
ios-automation-demo/
│
├── ios-app/
│   └── AutomationDemo/
│
├── automation/
│   └── webdriverio/
│       ├── test/
│       ├── pageobjects/
│       ├── config/
│       └── utils/
│
├── api/
├── database/
├── docs/
├── .gitignore
└── README.md
```

## 16. Future API and Swagger Integration

The first version does not require a backend.

A future version can use:

```text
iOS App
   |
   v
REST API
   |
   v
Node.js / Spring Boot
   |
   v
PostgreSQL
```

Swagger/OpenAPI can document and test APIs such as:

```text
POST /login
GET /tasks
POST /tasks
DELETE /tasks/{id}
```

## 17. Future AI Integration

AI can be added after the basic application and API are working.

```text
User
  |
  | "Summarize my tasks"
  v
iOS App
  |
  v
Backend
  |
  v
AI Service
  |
  v
AI Response
```

Keep AI credentials on the backend; do not expose private API keys directly in the iOS application.

## 18. Git Setup

Initialize:

```bash
git init
```

Check:

```bash
git status
```

Add:

```bash
git add .
```

Commit:

```bash
git commit -m "Initial iOS automation demo app"
```

Connect your GitHub repository:

```bash
git remote add origin <YOUR_GITHUB_REPOSITORY_URL>
```

Push:

```bash
git branch -M main
git push -u origin main
```

Recommended repository name:

```text
ios-automation-demo
```

## 19. Recommended `.gitignore`

```gitignore
# Xcode
DerivedData/
build/
*.xcuserstate
*.xcscmblueprint
xcuserdata/

# macOS
.DS_Store

# Swift Package Manager
.build/

# Node
node_modules/

# Test reports
allure-results/
allure-report/
```

Do not commit API keys, certificates, provisioning profiles, passwords, or other secrets.

## 20. Troubleshooting

### Simulator cannot be found

```bash
xcrun simctl list runtimes
xcrun simctl list devices
```

Open Simulator directly if necessary:

```bash
open /Applications/Xcode.app/Contents/Developer/Applications/Simulator.app
```

### `.app` says Missing Bundle ID

Verify:

```bash
plutil -p "/path/to/AutomationDemo.app/Info.plist" | grep CFBundleIdentifier
```

Expected:

```text
com.demo.AutomationDemo
```

Also verify the Debug Product Bundle Identifier in Xcode.

### `.app` does not install by drag-and-drop

Make sure it is a Simulator build:

```text
Debug-iphonesimulator/AutomationDemo.app
```

For reliable installation:

```bash
xcrun simctl install booted "/path/to/AutomationDemo.app"
```

### Appium cannot find elements

Verify that the corresponding `accessibilityIdentifier` exists in the SwiftUI code.

## 21. Learning Roadmap

```text
Phase 1
Xcode + Swift + SwiftUI
        ↓
Phase 2
Build AutomationDemo
        ↓
Phase 3
iOS Simulator
        ↓
Phase 4
Generate .app
        ↓
Phase 5
Appium + XCUITest
        ↓
Phase 6
WebdriverIO + TypeScript
        ↓
Phase 7
Page Object Model
        ↓
Phase 8
Allure Reporting
        ↓
Phase 9
REST API + Swagger
        ↓
Phase 10
PostgreSQL
        ↓
Phase 11
AI integration
        ↓
Phase 12
GitHub Actions CI/CD
```

## 22. Quick Start

```bash
# Verify Xcode
xcodebuild -version

# Verify iOS runtimes
xcrun simctl list runtimes

# Verify simulators
xcrun simctl list devices

# Build Simulator app
xcodebuild \
-project AutomationDemo.xcodeproj \
-scheme AutomationDemo \
-sdk iphonesimulator \
-configuration Debug \
build

# Find .app
find ~/Library/Developer/Xcode/DerivedData \
-path "*/Build/Products/Debug-iphonesimulator/AutomationDemo.app" \
-type d

# Install
xcrun simctl install booted "/path/to/AutomationDemo.app"

# Launch
xcrun simctl launch booted com.demo.AutomationDemo
```

## 23. Project Goal

The goal of this repository is to provide a beginner-friendly starting point for **iOS automation testing**.

The final learning project will demonstrate:

**iOS Development + SwiftUI + REST API + Swagger/OpenAPI + PostgreSQL + AI + Appium + XCUITest + WebdriverIO + TypeScript + Allure + GitHub Actions.**
