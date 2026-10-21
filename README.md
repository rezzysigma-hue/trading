# EventEdge AI (prototype)

An Android-first, offline-capable event research and paper-trading prototype. This repository is designed to build a debug APK with GitHub Actions.

## What works in this prototype

- Six navigable app areas: Home, Events, Markets, Strategy Lab, Portfolio, Settings (six bottom navigation destinations; the dashboard is Home).
- Bundled sample event feed and search/category filtering.
- Public GDELT article search from the Events screen (internet required; articles are leads, not verified trading signals).
- Stooq daily historical CSV lookup from Markets (availability and delay are not guaranteed; not real-time executable quotes).
- Local simulated cash balance and simulated buy records.
- Local persistence of mode, balance, emergency-stop state and simulated P/L.
- Emergency stop blocks simulated order recording.
- GitHub Actions workflow builds and uploads a debug APK.

## Important limitations

- This is **not** a trained AI trading system or a complete historical backtester.
- Market data is historical/delayed where available. No real-time exchange feed is promised.
- No broker integration, payment processing, Google Pay, live order submission, or real-money trading is included.
- The current simulated order reserves cash but does not calculate share units, execution prices, fees, or mark-to-market portfolio valuation.
- Public news may be incomplete, duplicated, misleading or delayed. Verify information independently.
- No profits are promised.

## Build with GitHub

1. Create a GitHub repository.
2. Upload the contents of this folder (the files inside `EventEdgeAI`, not an extra nested ZIP directory).
3. Open **Actions** and choose **Build EventEdge AI APK**.
4. Select **Run workflow**, or push to `main`/`master`.
5. Wait for the workflow to finish successfully.
6. Open the successful run and download the `eventedge-ai-debug-apk` artifact.
7. Extract the artifact ZIP and install `app-debug.apk` on your Android device. Android may ask you to allow installation from the browser/files app.

The workflow installs Gradle 8.11.1 and uses JDK 17. The Android Gradle Plugin is pinned to 8.9.2.

## Build locally

Install JDK 17, Android SDK platform 35 and Gradle 8.11.1, then run:

```bash
gradle testDebugUnitTest
gradle assembleDebug
```

The APK is created at `app/build/outputs/apk/debug/app-debug.apk`.

## Data sources

- GDELT DOC API: `https://api.gdeltproject.org/api/v2/doc/doc`
- Stooq daily CSV: `https://stooq.com/q/d/l/`

These are public endpoints; access, terms, availability, coverage and latency may change. No API keys are embedded.

## Next engineering steps

1. Replace simulated-only order accounting with a tested ledger and deterministic fill simulator.
2. Add data-source unit tests and fixtures.
3. Add robust article de-duplication, provenance and publication-time handling.
4. Implement a real historical backtester with fees, slippage, look-ahead prevention and out-of-sample evaluation.
5. Add a secure optional Python research service.
6. Assess broker eligibility and legal requirements before considering live execution.
