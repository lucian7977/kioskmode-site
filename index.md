# KioskMode — Support

_Last updated: 17 October 2026_

KioskMode is a native kiosk/lockdown browser for **iPhone, iPad and Android**
(phones, tablets and Android TV). Point it at one web page and it fills the
screen, hides every bar and stays there.

Contact: **apps.lucian7977@gmail.com**

## Getting out of kiosk mode

There is no default PIN, and the exit gesture is always available:

- **Tap the top-left corner 7 times within 2.5 seconds.**
- Or use the gesture you configured in Settings: long-press the top-left corner
  for 3 seconds, or swipe up then down inside the top-left corner.
- If you set a PIN, you are asked for it; with no PIN the exit goes straight to
  Settings.

The top-left corner used for the gesture is generous (the top-left 40% of the
screen), so you do not have to hit a small target — remote controls work too:
any key on an Android TV remote wakes the screensaver.

## Configuring it

Open **Settings** with the exit gesture. Everything is a dotted key in a
versioned JSON profile, for example:

```
web.startUrl        https://dashboard.example.com
kiosk.enabled       true
kiosk.pin           1234
web.allowlist       ["*example.com"]
idle.screensaver.delaySec   60
```

The same profile schema is used on iOS and Android, so a profile you export on
one device imports on the other. Settings can also export/import the whole
profile as JSON.

## Free and Plus

**Free, for ever:** full-screen browsing of any web page, immersive display,
lockdown with PIN/gesture, URL allow/block policy, reload rules, the watchdog
with crash-loop breaker and safe mode, launch on boot, the versioned JSON
profile, and the `window.kiosk` JavaScript API with all core getters.

**KioskMode Plus (one small one-time purchase, no subscription):** screensaver
(clock, images, video or a web page), on-device motion detection, anti burn-in,
power schedule, the full remote admin API, and injected JavaScript.

Prices are shown by the App Store / Google Play in your local currency.
Purchases can be restored from the paywall or from Settings.

## Remote admin

The remote server listens on port **2323** on your local network. Two endpoints
are free, the rest needs Plus:

```
curl "http://<device-ip>:2323/api/health"
curl "http://<device-ip>:2323/api/state?password=<pw>"
curl -N "http://<device-ip>:2323/api/events?password=<pw>"   # live events (SSE)
```

There is no cloud relay: the server is reachable only from the same LAN, and
you can set a password for it.

## Requirements

- iOS / iPadOS **16.0** or later.
- Android **7.0** (API 24) or later; Android TV is supported.

## Known behaviour worth knowing

- **Screen pinning on Android.** Without Device Owner, Android asks you to
  confirm screen pinning once when the kiosk engages. Tap **OK**; tapping
  "No thanks" means it will ask again next launch.
- **What cannot be locked.** No app can be a true boot-locked single-app kiosk
  without MDM on iOS or Device Owner on Android. KioskMode reports the
  difference honestly at runtime through `kiosk.capabilities()`.
- **Guided Access on iOS** must be started manually (triple-click) unless the
  device is supervised by MDM.
- **Local network permission on iOS** is required before the remote API is
  reachable from another machine.

## Privacy

See the [privacy policy](privacy.html). In one line: no account, no cloud, no
analytics of ours; everything you configure stays on the device.

## Troubleshooting

- **The app shows a page that is not yours** — the built-in welcome page is
  shown when `web.startUrl` is empty. Set a URL in Settings.
- **Remote API unreachable** — make sure the device and your computer are on the
  same network, the port is not blocked, and (iOS) local-network permission was
  granted.
- **Nothing opens on Android TV** — the banner and leanback launcher entry are
  required for the TV row; the app must also be the chosen HOME app for the
  HOME key to re-enter the kiosk.