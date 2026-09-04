# TGW Weather

**The Greco Weather**

A lightweight, browser-based weather comparison workspace for reviewing daily forecasts from multiple weather providers in one place.

TGW Weather is built as a **Single-File Local Application (SFLA)**. The complete application runs from a single HTML file with no application server, package manager, framework, installation process, or third-party runtime dependencies.

Enter a location, choose the weather services you want to use, and compare their forecasts side by side with a simple consensus for high temperature, low temperature, chance of rain, and wind speed.

> **Today's weather. More than one opinion.**

![TGW Weather screenshot](screenshot.jpeg)

## Run TGW Weather

**[▶ Run TGW Weather in your browser](https://mikejamesgreco.github.io/tgw-weather/)**

No installation is required. The GitHub Pages version runs TGW directly in your browser, just like opening the standalone `tgw-weather.html` file locally. Forecast requests are made directly from the browser to the weather services you enable.

---

## Why TGW Weather?

Weather services do not always agree.

Different providers may use different forecast models, update schedules, geographic grids, and interpretation methods. Looking at a single service can hide that disagreement.

TGW Weather takes a different approach.

```text
                 Location
                    │
                    ▼
        ┌───────────────────────┐
        │      TGW Weather      │
        │                       │
        │  Open-Meteo           │
        │  NWS                  │
        │  WeatherAPI.com       │
        │  OpenWeather          │
        │  Visual Crossing      │
        │  Tomorrow.io          │
        │  Weatherbit           │
        │                       │
        └───────────┬───────────┘
                    │
                    ▼
          Forecast Comparison
                    │
                    ▼
            Daily Consensus
```

The goal is not to create another weather forecast. It is to make several forecasts easier to compare.

---

## Core Principles

TGW Weather is designed around a few simple principles:

- **Single-file application** — the application is distributed as one HTML file.
- **Browser-native** — the application runs directly in a modern browser.
- **Zero third-party runtime dependencies** — no frameworks, CDNs, or runtime packages are required.
- **Provider comparison** — forecasts remain visible individually rather than being hidden behind a single calculated value.
- **Consensus with context** — averages are accompanied by provider ranges so disagreement remains visible.
- **User-controlled providers** — each weather service can be enabled or disabled.
- **User-owned API keys** — TGW does not distribute shared API credentials.
- **Local configuration** — provider choices and API keys are stored in the browser using `localStorage`.

---

## Getting Started

No installation is required.

1. Open the **[hosted TGW Weather](https://mikejamesgreco.github.io/tgw-weather/)** or open `tgw-weather.html` locally in a modern browser.
2. Enter a ZIP/postal code, city and state, or latitude/longitude.
3. Review the enabled weather providers.
4. Add personal API keys for any optional keyed services you want to use.
5. Choose **Get Forecast**.
6. Compare the provider forecasts and consensus values.

Open-Meteo and the U.S. National Weather Service do not require API keys.

---

## Forecast Comparison

TGW presents the available daily forecast from each successfully queried provider.

Current comparison fields include:

- Forecast description
- Daily high temperature
- Daily low temperature
- Chance of rain
- Wind speed
- Provider-specific details link

TGW also calculates consensus values for:

- High temperature
- Low temperature
- Chance of rain
- Wind speed

The consensus is a simple arithmetic average of providers that successfully report each metric.

The displayed range helps show how closely the providers agree.

---

## Weather Providers

TGW Weather currently supports:

| Provider | API Key | Notes |
| --- | --- | --- |
| Open-Meteo | No | Global forecast data |
| U.S. National Weather Service | No | U.S. locations only |
| WeatherAPI.com | Yes | Optional personal API key |
| OpenWeather | Yes | Optional personal API key |
| Visual Crossing | Yes | Optional personal API key |
| Tomorrow.io | Yes | Optional personal API key |
| Weatherbit | Yes | Optional personal API key |

Each provider can be individually enabled or disabled.

Keyed providers are called only when the provider is enabled **and** a key has been supplied.

Free plans, quotas, licensing terms, and API availability can change. Check each provider's current terms before relying on a service for production or commercial use.

---

## API Keys and Provider Settings

TGW Weather does not ship with shared API credentials.

Users can enter their own API keys for supported services. Provider choices and keys are stored in the browser using `localStorage`.

The **Weather Services & API Keys** section shows the current state of each provider:

- **Enabled — ready to call**
- **Enabled — add an API key to include this source**
- **Disabled — will not be called**

Click **Save Provider Settings** to preserve the current provider configuration in the browser.

Because TGW Weather is a browser application, JavaScript must be able to read a saved key in order to send it to the corresponding weather provider. Users should treat those keys as browser-accessible credentials and follow each provider's guidance.

---

## Location Handling

TGW Weather accepts several location formats:

- ZIP or postal code
- City and state
- Latitude and longitude

TGW resolves a named location to coordinates first, then sends the same general latitude and longitude to each enabled provider.

Using a common point makes the provider comparison more consistent.

---

## Local-First Architecture

TGW itself does not require a backend application server.

```text
┌──────────────────────── Browser ────────────────────────┐
│                                                        │
│ Location ──► TGW Weather ──► Provider APIs             │
│                  │                    │                 │
│                  │                    ▼                 │
│                  └────────────► Forecast Results        │
│                                      │                 │
│                                      ▼                 │
│                              Compare / Consensus        │
│                                                        │
│ Provider settings and API keys remain in localStorage. │
└────────────────────────────────────────────────────────┘
```

Unlike SFLAs that operate entirely on local files, TGW intentionally communicates with external weather services when a forecast is requested.

The application itself remains a standalone browser application.

---

## Single-File Local Application (SFLA)

TGW Weather follows an architecture we refer to as a **Single-File Local Application**, or **SFLA**.

An SFLA is a complete browser application designed to operate primarily from a single self-contained file.

For TGW this means:

```text
tgw-weather.html
```

contains the application.

No runtime installation is necessary.

The surrounding repository contains documentation and supporting project files, but they are not required to run the application itself.

---

## Repository Structure

The repository is intentionally simple.

```text
tgw-weather/
│
├── index.html              # GitHub Pages launcher
├── tgw-weather.html        # Standalone TGW application
├── screenshot.jpeg         # README screenshot
├── README.md
└── LICENSE
```

The application filename intentionally does not contain a release number. The current release version is maintained internally through the single `APP_VERSION` JavaScript variable and is displayed from the application's Help page.

---

## Help

TGW Weather includes embedded Help covering:

- Forecast consensus
- Supported providers
- API keys
- Provider settings
- Location input
- Differences between provider forecasts
- Privacy and local-first behavior
- Current application version
- GitHub documentation

---

## Browser Support

TGW Weather is designed for modern browsers.

Because forecast services are called directly from browser JavaScript, normal browser security rules apply, including **Cross-Origin Resource Sharing (CORS)**.

A weather provider must permit browser requests from the current origin for TGW to call it successfully.

Provider behavior and browser policies may change over time.

---

## Privacy

TGW does not require a TGW account or TGW-hosted application server.

Provider settings and API keys are stored locally in the browser using `localStorage`.

When a forecast is requested, the browser sends location information and any required API key directly to the enabled weather provider.

Users should consider the privacy policies and terms of the external weather services they choose to enable.

---

## Project Status

TGW Weather is under active development.

The initial focus is daily forecast comparison and simple provider consensus. Additional forecast views, provider integrations, and comparison features may evolve over time.

---

## Philosophy

TGW is intentionally small.

The objective is not to replace the individual weather services. It is to put their forecasts beside one another so differences are easier to see.

```text
No framework.
No package manager.
No application server.
No shared API credentials.

Just a browser, a location, and several weather opinions.
```

---

## Related SFLA Projects

- **TGG Grid — The Greco Grid**  
  https://mikejamesgreco.github.io/tgg-grid/

- **TGDS Data Scope — The Greco Data Scope**  
  https://mikejamesgreco.github.io/tgds-scope/

- **TGJVM Monitor — The Greco JVM Monitor**  
  https://mikejamesgreco.github.io/tgjvm-monitor/

- **SFLA Home**  
  https://mikejamesgreco.github.io/

---

## License

License information will be added to the repository's `LICENSE` file.

---

## Author

**Michael J. Greco**

TGW Weather — **The Greco Weather**

© mikejamesgreco.me LLC. All rights reserved.
