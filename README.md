# Uninstall Admin policy apps on Android
I recently come through a situation where my friend wants to uninstall an app that blocks nudity content, 
app : https://play.google.com/store/apps/details?id=com.blockerhero

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

---

My friend never Uninstalled that app since he payed for that.
