# USB Connection Setup Guide

## Quick Start for USB Streaming

This guide will help you set up USB streaming between your Android device and PC for smooth, reliable camera streaming.

## Prerequisites

- Android device with USB debugging enabled
- USB cable
- ADB (Android Debug Bridge) installed on your PC
- Desktop listener application running

## Step-by-Step Setup

### 1. Enable USB Debugging on Android

1. Open **Settings** on your Android device
2. Scroll down to **About Phone** (or **About Device**)
3. Find **Build Number** and tap it **7 times**
   - You should see "You are now a developer!"
4. Go back to Settings → **Developer Options**
5. Enable **USB Debugging**
6. If prompted, allow USB debugging when you connect your device

### 2. Install ADB on Your Computer

#### Windows:
```bash
# Download Android SDK Platform Tools from:
# https://developer.android.com/studio/releases/platform-tools

# Extract the zip file
# Add the platform-tools folder to your PATH environment variable
# Or navigate to the folder in Command Prompt/PowerShell
```

#### Linux:
```bash
sudo apt-get update
sudo apt-get install adb
```

#### macOS:
```bash
# Using Homebrew
brew install android-platform-tools
```

### 3. Connect Your Device

1. Connect your Android device to your PC using a USB cable
2. On your Android device, you may see a popup asking to "Allow USB debugging"
3. Check "Always allow from this computer" and tap **Allow**

### 4. Verify Connection

```bash
# Check if your device is connected
adb devices

# You should see output like:
# List of devices attached
# ABC123XYZ    device
```

If you see "unauthorized", go back to step 3 and allow USB debugging.

### 5. Set Up Port Forwarding

```bash
# Forward port 5000 from your PC to your Android device
adb forward tcp:5000 tcp:5000

# You can verify active forwards with:
adb forward --list
```

### 6. Start the Desktop Listener

```bash
cd desktop-listener
python main.py

# Or specify custom host/port:
# python main.py --host 0.0.0.0 --port 5000
```

### 7. Configure the Android App

1. Open **Camera Streamer Pro** on your Android device
2. In **Connection Mode**, select **🔌 USB**
3. The IP address will automatically be set to `127.0.0.1`
4. Keep the port as `5000` (or match your port forwarding)
5. Configure camera settings (camera facing, resolution, quality)
6. Tap **Start Streaming**

You should now see your camera feed on the desktop application!

## Advantages of USB Connection

✅ **No WiFi Required** - Works without any network connection  
✅ **More Stable** - Eliminates WiFi interference and signal issues  
✅ **Lower Latency** - Faster data transfer through direct USB connection  
✅ **Better Quality** - No WiFi bandwidth limitations  
✅ **Reliable** - Perfect for presentations, monitoring, or demo scenarios  

## Troubleshooting

### Device Not Found
```bash
# Kill and restart ADB server
adb kill-server
adb start-server
adb devices
```

### Connection Refused
1. Make sure port forwarding is active: `adb forward --list`
2. Restart port forwarding: 
   ```bash
   adb forward --remove-all
   adb forward tcp:5000 tcp:5000
   ```
3. Ensure desktop listener is running before starting the Android app

### "Unauthorized" Device
1. Disconnect and reconnect the USB cable
2. Revoke USB debugging authorizations in Developer Options
3. Re-enable USB debugging and reconnect
4. Allow the authorization popup on your device

### Stream Not Appearing
1. Check that the desktop listener is running
2. Verify port forwarding: `adb forward --list`
3. Try stopping and restarting the stream in the Android app
4. Check the status message in the Android app for connection details

### Multiple Devices
If you have multiple Android devices connected:
```bash
# List all devices
adb devices

# Target a specific device for port forwarding
adb -s DEVICE_ID forward tcp:5000 tcp:5000

# Example:
adb -s ABC123XYZ forward tcp:5000 tcp:5000
```

For multiple device streaming, use different ports:
```bash
# Device 1
adb -s DEVICE1_ID forward tcp:5000 tcp:5000

# Device 2
adb -s DEVICE2_ID forward tcp:5001 tcp:5001
```

## Switching Back to WiFi

To switch back to WiFi mode:
1. Open the app
2. Select **📡 WiFi** in Connection Mode
3. Enter your desktop's IP address
4. Enter the port (default: 5000)
5. Start streaming

The WiFi functionality remains completely unchanged and available at any time.

## Tips for Best Performance

1. **Use USB 3.0 ports** when available for better bandwidth
2. **Use a high-quality USB cable** to avoid connection issues
3. **Disable battery optimization** for the Camera Streamer app in Android settings
4. **Keep the screen on** during streaming for best performance
5. **Close other apps** that might use the camera

## Additional Resources

- Main README: [README.md](README.md)
- GitHub Issues: [Report a Problem](https://github.com/Sushree1j/camera-streamer/issues)
- Android Developer Options Guide: [Android Documentation](https://developer.android.com/studio/debug/dev-options)

---

**Happy Streaming! 🎥📱🔌**
