# KioskMode — Privacy Policy

_Last updated: 17 October 2026_

KioskMode is a kiosk/lockdown web browser for iPhone, iPad and Android. This
policy describes exactly what the app does with your data.

Contact: **apps.lucian7977@gmail.com**

## Short version

- There is **no KioskMode account, no cloud backend and no analytics or
  tracking of ours**. The app never contacts a server we operate.
- Everything you configure is stored **locally on the device**.
- Web pages you load are fetched **directly by the system web view** from the
  site you chose — not through us.
- Camera frames are processed **on the device only** and are never stored or
  transmitted.

## What the app stores, and where

Everything lives in the app's private storage on the device (Android
`SharedPreferences`; iOS `Application Support`). Nothing is uploaded by the
app.

| Data | Why |
| --- | --- |
| The kiosk profile: start URL, allow/block patterns, PIN, exit gesture, display, idle and screensaver settings, remote-admin password | So the device behaves as you configured it |
| A store-purchase receipt (Android: product id, purchase token, order id, purchase time; iOS: the App Store signed transaction in the **Keychain**) | To keep the one-time unlock working offline without a time limit |
| A bounded, in-memory log ring buffer | Shown in Settings and over the local API for troubleshooting; cleared when the app is killed |
| Site data of the web pages you load (cookies, local storage, cache) | Normal web browsing; controlled by the profile's `web.clearOnReload` |

There is no account, no sync and no export to any server. Settings can export
the profile as a JSON file to a location you choose with the system dialog;
that file is only as private as the place you keep it.

## Permissions and what they are used for

**Camera**
Used only when you enable motion detection (KioskMode Plus). Frames are
downsampled on the device and compared frame to frame to detect movement —
your signage page can wake on it. Frames are never written to storage, never
analysed for identity, and never leave the device. Motion detection is off
unless you turn it on.

**Motion & Fitness (iOS accelerometer)**
Used only when you enable movement detection, to wake the kiosk and the
screensaver when the device is picked up or moved.

**Local Network**
KioskMode can run a small web server on your own network (port 2323) so you can
manage the device from a computer — read state, push a profile, stream events.
This is a LAN-only server: it does not traverse the internet and there is no
relay. You can set a password for it; without one it answers only on your LAN.
On iOS the system asks for Local Network permission the first time this is
needed.

**Notifications (Android)**
Used to show the foreground-service notification while the kiosk service is
running, as Android requires. It carries no personal data.

**Location / microphone (Android)**
The JavaScript API exposes `kiosk.getLocation()` and a permission listing
(`kiosk.getPermissions()`), so an integrated web page can read the device's
last known location or record audio **if you grant it**. The app does not
request either permission for its own use, and neither is used unless a page
you load asks for it.

**Boot / foreground service (Android)**
Used to relaunch the kiosk after a reboot or power cut, which is the point of
an unattended kiosk.

## Purchases

KioskMode Plus is a one-time, non-consumable purchase handled entirely by
**Apple (StoreKit)** on iOS and **Google Play Billing** on Android. We never see
or store your payment details. The app stores only the receipt needed to keep
the unlock working offline, and asks the store to restore it on launch and on
resume.

## What we do not do

- No first-party analytics, crash reporting service, advertising or tracking.
- No account, no cloud sync, no telemetry upload.
- No background collection of location, contacts, photos or microphone audio.
- We do not sell or share data, because we do not receive any.

## Children

KioskMode is a tool for deploying screens; it is not directed at children and
collects no personal data.

## Your control over the data

- **Delete everything:** uninstalling the app removes the profile, logs and
  local receipts from the device.
- **Revoke permissions:** in the system settings, at any time; the app degrades
  honestly and reports the missing capability instead of failing silently.
- **Purchases:** deleting the app does not delete a purchase — the store
  account owns it, and "Restore Purchases" brings it back.

## Changes

If this policy changes, the date at the top of this page changes. Material
changes will be noted in the app's release notes.