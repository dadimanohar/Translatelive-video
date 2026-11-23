# TeluguTutor Mobile (Android alpha)

This repository contains the native Android port source. The Android app is separate from the Windows desktop build; it does not wrap or run the Windows executable.

## Build
A GitHub Actions workflow builds a debug APK for Android:
- Open **Actions → Build TeluguTutor Android APK**
- Download the **TeluguTutor-Mobile-debug-APK** artifact from a successful run.
- Install the APK on an Android device. Debug APKs are not Play Store releases.

## Source archive
The native project archive is stored in `.payload/part-*.b64` fragments because GitHub's text-file upload action does not accept binary ZIP uploads. The workflow reassembles it and validates the tar archive before building.

## Key Android limitations
- For reliable English-muted / Telugu-only dubbing, use videos played inside the TeluguTutor player. The app taps its decoded audio before muting the English output, translates in short segments, pauses the video for Telugu speech, then resumes.
- It cannot mute YouTube, Chrome, or another independent app system-wide. Android playback capture is restricted by Android and the source app's capture policy.
- Supports local media files and direct MP4/HLS stream URLs. A normal YouTube watch-page URL is not a direct media stream and isn't supported by this alpha.
- Offline translation requires the ML Kit Telugu language model to be downloaded once. On-device speech recognition availability depends on the Android device and installed speech service.
- Cloud providers require valid API keys; keys are encrypted using Android Keystore on the device.

See [Android project README](TeluguTutor-Android/README.md) and [device test checklist](TeluguTutor-Android/DEVICE_TEST_CHECKLIST.md) after the workflow expands the embedded archive.
