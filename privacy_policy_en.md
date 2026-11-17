# BMSViewer Privacy Policy

Developer: Alan Spohr Perius
Effective date: 2026-11-16
Contact: alan.perius.mv@gmail.com

BMSViewer is an Android app that connects over Bluetooth Low Energy (BLE) to the BMS (battery management system) of a battery that uses a JK BMS and shows its data on screen. The app only sends read requests (device information and cell information) and enables notifications. It never changes any BMS setting.

## 1. Summary

- By itself, the app does not send data to the developer's servers or to any third party. Your readings stay on your phone unless you export them.
- The app does not declare the INTERNET permission.
- No ads, no analytics, no crash-reporting SDK.
- No account, sign-up or login. No purchases.

## 2. Data the app reads

When connected to your BMS, the app reads:

- Battery reading: state of charge (SOC), voltage, current, power and remaining capacity.
- Voltage of each cell and the difference between cells.
- Temperatures (several sensors). In the history, the app stores the maximum temperature.
- Diagnostics: permission and Bluetooth state, signal strength, firmware variant and a connection log with fixed texts. This screen is not saved on the device.
- An opaque battery identifier, which may be the Bluetooth address of the BMS. It is used to recognize your saved battery and is never shown in the app.

The app does not use your location, contacts, photos, microphone, camera or advertising identifier. It creates a file only when you export history as CSV (section 5).

## 3. Permissions and why

- Nearby devices, scan (BLUETOOTH_SCAN, Android 12+): find your BMS. Declared with "neverForLocation", so the scan is not used to infer your location.
- Nearby devices, connect (BLUETOOTH_CONNECT, Android 12+): connect to the BMS you choose.
- Bluetooth and Bluetooth admin (BLUETOOTH, BLUETOOTH_ADMIN), Android 11 and older only: older equivalents of the two above.
- Approximate and precise location (ACCESS_COARSE_LOCATION, ACCESS_FINE_LOCATION), Android 11 and older only: Android requires it to scan for Bluetooth devices on those versions. The app does not read or store your location.
- Foreground service (FOREGROUND_SERVICE, FOREGROUND_SERVICE_CONNECTED_DEVICE): keeps the Bluetooth connection to the BMS while the app is in the background, in two cases. (1) By default ("Always connected" off): if a live reading is running when you leave the app, the connection is kept for a grace period of about 60 seconds, then the app closes the connection and the service stops. (2) With "Always connected" on: the connection is kept until you turn the setting off, tap Disconnect in the notification, or tap Stop in the app.
- Notifications (POST_NOTIFICATIONS): used only for the notification of that foreground service. It shows the battery charge percentage and power, and can be visible on the lock screen. If you deny the notification permission, the connection is still kept, but without a visible notice. The app sends no other notifications; alerts appear only inside the app.
- Wake lock (WAKE_LOCK): one partial wake lock, held for at most 75 seconds. It covers the 60-second background grace period, releasing the Bluetooth link and one reconnect cycle. It is held even when "Always connected" is off.

The app uses Android's link feature only to open the system settings page of the app.

## 4. What is stored on your device

Everything is stored locally in the app's private storage (AsyncStorage):

- Saved batteries (up to 10), each with an opaque identifier (which may be the Bluetooth address, never shown) and a nickname you choose; the pinned battery.
- Language, theme (auto, dark or light), alert thresholds and the "Always connected" setting.
- The last reading of each battery.
- Reading history per battery: SOC, voltage, current, power, cell difference, minimum and maximum cell voltage and maximum temperature. Kept per minute, then grouped into 15-minute intervals after 48 hours, for up to 30 days, capped at about 2.5 MB.

The data is not encrypted by the app at rest; it relies on Android's app-private storage. Automatic Android backup (cloud and device-to-device transfer) is disabled for the app.

## 5. Export and sharing

- The developer receives no data.
- On the History screen you can export a CSV file through the Android share sheet. This happens only when you tap export. The app creates a temporary file for sharing. The file contains UTC timestamps and the readings only, with no battery identifier, nickname or Bluetooth address.
- By itself, the app sends the CSV nowhere. You choose the destination app, and from then on that app's own privacy policy applies.
- The app does not sell data or share it with third parties by itself.

## 6. Retention and deletion

- History is kept for at most 30 days and capped at about 2.5 MB.
- "Erase history of this battery" deletes only the history of that battery.
- The app has no function to remove a saved battery. To remove saved batteries, identifiers, nicknames, last readings and settings, clear the app data in Android settings or uninstall the app.
- Because data stays on your device, the developer has no access to it and cannot fulfil deletion requests for it; you delete it as described above.
- A CSV you exported is a separate file outside the app; delete it yourself where you saved or sent it.

## 7. Children

The app is not directed at children and does not knowingly process children's data.

## 8. Changes

Changes to this policy will be published on this page with a new effective date.

## 9. Contact

alan.perius.mv@gmail.com

---
