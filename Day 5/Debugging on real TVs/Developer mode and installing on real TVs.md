# Developer Mode and Installing on Real TVs

Every TV platform locks down app installation by default. You first enable a **developer mode** that lets your computer push builds to the TV. Each platform does this differently.

## Summary

| Platform | Enable developer mode | Connect and install |
|---|---|---|
| Android TV | Build tap + Developer options | ADB from your computer |
| Apple TV | Pair in Xcode | Run from Xcode |
| Samsung (Tizen) | Developer Mode dialog | Tizen Studio Device Manager |
| LG (webOS) | Developer Mode app | Dev Mode and Key Server |

## Per-Platform Setup

### Android TV

1. On the TV, go to **Settings → Device Preferences → About** and tap **Build** 7 times.
2. Open **Developer options** and enable **USB debugging** or **Network/ADB debugging**.
3. Connect from your Fedora machine:


### Apple TV

1. Pair the Apple TV in Xcode under **Window → Devices and Simulators**.
2. Sign the app with an Apple Developer team.
3. Run from Xcode.

### Samsung (Tizen)

1. On the TV, open the **Apps** panel and type `12345` to get the Developer Mode dialog.
2. Turn it on and enter your computer's IP.
3. Use **Tizen Studio's Device Manager** to connect, then install the `.wgt` package.

### LG (webOS)

1. Install the **Developer Mode** app from the LG Content Store and log in with an LG developer account.
2. Turn on **Dev Mode** and the **Key Server**.
