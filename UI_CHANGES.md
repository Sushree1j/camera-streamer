# USB Connection Feature - UI Changes

## Visual Overview of the New USB Connection Feature

This document provides a text-based description of the UI changes for the USB connection feature.

---

## 🎨 Connection Settings Card (Updated)

### Before (WiFi Only):
```
┌─────────────────────────────────────────┐
│ Connection Settings                     │
│                                         │
│ [IP Address Field    ] [Port Field]    │
│                                         │
└─────────────────────────────────────────┘
```

### After (With USB Option):
```
┌─────────────────────────────────────────┐
│ Connection Settings                     │
│                                         │
│ [Connection Mode: 📡 WiFi      ▼]      │
│                                         │
│ [IP Address Field    ] [Port Field]    │
│                                         │
└─────────────────────────────────────────┘
```

---

## 📡 WiFi Mode (Default)

When WiFi is selected:
```
┌─────────────────────────────────────────┐
│ Connection Settings                     │
│                                         │
│ [Connection Mode: 📡 WiFi      ▼]      │
│                                         │
│ [192.168.1.10        ] [5000      ]    │
│  ✏️ IP can be edited    ✏️ Port editable │
│                                         │
└─────────────────────────────────────────┘

USB Info Card: HIDDEN ❌
```

---

## 🔌 USB Mode

When USB is selected:
```
┌─────────────────────────────────────────┐
│ Connection Settings                     │
│                                         │
│ [Connection Mode: 🔌 USB       ▼]      │
│                                         │
│ ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓ │
│ ┃ ⚠️  USB mode requires ADB setup.    ┃ │
│ ┃     See instructions below.         ┃ │
│ ┃                                     ┃ │
│ ┃ USB Connection Setup:               ┃ │
│ ┃ 1. Enable USB Debugging on phone   ┃ │
│ ┃ 2. Connect phone to PC via USB     ┃ │
│ ┃ 3. Run: adb forward tcp:5000       ┃ │
│ ┃         tcp:5000                    ┃ │
│ ┃ 4. Start streaming                 ┃ │
│ ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛ │
│   (Orange/Yellow warning card)          │
│                                         │
│ [127.0.0.1           ] [5000      ]    │
│  🔒 IP locked (grayed) ✏️ Port editable │
│                                         │
└─────────────────────────────────────────┘

USB Info Card: VISIBLE ✅
IP Field: DISABLED (auto-set to 127.0.0.1)
```

---

## 🎯 Connection Mode Dropdown

When user taps the dropdown:
```
┌─────────────────────────────┐
│ [Connection Mode: WiFi  ▼]  │
└─────────────────────────────┘
            ↓
┌─────────────────────────────┐
│ 📡 WiFi                     │ ← Currently selected
│ 🔌 USB                      │
└─────────────────────────────┘
```

---

## 🎬 Complete Screen Layout

### Full App Screen with USB Mode Selected:
```
╔═════════════════════════════════════════╗
║  📹 Camera Streamer Pro                 ║
║  Stream your camera feed                ║
╚═════════════════════════════════════════╝

┌─────────────────────────────────────────┐
│ Connection Settings                     │
│                                         │
│ [Connection Mode: 🔌 USB       ▼]      │
│                                         │
│ ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓ │
│ ┃ ⚠️  USB mode requires ADB setup    ┃ │
│ ┃ USB Connection Setup:               ┃ │
│ ┃ 1. Enable USB Debugging             ┃ │
│ ┃ 2. Connect via USB                  ┃ │
│ ┃ 3. Run: adb forward tcp:5000...    ┃ │
│ ┃ 4. Start streaming                  ┃ │
│ ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛ │
│                                         │
│ [127.0.0.1           ] [5000      ]    │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│ Camera Settings                         │
│                                         │
│ [📷 Rear] [🤳 Front]                    │
│                                         │
│ [Resolution: 📺 Medium (1280x720)  ▼]  │
│ [Quality: ⚡ Balanced (80%)          ▼]  │
│ [Camera Name: Front Camera        ]    │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│                                         │
│         [Camera Preview Area]           │
│                                         │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│      ▶️  Start Streaming                 │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│ 🟢 Ready to stream                      │
└─────────────────────────────────────────┘
```

---

## 🔄 State Changes

### When Switching WiFi → USB:
1. Connection Mode changes to "🔌 USB"
2. USB Info Card **appears** (slides in or fades in)
3. IP Address changes from WiFi IP to "127.0.0.1"
4. IP Address field becomes **grayed out** (disabled)

### When Switching USB → WiFi:
1. Connection Mode changes to "📡 WiFi"
2. USB Info Card **disappears** (slides out or fades out)
3. IP Address changes from "127.0.0.1" to WiFi IP
4. IP Address field becomes **active** (enabled, white background)

---

## 🎨 Color Scheme

### USB Info Card:
- **Background**: `#FFF3E0` (Light Orange/Yellow - warning color)
- **Title Text**: `#E65100` (Dark Orange - bold)
- **Body Text**: `#BF360C` (Red-Brown - monospace font)
- **Border Radius**: 8dp
- **Elevation**: 0dp (flat design)

### Connection Mode Icons:
- **WiFi**: 📡 (Signal waves emoji)
- **USB**: 🔌 (Plug emoji)

### Status Indicators:
- **Connected**: 🟢 Green indicator
- **Disconnected**: 🔴 Red indicator
- **Connecting**: 🟡 Yellow indicator

---

## 📐 Layout Specifications

### Connection Mode Dropdown:
- **Width**: Match parent
- **Height**: Wrap content
- **Margins**: 12dp bottom
- **Corner Radius**: 12dp
- **Icon**: Settings/preferences icon
- **Style**: Material Outlined Dropdown

### USB Info Card:
- **Width**: Match parent
- **Height**: Wrap content
- **Margins**: 12dp bottom
- **Padding**: 12dp all sides
- **Visibility**: `GONE` by default, `VISIBLE` in USB mode

### IP Address Field:
- **State (WiFi)**: Enabled, editable, white background
- **State (USB)**: Disabled, read-only, grayed background
- **Text Color (Disabled)**: Light gray (#9E9E9E)

---

## 🔀 User Flow Diagram

```
App Launch
    ↓
WiFi Mode (Default)
    ↓
User taps Connection Mode
    ↓
Dropdown shows: WiFi, USB
    ↓
User selects USB
    ↓
┌─────────────────────────┐
│ UI Updates:             │
│ 1. Show USB card        │
│ 2. Set IP to 127.0.0.1  │
│ 3. Disable IP field     │
└─────────────────────────┘
    ↓
User reads instructions
    ↓
User sets up ADB forwarding
    ↓
User taps "Start Streaming"
    ↓
Connection established!
```

---

## ✅ Accessibility Features

- **Large Touch Targets**: All interactive elements are at least 48dp tall
- **Clear Labels**: All fields have descriptive labels
- **Color Contrast**: Warning card has high contrast for visibility
- **Disabled State**: Clear visual indication when IP field is disabled
- **Instructions**: In-app guidance for USB setup

---

## 📱 Responsive Design

The UI adapts to different screen sizes:
- **Small Screens**: Scrollable layout ensures all content is accessible
- **Large Screens**: Content is centered and properly spaced
- **Landscape**: Layout adjusts appropriately

---

## 🎭 Animation Suggestions (Future Enhancement)

- USB Info Card: Fade in/out or slide down/up when mode changes
- IP Field: Smooth transition when enabling/disabling
- Connection Mode: Ripple effect on selection

---

This text-based UI description helps visualize the changes without needing actual screenshots. The actual implementation follows Material Design 3 guidelines with smooth transitions and modern styling.

**Note**: For actual screenshots of the implemented UI, build and run the app on an Android device or emulator.
