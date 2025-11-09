# Camera Streamer Pro 📹

A modern, feature-rich Android application that streams your device's camera feed to a desktop application in real-time with advanced controls and multi-camera support. Perfect for remote monitoring, presentations, or computer vision applications.

## ✨ Features

### 🎥 Core Streaming
- **Real-time Camera Streaming**: Stream live camera feed from your Android device
- **Multiple Connection Methods**: WiFi or USB connection options
- **Multiple Camera Support**: Connect and stream from multiple Android devices simultaneously
- **Dual Camera Support**: Choose between front and rear cameras
- **Multiple Resolution Options**: Low (640x480), Medium (1280x720), High (1920x1080)
- **Adjustable Quality Settings**: Battery Saver (60%), Balanced (80%), High Quality (95%)

### 🎛️ Advanced Controls
- **Camera Controls** (Android to Desktop):
  - Digital Zoom: 1x to 10x magnification
  - Exposure Compensation: -12 to +12 adjustment
  - Manual Focus: Fine-tune focus distance
  
- **Image Processing** (Desktop-side):
  - Brightness: 0.0 to 2.0 adjustment
  - Contrast: 0.0 to 2.0 adjustment
  - Saturation: 0.0 to 2.0 adjustment
  - Video Filters: Grayscale, Blur, Sharpen, Edge Enhance

### 🎨 Enhanced UI/UX
- **Modern Material Design 3**: Beautiful, intuitive interface on Android
- **Multi-Camera Management**: Add and switch between multiple camera streams
- **Real-time Statistics**: FPS, latency, and connection status
- **Camera Identification**: Custom camera naming for easy identification
- **Responsive Layout**: Optimized for various screen sizes

## 🏗️ Architecture

This project consists of two main components:

### Android Client (`android-client/`)
- Built with Kotlin and Android Camera2 API
- Material Design 3 UI with modern card-based interface
- Supports both front and rear camera streaming
- Configurable resolution, quality, and network settings
- Real-time camera control via bidirectional communication

### Desktop Listener (`desktop-listener/`)
- Python-based desktop application using Tkinter
- Multi-camera stream management
- Advanced image processing with PIL/Pillow
- Real-time control commands to Android client
- Modern, responsive UI with tooltips and visual feedback

## 🚀 Quick Start

### Prerequisites

- **Android**: Minimum SDK 26 (Android 8.0)
- **Java**: JDK 17 or higher
- **Android SDK**: API level 34
- **Python**: 3.8+ (for desktop listener)
- **Pillow**: 10.0.0+ (Python imaging library)

### Building the Android App

1. **Clone the repository:**
   ```bash
   git clone https://github.com/Sushree1j/camera-streamer.git
   cd camera-streamer
   ```

2. **Set up Android SDK:**
   - Download and install Android SDK
   - Set `ANDROID_HOME` environment variable
   - Ensure `build-tools` and `platforms` are installed

3. **Build the app:**
   ```bash
   cd android-client
   ./gradlew build
   ```

4. **Install on device:**
   - Transfer `app/build/outputs/apk/debug/app-debug.apk` to your Android device
   - Install the APK (you may need to enable "Install unknown apps")

### Running the Desktop Listener

1. **Install dependencies:**
   ```bash
   cd desktop-listener
   pip install -r requirements.txt
   ```

2. **Run the listener:**
   ```bash
   python main.py
   ```
   
   Or specify custom host/port:
   ```bash
   python main.py --host 0.0.0.0 --port 5000
   ```

## 📱 Usage

### WiFi Connection

1. **Launch the app** on your Android device
2. **Select WiFi mode** in Connection Mode dropdown
3. **Configure camera:**
   - Give your camera a custom name (e.g., "Front Camera", "Rear Camera")
   - Select camera facing (front or rear)
   - Choose resolution based on your needs (Low/Medium/High)
   - Select quality setting (Battery Saver/Balanced/High Quality)
4. **Enter connection details:**
   - IP address of your desktop computer running the listener
   - Port number (default: 5000)
5. **Start streaming** by tapping the "Start Streaming" button

### USB Connection (Android Only)

For smoother, more reliable streaming when both devices are physically connected:

**📖 For detailed USB setup instructions, see [USB_SETUP_GUIDE.md](USB_SETUP_GUIDE.md)**

**Quick Setup:**

1. **Enable USB Debugging** on your Android device:
   - Go to Settings → About Phone
   - Tap "Build Number" 7 times to enable Developer Options
   - Go to Settings → Developer Options
   - Enable "USB Debugging"

2. **Connect your phone to PC** via USB cable

3. **Set up ADB port forwarding** on your PC:
   ```bash
   # Install ADB if not already installed
   # Windows: Download Android SDK Platform Tools
   # Linux: sudo apt-get install adb
   # Mac: brew install android-platform-tools
   
   # Set up port forwarding
   adb forward tcp:5000 tcp:5000
   ```

4. **Start the desktop listener** on your computer:
   ```bash
   cd desktop-listener
   python main.py
   ```

5. **Configure the Android app**:
   - Launch the app
   - Select "🔌 USB" in Connection Mode dropdown
   - The IP will automatically be set to 127.0.0.1 (localhost)
   - Keep port as 5000
   - Configure camera settings as needed
   - Tap "Start Streaming"

**Advantages of USB Connection:**
- No WiFi network required
- More stable connection
- Lower latency
- Better for locations with poor WiFi
- Ideal for live presentations or monitoring

### Android App Setup

### Desktop Listener Features

1. **View live stream** from connected camera
2. **Add multiple cameras:**
   - Click "➕ Add Camera" to add another camera stream
   - Each camera can run on a different port
3. **Switch between cameras:**
   - Use the "Active Camera" dropdown to switch views
4. **Adjust camera settings** (sent to Android device):
   - Zoom: 1x to 10x digital zoom
   - Exposure: -12 to +12 compensation
   - Focus: Manual focus control (0.0 to 1.0)
5. **Apply image processing** (desktop-side):
   - Brightness: Adjust image brightness (0.0 to 2.0)
   - Contrast: Adjust image contrast (0.0 to 2.0)
   - Saturation: Adjust color saturation (0.0 to 2.0)
   - Filters: Apply visual effects (Grayscale, Blur, Sharpen, Edge Enhance)
6. **Monitor performance:**
   - Real-time FPS counter
   - Network latency display
   - Connection status indicator

## 🔧 Configuration

### Connection Mode
- **WiFi Mode**: Connect over local network (both devices must be on same network)
- **USB Mode**: Connect via USB cable with ADB port forwarding (requires USB debugging enabled)

### Network Settings
- **IP Address**: 
  - WiFi mode: Enter the IP address of the machine running the desktop listener
  - USB mode: Automatically set to 127.0.0.1 (localhost)
- **Port**: Specify the port number for streaming (must match desktop listener, default: 5000)

### Camera Settings
- **Camera Selection**: Toggle between front and rear cameras
- **Camera Naming**: Give each camera a custom identifier
- **Resolution**: Choose appropriate resolution based on network speed and quality needs
- **Quality Settings**: Balance between battery life and image quality

### Stream Control Settings
- **Zoom**: Digital zoom from 1x to 10x (Android-side)
- **Exposure**: Compensation from -12 to +12 (Android-side)
- **Focus**: Manual focus control from 0.0 (infinity) to 1.0 (closest) (Android-side)
- **Brightness**: Desktop-side brightness adjustment (0.0 to 2.0)
- **Contrast**: Desktop-side contrast adjustment (0.0 to 2.0)
- **Saturation**: Desktop-side saturation adjustment (0.0 to 2.0)
- **Filters**: Apply real-time video effects on desktop

### Multi-Camera Setup
1. **Start the desktop listener** on your computer (default port 5000)
2. **Add additional cameras**:
   - Click "➕ Add Camera" in the desktop app
   - Enter camera name, host (0.0.0.0), and port (e.g., 5001, 5002)
   - Click "Add"
3. **Configure each Android device**:
   - Set unique camera name on each device
   - Use desktop IP and respective port (5000, 5001, 5002, etc.)
   - Start streaming from each device
4. **Switch between cameras** using the dropdown in desktop app

## 🛠️ Development

### Android Development Setup

1. **Import project** in Android Studio
2. **Sync Gradle** files
3. **Run on device/emulator**

### Desktop Development Setup

1. **Create virtual environment** (recommended):
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```
2. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```
3. **Run the application**:
   ```bash
   python main.py
   ```

### Key Technologies Used

#### Android
- **Kotlin**: Primary programming language
- **Android Camera2 API**: Low-level camera access and streaming
- **Material Design 3**: Modern UI components
- **ConstraintLayout**: Responsive layouts
- **Coroutines**: Asynchronous operations
- **JSON**: Camera metadata transmission

#### Desktop
- **Python 3**: Core application language
- **Tkinter**: GUI framework
- **Pillow (PIL)**: Image processing library
- **Threading**: Concurrent frame processing
- **Socket Programming**: Network communication

### Project Structure

```
android-client/
├── app/
│   ├── src/main/
│   │   ├── java/com/example/chessassiststreamer/
│   │   │   └── MainActivity.kt          # Main activity with camera logic
│   │   ├── res/                         # Resources
│   │   │   ├── drawable/                # Icons and graphics
│   │   │   ├── layout/                  # UI layouts
│   │   │   ├── values/                  # Colors, strings, themes
│   │   │   └── xml/                     # Configuration files
│   │   └── AndroidManifest.xml          # App manifest
│   └── build.gradle                     # App build configuration
├── build.gradle                         # Project build configuration
├── gradle.properties                    # Gradle properties
└── settings.gradle                      # Project settings

desktop-listener/
├── main.py                              # Desktop streaming receiver
└── requirements.txt                     # Python dependencies
```

## 📋 Requirements

### Android App
- **Min SDK**: 26 (Android 8.0)
- **Target SDK**: 34 (Android 14)
- **Permissions**:
  - `CAMERA`: For camera access
  - `INTERNET`: For network streaming
  - `ACCESS_WIFI_STATE`: For WiFi information
  - `ACCESS_NETWORK_STATE`: For network state

### Desktop Listener
- **Python**: 3.8 or higher
- **Libraries**: See `desktop-listener/requirements.txt`

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🐛 Issues & Support

- **Bug Reports**: [GitHub Issues](https://github.com/Sushree1j/camera-streamer/issues)
- **Feature Requests**: [GitHub Issues](https://github.com/Sushree1j/camera-streamer/issues)
- **Discussions**: [GitHub Discussions](https://github.com/Sushree1j/camera-streamer/discussions)

## 🔧 Troubleshooting

### USB Connection Issues

1. **"Connection failed" error in USB mode:**
   - Verify USB debugging is enabled on your Android device
   - Check that ADB is properly installed: `adb version`
   - Confirm device is connected: `adb devices`
   - Ensure port forwarding is set up: `adb forward tcp:5000 tcp:5000`
   - Check that desktop listener is running before starting Android app

2. **ADB not recognized:**
   - Windows: Add Android SDK platform-tools to your PATH
   - Linux: Install via package manager: `sudo apt-get install adb`
   - Mac: Install via Homebrew: `brew install android-platform-tools`

3. **Device unauthorized in adb devices:**
   - A popup should appear on your Android device
   - Tap "Allow" to authorize USB debugging
   - If popup doesn't appear, try: `adb kill-server` then `adb start-server`

4. **Stream works on WiFi but not USB:**
   - Restart ADB: `adb kill-server && adb start-server`
   - Remove and re-setup port forwarding: `adb forward --remove-all` then `adb forward tcp:5000 tcp:5000`
   - Check firewall settings on desktop computer

### WiFi Connection Issues

1. **Cannot connect to desktop:**
   - Ensure both devices are on the same network
   - Check desktop firewall allows incoming connections on the specified port
   - Verify the IP address is correct (it should be desktop's local IP)

2. **Stream is laggy:**
   - Try lower resolution or quality settings
   - Check WiFi signal strength
   - Consider using USB mode for better performance

## 🙏 Acknowledgments

- Built with [Android Camera2 API](https://developer.android.com/reference/android/hardware/camera2/package-summary)
- UI designed with [Material Design 3](https://material.io/design)
- Icons from Android Studio and custom vector graphics

---

**Made with ❤️ for computer vision and remote monitoring applications**
