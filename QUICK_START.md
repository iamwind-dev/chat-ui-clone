# 🚀 QUICK START GUIDE

## Run the App

```bash
# Install dependencies
flutter pub get

# Run on connected device
flutter run

# Run on specific device
flutter devices  # List available devices
flutter run -d <device_id>

# Run on Chrome (Web)
flutter run -d chrome

# Run on Android Emulator
flutter run -d android

# Run on iOS Simulator (Mac only)
flutter run -d ios
```

## Common Commands

```bash
# Hot reload (while app is running)
Press 'r' in terminal

# Hot restart (while app is running)
Press 'R' in terminal

# Quit app
Press 'q' in terminal

# Analyze code
flutter analyze

# Run tests
flutter test

# Build APK (Android)
flutter build apk --release

# Build iOS (Mac only)
flutter build ios --release

# Clean build
flutter clean
flutter pub get
```

## Troubleshooting

### Issue: Dependencies not found
**Solution:**
```bash
flutter pub get
```

### Issue: Build errors
**Solution:**
```bash
flutter clean
flutter pub get
flutter run
```

### Issue: Can't find device
**Solution:**
- Android: Start emulator from Android Studio
- iOS: Open Xcode and run simulator
- Web: Chrome should be available by default

### Issue: Google Fonts not loading
**Solution:**
- Ensure internet connection (fonts download on first use)
- Or fonts will be cached after first load

## File Locations

- **Main entry point:** `lib/main.dart`
- **Chat screen:** `lib/screens/chat_screen.dart`
- **Theme config:** `lib/theme/app_theme.dart`
- **Message model:** `lib/models/message_model.dart`
- **Message bubble:** `lib/widgets/message_bubble.dart`
- **Input widget:** `lib/widgets/message_input.dart`

## Test the Features

1. **Send a message:** Type and press send button
2. **Auto-reply:** Wait 1 second for bot response
3. **Try greetings:** Type "hello" or "hi"
4. **Ask questions:** Type any message with "?"
5. **Say thanks:** Type "thank you"
6. **Scroll:** Messages auto-scroll to bottom

## Customize

### Change colors:
Edit `lib/theme/app_theme.dart`:
```dart
static const Color primaryColor = Color(0xFF0084FF); // Your color
```

### Change font:
Edit `lib/theme/app_theme.dart`:
```dart
GoogleFonts.roboto() // or any Google Font
```

### Add bot responses:
Edit `lib/screens/chat_screen.dart` → `_getBotResponse()` method

## Project Structure

```
lib/
├── main.dart              ← Start here
├── models/
│   └── message_model.dart ← Message data structure
├── screens/
│   └── chat_screen.dart   ← Main chat UI
├── widgets/
│   ├── message_bubble.dart ← Individual message
│   └── message_input.dart  ← Input field
└── theme/
    └── app_theme.dart      ← Colors & styles
```

## Tips

- 💡 Use hot reload ('r') to see UI changes instantly
- 💡 Check console for debug messages
- 💡 Use Flutter DevTools for debugging
- 💡 All code is commented - read through it!
- 💡 Start with `main.dart` to understand flow

## Need Help?

1. Check `README.md` for detailed info
2. Read `PROJECT_SUMMARY.txt` for overview
3. Look at inline code comments
4. Run `flutter doctor` to check setup

---

**Ready? Run: `flutter run`** 🚀
