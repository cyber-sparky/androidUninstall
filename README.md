# Uninstall Admin policy apps on Android
I recently come through a situation where my friend wants to uninstall an app that blocks nudity content, 
app : https://play.google.com/store/apps/details?id=com.blockerhero

Turn on this Settings in Developer Mode:

- **USB Debugging**
    - Allows `adb shell`, install/uninstall, `dpm` commands, etc.
- **Wireless Debugging**
    - If you want to connect over Wi-Fi instead of USB.
- **Install via USB** (MIUI setting)
    - Lets you push APKs with `adb install` without extra prompts.
- **USB Debugging (Security settings)**
    - Prompts you to authorize your host computer for sensitive operations (you’ll need to confirm the RSA fingerprint).
- **OEM Unlocking**
    - Required if you ever want to unlock the bootloader to install a custom recovery or push your app as a system APK.
    - **Warning:** unlocking the bootloader will wipe user data!

# METHOD #1 - ADB

Normal Uninstallation

```bash
adb devices
adb shell
pm list packages | grep app #find the package name of the app
pm uninstall package:com.blockerhero # To uninstall a user app
```

If the above uninstallation didnt work

```bash
pm uninstall --user 0 com.blockerhero # To remove a system app for user 0
```

If Device Policy Manager (DPM) app or Device Admin is enabled ?

```bash
$dumpsys device_policy | blockerhero # app name
com.blockerhero/.MyDeviceAdminReceiver. # receiver name

dpm remove-active-admin com.blockerhero/.DeviceAdminReceiver # remove policy
pm uninstall --user 0 com.blockerhero # remove app
```

If nothing work go for METHOD #2

---

# METHOD #2

- Go to Safe Mode in Your phone
- Go to Setting > Apps > blockerhero > Remove admin access > Uninstall app
- Reboot - You’ll be come to Normal Mode

When you granted BlockerHero “Device admin” access, Android created a set of policies in its DevicePolicyManager (stored in `/data/system/device_policies.xml`) that prevent normal users (and even Safe Mode) from removing or disabling the app’s admin component.  What you did in Safe Mode was:

1. Safe Mode temporarily disabled *all third-party apps*, so you could go into Settings → Device admin apps and toggle BlockerHero **off**.
2. Once its admin bit was turned off, you could uninstall it normally.
---

My friend never Uninstalled that app since he payed for that.
