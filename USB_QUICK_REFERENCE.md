# USB Connection Quick Reference

## 🚀 Quick Setup (5 Steps)

### 1️⃣ Enable USB Debugging
```
Settings → About Phone → Tap "Build Number" 7x → Back → Developer Options → Enable "USB Debugging"
```

### 2️⃣ Install ADB
**Windows:** Download [SDK Platform Tools](https://developer.android.com/studio/releases/platform-tools)  
**Linux:** `sudo apt-get install adb`  
**Mac:** `brew install android-platform-tools`

### 3️⃣ Connect & Forward
```bash
# Connect phone via USB
adb devices              # Verify connection
adb forward tcp:5000 tcp:5000
```

### 4️⃣ Start Desktop
```bash
cd desktop-listener
python main.py
```

### 5️⃣ Configure App
```
Open App → Connection Mode: 🔌 USB → Start Streaming
```

---

## 🔧 Common Commands

### Check Connection
```bash
adb devices
```

### Set Up Port Forwarding
```bash
adb forward tcp:5000 tcp:5000
```

### Check Active Forwards
```bash
adb forward --list
```

### Remove All Forwards
```bash
adb forward --remove-all
```

### Restart ADB
```bash
adb kill-server
adb start-server
```

---

## 🆚 WiFi vs USB

| Feature | WiFi Mode | USB Mode |
|---------|-----------|----------|
| **Setup** | Easy | Requires ADB |
| **Stability** | Depends on WiFi | Very Stable |
| **Latency** | Higher | Lower |
| **Requirements** | Same network | USB cable + ADB |
| **Best For** | Convenience | Performance |

---

## ⚠️ Troubleshooting

### "Unauthorized" Device
```bash
# Allow USB debugging popup on phone, then:
adb kill-server
adb start-server
```

### Connection Failed
```bash
# Check port forwarding:
adb forward --list

# If empty, set it up:
adb forward tcp:5000 tcp:5000
```

### Can't Find Device
```bash
# Restart ADB:
adb kill-server
adb start-server
adb devices
```

---

## 📱 Multiple Devices

```bash
# List all devices
adb devices

# Forward for specific device
adb -s DEVICE_ID forward tcp:5000 tcp:5000

# Use different ports for multiple devices
adb -s DEVICE_1 forward tcp:5000 tcp:5000
adb -s DEVICE_2 forward tcp:5001 tcp:5001
```

---

## 💡 Pro Tips

✅ **Use USB 3.0** ports for best performance  
✅ **Disable battery optimization** for the app  
✅ **Keep screen on** during streaming  
✅ **Use quality USB cable** to avoid disconnects  
✅ **Close background apps** for better performance  

---

## 📚 More Info

- Full Setup Guide: [USB_SETUP_GUIDE.md](USB_SETUP_GUIDE.md)
- Main Documentation: [README.md](README.md)
- Report Issues: [GitHub Issues](https://github.com/Sushree1j/camera-streamer/issues)

---

**Need Help?** Check the [USB Setup Guide](USB_SETUP_GUIDE.md) for detailed instructions! 📖
