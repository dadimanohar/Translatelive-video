# TeluguTutor 1.2.0

Windows desktop app for real-time English system-audio capture, English speech recognition, Telugu translation, and optional Telugu speech playback.

## Source

The complete application source tree is packaged in **TeluguTutor-1.2.0-source.tar.xz** in this repository. It includes the Python application, tests, Windows installer definition, model fetcher, third-party notices, and its own project README. The large model weights are intentionally not committed; the Windows build downloads and verifies them before packaging.

Extract the source archive with 7-Zip or:

```powershell
tar -xJf TeluguTutor-1.2.0-source.tar.xz
```

Then read the extracted `README.md`.

## Windows installer

GitHub Actions builds the single-file Windows installer on a Windows runner. The build runs the automated tests, downloads and self-tests all four offline model assets (Whisper Tiny, NLLB-200, MMS Telugu TTS, and the Qwen3 0.6B GGUF local LLM), builds the standalone application, and compiles the Inno Setup installer.

The output is named `TeluguTutor_Setup.exe`. Download the `TeluguTutor-Windows-Installer` artifact from the Actions run after the workflow succeeds.

## Hardware and licence notes

The target is 64-bit Windows 10/11. A 4 GB RAM system is low-memory for continuous offline speech recognition, translation, local LLM explanation, and speech synthesis; performance may be slow. The bundled NLLB and MMS model weights are CC-BY-NC 4.0 and this model bundle is intended for personal/non-commercial use. See `THIRD_PARTY_NOTICES.md` inside the source archive.
