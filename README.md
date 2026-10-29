# 🗺️ TouristGuide MAD — Mumbai Travel & Exploration Android App

[![Android](https://img.shields.io/badge/Platform-Android-3DDC84?logo=android&logoColor=white)](https://developer.android.com/)
[![Java](https://img.shields.io/badge/Language-Java%2017-ED8B00?logo=openjdk&logoColor=white)](https://www.java.com/)
[![Material 3](https://img.shields.io/badge/UI-Material%20Design%203-757575?logo=materialdesign&logoColor=white)](https://m3.material.io/)
[![Google Maps](https://img.shields.io/badge/Maps-Google%20Maps%20SDK-4285F4?logo=googlemaps&logoColor=white)](https://developers.google.com/maps/documentation/android-sdk)
[![Gemini](https://img.shields.io/badge/AI-Google%20Gemini-8E75C2?logo=googlegemini&logoColor=white)](https://ai.google.dev/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A native Android application designed to help travelers discover, explore, and plan trips around **Mumbai**. Features a rich attraction catalogue, interactive embedded Google Maps with real-time location tracking, an automated itinerary planner with budget and time estimates, saved favorites, and a direct AI travel assistant powered by **Google Gemini**.

Built with Java, Material 3 components, and ViewBinding — lightweight, fast, and dependency-conscious.

---

## 📸 Key Features

### 🌟 Explore Tab
- **Interactive Search & Filter**: Real-time search as you type, with instant category filter chips (*All*, *Historic*, *Beach*, *Museum*, *Shopping*, *Nature*).
- **"Surprise Me" Discovery**: One-tap serendipitous attraction discovery.
- **Mumbai Mini-Quiz**: Test your knowledge of Mumbai landmarks with persistent progress tracking.

### 📍 Map Tab
- **Embedded Google Maps SDK**: Custom markers for every attraction with interactive detail preview sheets.
- **Auto-Fitted Camera & Live Location**: "Locate Me" Floating Action Button (FAB) with runtime location permissions.
- **Graceful Fallbacks**: If no Maps API key is configured, provides a seamless fallback panel to open coordinates in the Google Maps app.

### 📋 Itinerary Planner & Details
- **Detailed Bottom Sheet**: Highlighting attraction descriptions, entry fees, recommended visit durations, area tags, and direct actions (Add to Plan, Bookmark, Navigate).
- **Smart Itinerary**: Ordered day plans with cumulative time and budget calculation.
- **Route Optimization**: "Reorder by area" clustering to minimize transit time, with a one-click action to launch waypoints directly in external Google Maps.

### 🤖 Gemini AI Travel Assistant
- **Direct Gemini Integration**: On-device API client communicating directly with Google Generative AI (defaulting to `gemini-3.1-flash-lite` for high reliability and speed).
- **Context-Aware Recommendations**: Generates tailored advice, itineraries, and local tips under 150 words.
- **Resilient Fallback**: Offline guidance mode with retry logic in case of network disruptions or quota limits.

### 👤 Profile & Saved Places
- **Explorer Badges**: Earn milestones like *Local Curator* and *Trip Planner*.
- **Syncing Bookmarks**: Instant state synchronization across lists, maps, and detail views via persistent `SharedPreferences`.

---

## 📂 Project Architecture

```
TouristGuideMAD/
├── app/                      # Android Application Module
│   ├── src/main/java/        # Java source code (MVC/Clean architecture)
│   │   └── com/example/touristguide/
│   │       ├── AiClient.java         # Direct Gemini API integration
│   │       ├── Catalog.java          # Landmark & attractions database
│   │       ├── ChatFragment.java     # AI chat interface & state management
│   │       ├── ExploreFragment.java  # Search, filter chips, and quiz UI
│   │       ├── MapTabFragment.java   # Google Maps SDK lifecycle & markers
│   │       ├── PlanFragment.java     # Trip planner, budget/time calculator
│   │       └── Store.java            # SharedPreferences persistence layer
│   ├── src/main/res/         # Material 3 layouts, drawables, strings, themes
│   └── build.gradle.kts      # App-level build config, SDK levels & key injection
├── backend/                  # Optional standalone FastAPI proxy (for server deployments)
│   ├── main.py               # FastAPI server implementation
│   ├── requirements.txt      # Python dependencies
│   └── .env.example          # Sample server environment file
├── docs/                     # Comprehensive documentation & test cases
│   ├── PROJECT_DOCUMENTATION.md
│   └── TEST_CASES.md
├── prebuilt/                 # Standalone debug APK for testing
│   └── TouristGuide-debug.apk
├── local.properties.example  # Safe template for local API keys
└── .gitignore                # Protects credentials and build outputs
```

---

## 🚀 Getting Started & Setup

### Prerequisites
- **Android Studio** Ladybug (2024.2+) or newer
- **JDK 17**
- **Android Device or Emulator** running API 24+ (Android 7.0 Nougat or higher)

### 1. Clone the Repository
```bash
git clone https://github.com/PanavCodes/TouristGuide.git
cd TouristGuide
```

### 2. Configure API Keys Securely
This repository uses `local.properties` for key injection at compile time, guaranteeing that **no credentials or API keys are committed to Git**.

1. Copy the template to create `local.properties`:
   ```bash
   cp local.properties.example local.properties
   ```
2. Open `local.properties` and add your valid keys:
   ```properties
   ## Android SDK location (usually populated automatically by Android Studio)
   sdk.dir=C:\\Users\\YOUR_USERNAME\\AppData\\Local\\Android\\Sdk

   ## Google Maps Android SDK Key (https://console.cloud.google.com/)
   MAPS_API_KEY=AIzaSyYourGoogleMapsApiKeyHere

   ## Google Gemini API Key (https://aistudio.google.com/apikey)
   GEMINI_API_KEY=your_gemini_api_key_here
   GEMINI_MODEL=gemini-3.1-flash-lite
   ```

> [!NOTE]
> The app runs gracefully even without keys:
> - Without `MAPS_API_KEY`, the Map tab falls back to an external Google Maps launcher.
> - Without `GEMINI_API_KEY`, the Chat tab informs the user and provides curated offline recommendations.

### 3. Build & Run
You can run the app directly through Android Studio or via Gradle CLI:

```bash
# Build the debug APK
./gradlew assembleDebug

# Install on a connected emulator or device
adb install -r app/build/outputs/apk/debug/app-debug.apk
```

---

## 🔒 Security & Privacy Practices

- **Zero Credential Leaks**: All local configurations (`local.properties`), keystores (`*.jks`, `*.keystore`), and environment files (`.env`) are strictly excluded via `.gitignore`.
- **Runtime Key Binding**: Keys are read from `local.properties` during build time into `BuildConfig` and `manifestPlaceholders`.
- **Production Note**: For enterprise/production deployments, keys should be proxied through a backend service (such as Firebase AI Logic with App Check or the included `backend/` FastAPI proxy) to prevent extraction via APK decompilation.

---

## 🧪 Testing

Test cases and validation procedures are documented in [`docs/TEST_CASES.md`](docs/TEST_CASES.md).

Run unit and instrumentation checks:
```bash
./gradlew testDebugUnitTest
```

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).
