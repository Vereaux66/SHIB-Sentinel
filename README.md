# SHIB Sentinel

SHIB Sentinel is a monitoring-only Android application and optional cloud backend for rapid SHIB market alerts.

## Android monitor

The Android app watches public SHIB market WebSocket feeds from Kraken, Coinbase, and Binance. It does not require an exchange login, wallet connection, seed phrase, private key, or trading permission.

Configured upward price thresholds:

- $0.00001
- $0.0001
- $0.001
- $0.01
- $0.10
- $1.00
- $10.00

Each newly crossed threshold generates a ten-notification emergency series. The app runs as a foreground service, reconnects failed feeds, can restart after reboot when armed, and includes controls for Android notification, battery, and Do-Not-Disturb settings.

## Optional backend

The backend can independently monitor the same public price feeds. When an Ethereum WebSocket RPC endpoint is configured, it also watches the SHIB ERC-20 contract for large transfers and transfers into the canonical dead address. Optional notification providers are configured only through deployment environment variables.

Never commit live tokens, RPC credentials, wallet credentials, or `.env` files.

## Verified build

GitHub Actions reconstructs the exact source archive from `source_chunks/`, verifies SHA-256 before extraction, runs the Python backend tests and Android unit tests, and then builds `app-debug.apk`.

Expected source archive SHA-256:

`6e03d896c05ab0fa8f49456c44aafed3e6d0400055aa3797b909ad270f21c5f6`

When the workflow succeeds, open the latest **Build Android APK** run and download the `shib-sentinel-debug-apk` artifact. It contains the APK and its SHA-256 checksum.

## Samsung S23 installation

1. Download and unzip the GitHub Actions artifact.
2. Open `app-debug.apk` on the phone.
3. If Android blocks sideloading, allow **Install unknown apps** for the file manager/browser you used.
4. Open SHIB Sentinel and allow notifications.
5. Set SHIB Sentinel battery usage to **Unrestricted** and add it to Samsung **Never sleeping apps**.
6. Optionally allow its critical notification channel to bypass Do Not Disturb.
7. Tap **ARM SENTINEL**.
8. Use **TEST 10-ALERT EMERGENCY** and verify alarm sound/vibration while the phone is locked before relying on the app.

A powered-off phone, loss of network connectivity, exchange feed outage, or Android/vendor restrictions can still prevent or delay alerts. The app reduces those failure modes but cannot guarantee delivery under every device/network condition.
