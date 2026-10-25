# Test Plan — NerdMiner Solo Android

## Build/CI
- [ ] GitHub Actions workflow completes successfully.
- [ ] APK file exists and is non-empty.
- [ ] APK installs on Android API 24+ device/emulator compatible with the native ABI.

## App and configuration
- [ ] App opens and displays NerdMiner Solo branding.
- [ ] Pool host/port can be edited and persist as expected.
- [ ] Invalid or blank BTC address is rejected.
- [ ] Public receiving address is used; no seed phrase/private key is requested.

## Mining
- [ ] Connection errors are visible for invalid host/port.
- [ ] Successful Stratum authorization is reflected in UI.
- [ ] Hashrate is non-zero only while a hashing worker is active.
- [ ] Accepted/rejected shares are counted from actual pool responses, not simulated.
- [ ] Stop control stops mining and releases CPU workers.
- [ ] Low-thread test runs 5–10 minutes with temperature checked manually.

## Safety
- [ ] Test at low CPU intensity first.
- [ ] Stop if device becomes uncomfortably hot, throttles, or battery swells.
- [ ] Confirm app does not request wallet seed phrase or private keys.

A successful CI build confirms compilation and artifact creation only. It does not by itself prove pool compatibility, accepted shares, or successful block discovery; those require on-device and pool-side testing.
