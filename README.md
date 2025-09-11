## ResQ‑GPT (Android)

An Android app built with Kotlin and Jetpack Compose that provides an on‑device rescue assistant with chat, emergency messaging, and mapping. The project contains a Compose UI app module (`app`) and a native addon module (`llama`) for local LLM inference via NDK/CMake.

### Features

- **Chat assistant**: Conversational UI with bot/human message bubbles
- **Emergency contacts**: Add, list, and message predefined contacts
- **Quick SOS**: Send templated SMS to contacts (requires SMS permission)
- **Offline/local model support**: `llama` module integrates native code for local inference
- **Map preview**: Simple web‑based map view embedded via `WebView` (`assets/map.html`)
- **Settings & about** screens

### Project structure

- **`app/`**: Main Android app (Compose UI, screens, preferences, receivers)
  - `src/main/java/com/nervesparks/resqgpt/`
    - `MainActivity.kt`, `ResQGptApp.kt`, `MainViewModel.kt`
    - UI screens in `ui/` and `ui/components/`
    - Data helpers in `data/` (e.g., SMS sender, preferences)
    - `receiver/NetworkChangeReceiver.kt`
  - `src/main/assets/map.html`
  - `src/main/res/…` app resources
- **`llama/`**: Native addon
  - `src/main/cpp/` with `CMakeLists.txt` and `llama-android.cpp`
  - Kotlin JNI bridge in `java/android/llama/cpp/LLamaAndroid.kt`

### Requirements

- Android Studio Jellyfish or newer
- JDK 17 (Android Studio bundles a compatible JDK by default)
- Android Gradle Plugin per `build.gradle.kts`
- For native module (`llama`): Android NDK and CMake installed via SDK Manager

### Getting started

1. Open the project root (`ResQ-GPT/`) in Android Studio.
2. Let Gradle sync finish. If prompted, install NDK/CMake for the `llama` module.
3. Select a device or emulator with Android 8.0+.
4. Run the `app` configuration.

### Build from command line (Windows PowerShell)

```powershell
./gradlew clean assembleDebug
```

APK outputs will be under `app/build/outputs/apk/`.

### Permissions

The app may request:

- **SMS**: send emergency messages (`SEND_SMS`)
- **Phone state**: to validate capabilities on some devices (optional)
- **Location**: to include location info in messages or map (if implemented)
- **Internet**: for network connectivity and map content

Grant permissions when prompted. If you deny SMS/location, related features will be limited.

### Configuring emergency contacts

1. Open the Emergency Contacts screen.
2. Add one or more contacts with names and phone numbers.
3. Use the SOS or messaging actions to send messages.

### Local model integration (`llama`)

- Ensure NDK and CMake are installed (SDK Manager → SDK Tools → check both).
- Gradle will invoke CMake to build native libs for supported ABIs.
- The bridge class is `android.llama.cpp.LLamaAndroid`.
- If you plan to bundle or download model files, store them appropriately and load via the JNI bridge (see `llama-android.cpp`).

### Troubleshooting

- If Gradle sync fails with NDK/CMake errors, open SDK Manager and install the required versions, then re‑sync.
- On Windows, if `./gradlew` is blocked, run `Set-ExecutionPolicy -Scope Process RemoteSigned` in the current PowerShell session or use `gradlew.bat`.
- If maps do not render, confirm `assets/map.html` loads in the embedded `WebView` and the app has Internet permission.
- For SMS failures, verify the default SMS app setting and that the device/SIM supports SMS.

### Screenshots

The images below illustrate key UI areas:

![1](https://github.com/user-attachments/assets/cfcd26ab-a6ea-4496-86be-ef1f4502c6d0)
![2](https://github.com/user-attachments/assets/12221253-e277-4746-83f1-50e6c70a79b2)
![3](https://github.com/user-attachments/assets/ea7cc0fe-0c0a-402d-b2c1-8df2319bce4f)

### License

This codebase is provided as‑is. If you intend to publish or distribute, ensure that all third‑party assets, models, and dependencies comply with their respective licenses.

![1](https://github.com/user-attachments/assets/cfcd26ab-a6ea-4496-86be-ef1f4502c6d0)
![2](https://github.com/user-attachments/assets/12221253-e277-4746-83f1-50e6c70a79b2)
![3](https://github.com/user-attachments/assets/ea7cc0fe-0c0a-402d-b2c1-8df2319bce4f)
