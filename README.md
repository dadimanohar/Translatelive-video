# TeluguTutor Mobile 1.2.0-beta3

Native Android live-dubbing build for testing on a phone or tablet. This is a separate Android implementation, not a wrapped Windows executable.

## What this build does

- Plays local videos and direct MP4/HLS streams inside its own Media3 player.
- Mutes the source English track inside that player while copying the decoded PCM audio before output mute.
- Runs offline English recognition with a bundled Vosk model, or Groq Whisper when configured.
- Translates into Telugu with the selected cloud provider or ML Kit on-device translation.
- Speaks Telugu using the device's installed Telugu Text-to-Speech voice.
- Pauses the video while each captured phrase is translated and spoken, then resumes.

## Install the APK

1. Open **Actions → Build and test TeluguTutor Android APK**.
2. Download artifact **TeluguTutor-Mobile-1.2.0-beta3-APK** from the latest successful run.
3. Extract the artifact ZIP and install `app-debug.apk` on your Android 10+ device.
4. Verify the APK checksum using the accompanying `app-debug.apk.sha256` file.

The debug APK targets ARM64 and x86_64. It is not a Play Store release and is unsigned for Play Store distribution.

## First launch

The approximately 40 MB Vosk English speech model is bundled in the APK and installed into app-private storage on first launch. Wait for the speech engine status to report **READY**. For offline Telugu translation, connect to Wi-Fi once and tap **Save settings / Prepare offline engines** to download the ML Kit English-to-Telugu model. You also need an installed Telugu (India) Text-to-Speech voice.

For cloud mode, set the Groq speech key and the selected translation provider key separately. Use **Test Groq speech key**, **Test translation API**, and **Test Telugu voice** before starting playback.

## Real platform limits

- Android apps cannot reliably capture/mute audio from every other app. This app only replaces sound for video played inside its own player.
- YouTube watch-page URLs and DRM-protected streams are not supported as direct video streams. Use a local file or a direct MP4/HLS media URL.
- Dubbing is phrase-by-phrase. The player pauses while the Telugu phrase is generated and spoken. It is not seamless frame-accurate dubbing and may have noticeable pauses.
- Vosk small English is a compact ASR model; its accuracy may vary with Indian-English accents, noisy audio, music, and specialist vocabulary.
- Offline translation requires the one-time ML Kit model download. Telugu TTS availability depends on the Android device and installed voice.

## Build and test gates

The GitHub Actions workflow downloads the Vosk model, verifies its SHA-256, embeds it in the APK, compiles the Android app, runs instrumentation tests on an Android emulator, verifies that the APK contains Vosk native libraries and model assets, and uploads the APK plus checksum.

A passing emulator build does not prove that every physical phone, video codec, network source, or TTS voice works. Test it on the actual device.

## Source layout

The exact Android source snapshot used by the workflow is encoded in `.payload/beta3/part-*.b64`; the workflow reassembles it before building. The source archive is also available from the ChatGPT conversation where this build was produced.
