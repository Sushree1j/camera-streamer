# USB Connection Guide

## Overview

The Camera Streamer Pro app now supports USB streaming alongside WiFi for smoother, more reliable camera streaming. USB mode uses ADB port forwarding to stream video directly through the USB cable, eliminating network dependencies.

### Key Benefits
- **No WiFi required** - Works anywhere with a USB cable
- **Lower latency** - Faster, smoother streaming
- **More stable** - No network interference
- **Higher quality** - Full USB bandwidth available

### How It Works
USB mode connects to `127.0.0.1:5000` (localhost) on the Android device, with ADB forwarding the port to your desktop listener running on port 5000.

---

## Quick Setup (5 Steps)

### 1. Enable USB Debugging
```
Settings → About Phone → Tap "Build Number" 7x → Back → Developer Options → Enable "USB Debugging"
```

### 2. Install ADB
**Windows:** Download [SDK Platform Tools](https://developer.android.com/studio/releases/platform-tools)  
**Linux:** `sudo apt-get install adb`  
**Mac:** `brew install android-platform-tools`

### 3. Connect & Forward
```bash
adb devices              # Verify connection
adb forward tcp:5000 tcp:5000
```

### 4. Start Desktop Listener
```bash
cd desktop-listener
python main.py
```

### 5. Configure App
```
Open App → Connection Mode: 🔌 USB → Start Streaming
```

---

## Detailed Setup

### Prerequisites
- Android device (API 26+)
- USB cable
- ADB installed on PC
- Desktop listener application

### Step-by-Step Instructions

1. **Enable USB Debugging on Android**
   - Go to Settings → About Phone
   - Tap "Build Number" 7 times to enable Developer Options
   - Go to Developer Options → Enable "USB Debugging"
   - Allow USB debugging when prompted

2. **Install ADB**
   - **Windows:** Download and extract Android SDK Platform Tools, add to PATH
   - **Linux:** `sudo apt-get install adb`
   - **macOS:** `brew install android-platform-tools`

3. **Connect Device**
   - Connect Android device via USB
   - Allow USB debugging authorization on device

4. **Verify Connection**
   ```bash
   adb devices
   ```
   Should show your device as "device" (not "unauthorized")

5. **Set Up Port Forwarding**
   ```bash
   adb forward tcp:5000 tcp:5000
   ```

6. **Start Desktop Listener**
   ```bash
   cd desktop-listener
   python main.py
   ```

7. **Configure Android App**
   - Open Camera Streamer Pro
   - Select "🔌 USB" in Connection Mode
   - IP automatically sets to `127.0.0.1`
   - Tap "Start Streaming"

---

## Common Commands

```bash
# Check connection
adb devices

# Set up port forwarding
adb forward tcp:5000 tcp:5000

# Check active forwards
adb forward --list

# Remove all forwards
adb forward --remove-all

# Restart ADB
adb kill-server
adb start-server
```

---

## Troubleshooting

### Device Not Found
```bash
adb kill-server
adb start-server
adb devices
```

### "Unauthorized" Device
- Disconnect/reconnect USB cable
- Revoke USB debugging authorizations in Developer Options
- Re-enable USB debugging and allow authorization

### Connection Failed
- Verify port forwarding: `adb forward --list`
- Restart forwarding: `adb forward --remove-all && adb forward tcp:5000 tcp:5000`
- Ensure desktop listener is running

### Stream Not Appearing
- Check desktop listener is running
- Verify port forwarding is active
- Restart stream in Android app
- Check app status messages

---

## WiFi vs USB Comparison

| Feature | WiFi Mode | USB Mode |
|---------|-----------|----------|
| **Setup** | Easy | Requires ADB |
| **Stability** | Network dependent | Very stable |
| **Latency** | 50-200ms | 10-50ms |
| **Bandwidth** | WiFi speed | USB 2.0: 480 Mbps<br>USB 3.0: 5 Gbps |
| **Requirements** | Same network | USB cable + ADB |
| **Best For** | Convenience | Performance |

---

## Multiple Devices

For multiple Android devices:
```bash
# List devices
adb devices

# Forward for specific device
adb -s DEVICE_ID forward tcp:5000 tcp:5000

# Different ports for multiple devices
adb -s DEVICE1 forward tcp:5000 tcp:5000
adb -s DEVICE2 forward tcp:5001 tcp:5001
```

---

## Performance Tips

- Use USB 3.0 ports for best performance
- Use high-quality USB cable
- Disable battery optimization for the app
- Keep screen on during streaming
- Close background apps

---

## Switching Between Modes

- **To USB:** Select "🔌 USB" in Connection Mode
- **To WiFi:** Select "📡 WiFi", enter desktop IP address

WiFi functionality remains unchanged and available at any time.

---

## Technical Details

- Uses ADB port forwarding instead of USB accessories API
- Compatible with all Android devices (API 26+)
- No special permissions required
- Metadata includes `connection_type: "usb"`
- Localhost connection (127.0.0.1) for security

---

## Need More Help?

- Report issues: [GitHub Issues](https://github.com/Sushree1j/camera-streamer/issues)
- Main documentation: [README.md](README.md)

---

*Last Updated: 2025-11-09*