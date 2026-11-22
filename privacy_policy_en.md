# BMSViewer Privacy Policy


App: BMSViewer, listed on Google Play as "BMS Battery Monitor: LiFePO4" (package local.bmsviewer.app).

Developer: Alan Spohr Perius

Effective date: 2026-11-22

Contact: alan.perius.mv@gmail.com

BMSViewer is an Android app that connects over Bluetooth Low Energy (BLE) to the BMS (battery management system) of JK, LiTime, JBD and Daly batteries (read-only; LiTime, JBD and Daly are experimental), and reads Victron devices (experimental) from their Bluetooth advertisement, without connecting and without sending anything to the device; for this it needs the device's encryption key, obtained from VictronConnect. The app shows the data on screen. Optionally, you can turn on remote monitoring to send your readings, end-to-end encrypted, to another phone of yours or of someone you authorized (section 5). The app only sends read requests (for a JK BMS: device information and cell information; for a LiTime battery: one status request; for JBD and Daly BMSs: read requests only; for Victron devices: nothing is sent) and enables notifications. It never changes any BMS setting and never asks for Bluetooth pairing; if Android asks to pair, decline.

## 1. Summary


- Remote monitoring is optional and off by default. Unless you turn it on, the app does not send data to the developer's servers or to any third party. Your readings stay on your phone unless you export them. Reading your battery over Bluetooth works offline.

- If you turn remote monitoring on, your readings are sent end-to-end encrypted to the developer's server. The encryption keys exist only on your phone and on the phones you authorize, so the developer cannot read your readings.

- The app declares the INTERNET and ACCESS_NETWORK_STATE permissions only for remote monitoring. They are not used for anything else: no ads, no analytics, no crash reports.

- No ads, no analytics, no crash-reporting SDK.

- No account, sign-up or login. No purchases.

## 2. Data the app reads


When connected to your BMS (JK, LiTime, JBD or Daly) or when reading a Victron device, the app reads:

- Battery reading: state of charge (SOC), voltage, current, power and remaining capacity.

- Voltage of each cell and the difference between cells.

- Temperatures (several sensors). In the history, the app stores the maximum temperature.

- Diagnostics: permission and Bluetooth state, signal strength, firmware variant and a connection log with fixed texts. This screen is not saved on the device.

- Victron devices: the app reads the device's Bluetooth advertisement, without connecting and without sending anything to it. To decode the advertisement it uses the device's encryption key, which you get from VictronConnect and enter in the app.
- An opaque battery identifier, which may be the Bluetooth address of the BMS. It is used to recognize your saved battery and is never shown in the app.

The app does not use your location, contacts, photos, microphone, camera or advertising identifier. It creates a file only when you export history as CSV (section 5). If remote monitoring is on, the app also uses a random channel token and encryption keys (section 5).

## 3. Permissions and why


- Nearby devices, scan (BLUETOOTH_SCAN, Android 12+): find your BMS. Declared with "neverForLocation", so the scan is not used to infer your location.

- Nearby devices, connect (BLUETOOTH_CONNECT, Android 12+): connect to the BMS you choose.

- Bluetooth and Bluetooth admin (BLUETOOTH, BLUETOOTH_ADMIN), Android 11 and older only: older equivalents of the two above.

- Approximate and precise location (ACCESS_COARSE_LOCATION, ACCESS_FINE_LOCATION), Android 11 and older only: Android requires it to scan for Bluetooth devices on those versions. The app does not read or store your location.

- Foreground service (FOREGROUND_SERVICE, FOREGROUND_SERVICE_CONNECTED_DEVICE): keeps the Bluetooth connection to the BMS while the app is in the background, in two cases (and, if you turn on remote monitoring, it also keeps the app running so encrypted readings can be uploaded at the interval you chose). (1) By default ("Always connected" off): if a live reading is running when you leave the app, the connection is kept for a grace period of about 60 seconds, then the app closes the connection and the service stops. (2) With "Always connected" on: the connection is kept until you turn the setting off, tap Disconnect in the notification, or tap Stop in the app. When this phone starts sending, the app turns this setting on and locks it in Settings while it is sending. If you pause sending it stays on, but you can turn it off in Settings; when you stop and delete the sending, it goes back to what it was before.

- Notifications (POST_NOTIFICATIONS): used only for the notification of that foreground service. It shows the battery charge percentage and power, and can be visible on the lock screen. If you deny the notification permission, the connection is still kept, but without a visible notice. The app sends no other notifications; alerts appear only inside the app.

- Internet (INTERNET) and network state (ACCESS_NETWORK_STATE): used only if you turn on remote monitoring, to send and receive encrypted readings and to check whether the phone is online. Not used otherwise.

- Wake lock (WAKE_LOCK): one partial wake lock, held for at most 75 seconds. It covers the 60-second background grace period, releasing the Bluetooth link and one reconnect cycle. It is held even when "Always connected" is off.

The app registers no link in Android: no link opens the app. It only opens the system settings page of the app, through the standard Android feature.

## 4. What is stored on your device


Everything the app keeps on the phone is stored in the app's private storage:

- Saved batteries (up to 10), each with an opaque identifier (which may be the Bluetooth address, never shown) and a nickname you choose; the pinned battery.

- Language, theme (auto, dark or light), alert thresholds and the "Always connected" setting.

- The last reading of each battery.

- Reading history per battery: SOC, voltage, current, power, cell difference, minimum and maximum cell voltage and maximum temperature. Kept per minute, then grouped into 15-minute intervals after 48 hours, for up to 30 days, capped at about 2.5 MB.

- The Victron encryption key: stored in Android's Keystore-backed secret store, on your phone only, and never sent anywhere.
- Saved Victron devices: nickname and capacity, stored on the phone.
- On the viewing phone: a local, already decrypted copy of the readings received in the last 7 days, so the last reading can be shown offline.
- If you use remote monitoring: its on/off setting, the list of authorized viewer phones, the random channel and viewer tokens, and the encryption keys. Android backup stays disabled, so these are not copied to the cloud.

Apart from the Victron key (in the Keystore), the app does not encrypt data at rest; it relies on Android's app-private storage. Automatic Android backup (cloud and device-to-device transfer) is disabled for the app.

## 5. Export, sharing and remote monitoring


- With remote monitoring off, the developer receives no data.

- With remote monitoring on, the sending phone encrypts each reading on the phone before it is sent. Authorized viewer phones download and decrypt it. The keys are only on those phones; the developer cannot read the readings.

- What is sent, all end-to-end encrypted: charge, voltage, current and power; capacity, remaining charge and the time estimate; number of cells, the lowest and highest voltage and the difference; temperatures; BMS alarms and brand; for a bank, how many batteries it has, how many were read and the lowest charge. From this phone: whether it is plugged in, its charge and temperature, kind of internet, whether Bluetooth is reading the battery or was stopped, the upload interval, battery saving, whether notifications are allowed, last restart, the phone's restart count (an Android counter, used only to know whether the phone restarted; on its own it does not identify the device), time since it started, number of stored readings, app version and whether it is sending. And the name each authorized phone chooses. Not sent: GPS location, name, email, the battery's Bluetooth address, the battery password, the battery nickname and the Victron key.
- What the server stores: the encrypted readings; the channel and viewer tokens, stored only as hashes; and pairing and usage metadata (which viewer phones are linked to a channel, viewer entries, and the times, sequence numbers, key epoch and sizes of uploads). The server has no account, email address, name, device identifier, advertising identifier or location.

- IP address: the hosting provider (Railway, USA) may record the IP address in its technical logs; the app and the server do not store the IP address. To limit abuse, the server uses only a short-lived, daily-salted hash of the IP address prefix, kept in memory for rate limiting.

- The server is hosted on Railway, which processes data on the developer's behalf. Nothing is sold or used for advertising or analytics.

- Pairing is only by a code you type, confirmed with a verification number on both phones. You choose who can view: only people you authorize. Removing a viewer revokes its access when the server confirms; if it does not confirm, the app tells you.

- On the History screen you can export a CSV file through the Android share sheet. This happens only when you tap export. The app creates a temporary file for sharing. The file contains UTC timestamps and the readings only, with no battery identifier, nickname or Bluetooth address.

- By itself, the app sends the CSV nowhere. You choose the destination app, and from then on that app's own privacy policy applies.

- The app does not sell data or share it with third parties by itself.

## 6. Retention and deletion


- History is kept for at most 30 days and capped at about 2.5 MB.

- "Erase history of this battery" deletes only the history of that battery.

- The app has no function to remove a saved battery. To remove saved batteries, identifiers, nicknames, last readings and settings, clear the app data in Android settings or uninstall the app.

- Local data: you delete it as described above; the developer has no access to it.

- Remote data, encrypted readings: deleted from the server automatically after 7 days.

- Remote data, channel record and metadata (links between phones, viewer entries, upload times, sequence numbers, key epoch and sizes): kept until 180 days without receiving uploads, then deleted (7 days if the channel never received any upload and no viewer was authorized). Viewers unused for 180 days are also deleted. Expired pairings and pending viewers are deleted after 1 hour.

- "Stop and delete the server data" in the app deletes the server copy as follows: if the server accepts the request, it is deleted right away; with no network, the request stays pending and the app retries; if access is refused (the phone lost access), the app erases the data on the phone but cannot confirm it on the server, and the server copy expires by itself at the end of the retention period. Removing a viewer revokes its access when the server confirms; if it does not confirm, the app tells you. The server keeps no email, name or other identification of you, so the developer cannot find your data from an email address: delete from the app or wait for automatic expiry.

- No database backups are configured (no scheduled copies, no point-in-time recovery). If that changes, this policy is updated first.
- A CSV you exported is a separate file outside the app; delete it yourself where you saved or sent it.

## 7. Children


The app is not directed at children and does not knowingly process children's data.

## 8. Changes


Changes to this policy will be published on this page with a new effective date. Effective date 2026-11-22: added optional remote monitoring and reading of Victron devices.

## 9. Contact


alan.perius.mv@gmail.com

---
