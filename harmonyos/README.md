# HarmonyOS Next Support

This Flutter plugin now supports HarmonyOS Next platform.

## Requirements

- HarmonyOS Next SDK
- Flutter SDK with HarmonyOS support
- CMake 3.14 or later

## Build Configuration

The HarmonyOS platform uses the same CMake-based build system as Linux and Windows platforms. The plugin will:

1. Build the Stockfish chess engine as a shared library (`.so`)
2. Download necessary NNUE files during build
3. Configure the library for HarmonyOS target architecture

## Platform Detection

The plugin automatically detects HarmonyOS platforms using either:
- `Platform.operatingSystem == 'harmonyos'`
- `Platform.operatingSystem == 'ohos'`

## Usage

No changes are needed in your application code. The plugin will automatically work on HarmonyOS devices just like on other supported platforms:

```dart
final stockfish = await Stockfish.create();

// Use normally
stockfish.stdin = 'isready';
stockfish.stdin = 'position startpos';
stockfish.stdin = 'go movetime 1500';

// Clean up
await stockfish.dispose();
```

## Build Files

The following files are included for HarmonyOS support:

- `harmonyos/CMakeLists.txt` - Main CMake configuration
- `example/harmonyos/` - Example app configuration for HarmonyOS
  - `CMakeLists.txt` - Example app build configuration
  - `flutter/CMakeLists.txt` - Flutter integration
  - `runner/CMakeLists.txt` - Runner executable configuration

## Notes

- HarmonyOS is treated as a mobile target, so only the smaller NNUE file is downloaded
- The same compilation flags and optimizations as Android are applied
- Build artifacts are generated as `.so` shared libraries