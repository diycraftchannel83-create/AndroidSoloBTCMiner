# AndroidSoloBTCMiner — NerdMiner Solo Android

A GitHub Actions build pipeline for an Android-only Bitcoin SHA-256d mining experiment. The APK is based on the MIT-licensed upstream project [VirtusVerbis/BTC_Anrdoid_Miner](https://github.com/VirtusVerbis/BTC_Anrdoid_Miner), branded as **NerdMiner Solo** for this repository.

## Build an APK

1. Open the **Actions** tab in this repository.
2. Select **Build NerdMiner Solo APK**.
3. Press **Run workflow** on the `main` branch.
4. Wait for the job to finish.
5. Open the completed workflow run and download the artifact named **NerdMiner-Solo-Android-debug**.
6. Extract the ZIP and install `app-debug.apk` on your Android device. Android may ask you to allow installation from the browser/file manager.

The workflow checks out the upstream source at its current `main` revision, applies the app label and application ID, installs Android NDK/CMake and the GLSL shader compiler, builds the debug APK, and verifies that the APK exists. The APK artifact is retained for 14 days.

## Important implementation notes

- This app mines directly on the Android device; it is not ESP32 firmware and does not control a NerdMiner board.
- It uses SHA-256d/Stratum mining code from the upstream project. Pool protocol compatibility varies; use the pool settings supported by the app and verify the server's current requirements.
- This repository currently builds the upstream app with NerdMiner Solo branding. The mining engine and most UI are maintained upstream; this workflow does not claim to be an independently rewritten miner.
- A debug APK is suitable for testing, not a signed production release. Each locally signed release needs a signing key kept private.
- Never enter a wallet seed phrase or private key. Only use a public Bitcoin receiving address. Pool mining has no guaranteed reward; phone CPU mining is unlikely to find a Bitcoin block and can cause heat, battery wear, and thermal throttling.

## Test checklist

1. Install APK on a supported ARM64 Android device.
2. Open app and verify it launches without crashing.
3. Enter a valid public BTC receiving address and a pool endpoint supported by the app.
4. Confirm connection/subscription and worker authorization status.
5. Run at low CPU thread count for 5–10 minutes; confirm displayed hashrate and no sustained overheating.
6. If the pool reports shares, confirm accepted/rejected counters agree with pool-side stats.
7. Stop mining and verify CPU activity stops.
8. Test invalid wallet address, unreachable host, and incorrect port; the app should report errors rather than claim mining is active.
9. Confirm no seed phrase or private key is requested.

## License

The upstream project declares the MIT License. Its copyright and license notice must be retained in redistributed copies. See the upstream repository's `LICENSE` file.
