# 🤖 Android CI/CD Pipeline

![Platform](https://img.shields.io/badge/Platform-Android-3DDC84?style=flat-square&logo=android&logoColor=white)
![Language](https://img.shields.io/badge/Language-Kotlin-7F52FF?style=flat-square&logo=kotlin&logoColor=white)
![CI/CD](https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white)
![Build](https://img.shields.io/badge/Build-Gradle-02303A?style=flat-square&logo=gradle&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)

A fully automated CI/CD pipeline for Android applications using **GitHub Actions**, capable of building both **Debug** and **Release** APKs on every push and pull request — with zero manual intervention.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Pipeline Architecture](#pipeline-architecture)
- [Workflow Triggers](#workflow-triggers)
- [Build Variants](#build-variants)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [GitHub Secrets Configuration](#github-secrets-configuration)
- [Artifacts & Output](#artifacts--output)
- [Tech Stack](#tech-stack)
- [Contributing](#contributing)

---

## Overview

This repository demonstrates a production-ready CI/CD setup for Android development. The pipeline automates the entire build process — from code compilation to APK generation — ensuring that every code change is validated and packaged without manual effort.

Key benefits:
- ✅ Automated builds on every `push` and `pull_request`
- ✅ Separate **Debug** and **Release** build variants
- ✅ APK artifacts uploaded and accessible directly from GitHub Actions
- ✅ Consistent build environment using Ubuntu runners
- ✅ Secure signing configuration via GitHub Secrets

---

## Pipeline Architecture

```
Developer Push / PR
        │
        ▼
┌───────────────────┐
│   GitHub Actions   │
│  (ubuntu-latest)  │
└────────┬──────────┘
         │
    ┌────┴────┐
    │         │
    ▼         ▼
 Debug      Release
 Build       Build
    │         │
    ▼         ▼
 Debug APK  Signed
 Uploaded   Release APK
            Uploaded
```

---

## Workflow Triggers

The pipeline is triggered automatically on:

| Event          | Branch        | Action          |
|----------------|---------------|-----------------|
| `push`         | `main`        | Full build      |
| `pull_request` | `main`        | Full build      |

---

## Build Variants

### 🐛 Debug Build
- Built with `./gradlew assembleDebug`
- No signing required
- Ideal for development and testing
- APK uploaded as a GitHub Actions artifact

### 🚀 Release Build
- Built with `./gradlew assembleRelease`
- Signed using a keystore stored in GitHub Secrets
- Optimized and minified for production distribution
- APK uploaded as a GitHub Actions artifact

---

## Project Structure

```
CI_CD/
├── .github/
│   └── workflows/
│       └── android.yml        # GitHub Actions workflow definition
├── app/
│   ├── src/
│   │   ├── main/              # Main application source
│   │   ├── debug/             # Debug-specific configs
│   │   └── release/           # Release-specific configs
│   └── build.gradle.kts       # App-level Gradle config
├── gradle/
│   └── wrapper/
│       └── gradle-wrapper.properties
├── build.gradle.kts           # Project-level Gradle config
├── settings.gradle.kts        # Module settings
├── gradle.properties          # Gradle properties
├── gradlew                    # Gradle wrapper (Unix)
└── gradlew.bat                # Gradle wrapper (Windows)
```

---

## Getting Started

### Prerequisites

- Android Studio (latest stable)
- JDK 17+
- Git

### Clone the Repository

```bash
git clone https://github.com/Asghar-ali-code/CI_CD.git
cd CI_CD
```

### Run Locally

**Debug build:**
```bash
./gradlew assembleDebug
```

**Release build:**
```bash
./gradlew assembleRelease
```

Output APKs are located at:
```
app/build/outputs/apk/debug/app-debug.apk
app/build/outputs/apk/release/app-release.apk
```

---

## GitHub Secrets Configuration

For the **Release** build to sign the APK correctly, configure the following secrets in your GitHub repository under **Settings → Secrets and variables → Actions**:

| Secret Name             | Description                                      |
|-------------------------|--------------------------------------------------|
| `KEYSTORE_FILE`         | Base64-encoded `.jks` / `.keystore` file         |
| `KEY_ALIAS`             | Alias of the signing key                         |
| `KEY_PASSWORD`          | Password for the key                             |
| `STORE_PASSWORD`        | Password for the keystore                        |

To encode your keystore to Base64:
```bash
base64 -i your-keystore.jks | tr -d '\n'
```

---

## Artifacts & Output

After each successful workflow run, the built APKs are available as downloadable artifacts in the **Actions** tab of your GitHub repository.

1. Go to the **Actions** tab
2. Select a completed workflow run
3. Scroll to the **Artifacts** section at the bottom
4. Download `debug-apk` or `release-apk`

Artifacts are retained for **30 days** by default.

---

## Tech Stack

| Tool               | Purpose                         |
|--------------------|---------------------------------|
| **Kotlin**         | Primary programming language    |
| **Android SDK**    | Android application framework   |
| **Gradle (KTS)**   | Build system (Kotlin DSL)       |
| **GitHub Actions** | CI/CD automation platform       |
| **Ubuntu Runner**  | Build environment               |

---

## Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a new branch: `git checkout -b feature/your-feature-name.`
3. Make your changes and commit: `git commit -m "Add: your message"`
4. Push to your branch: `git push origin feature/your-feature-name.`
5. Open a Pull Request

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

<p align="center">
  Made with ❤️ by <a href="https://github.com/Asghar-ali-code">Asghar Ali</a>
</p>
