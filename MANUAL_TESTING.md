# Manual Testing Guide for USB Connection Feature

## Test Scenarios

This document outlines the manual testing scenarios to verify the USB connection feature works correctly.

## Prerequisites
- Android device with USB debugging enabled
- USB cable
- ADB installed on testing PC
- Desktop listener application

---

## Test Case 1: WiFi Mode Default Behavior

**Objective**: Verify WiFi mode is selected by default and works as before

### Steps:
1. Launch the Camera Streamer Pro app
2. Verify "Connection Mode" dropdown shows "📡 WiFi"
3. Verify IP address field shows local IP address (not 127.0.0.1)
4. Verify IP address field is enabled (can be edited)
5. Verify USB info card is NOT visible
6. Enter desktop IP and port
7. Start streaming
8. Verify connection works as expected

### Expected Results:
- ✓ WiFi mode selected by default
- ✓ IP field shows actual device IP
- ✓ IP field is editable
- ✓ USB instructions hidden
- ✓ Streaming works normally

---

## Test Case 2: Switch to USB Mode

**Objective**: Verify USB mode changes UI correctly

### Steps:
1. Launch the Camera Streamer Pro app
2. Tap on "Connection Mode" dropdown
3. Select "🔌 USB"

### Expected Results:
- ✓ USB info card becomes visible (orange/yellow background)
- ✓ USB setup instructions are displayed
- ✓ IP address field automatically changes to "127.0.0.1"
- ✓ IP address field becomes disabled (grayed out)
- ✓ Port remains "5000"

---

## Test Case 3: USB Mode Streaming

**Objective**: Verify streaming works in USB mode

### Prerequisites:
- USB debugging enabled on Android
- Phone connected via USB
- ADB port forwarding active: `adb forward tcp:5000 tcp:5000`
- Desktop listener running

### Steps:
1. Select "🔌 USB" in Connection Mode
2. Verify IP shows "127.0.0.1"
3. Configure camera settings (facing, resolution, quality)
4. Tap "Start Streaming"
5. Observe video feed on desktop

### Expected Results:
- ✓ Connection establishes successfully
- ✓ Video stream appears on desktop
- ✓ FPS counter shows reasonable frame rate
- ✓ Stream is smooth and responsive
- ✓ Camera controls work (if desktop sends control commands)

---

## Test Case 4: Switch Back to WiFi

**Objective**: Verify switching from USB to WiFi restores WiFi functionality

### Steps:
1. Start with USB mode selected
2. Stop streaming (if active)
3. Change Connection Mode to "📡 WiFi"

### Expected Results:
- ✓ USB info card disappears
- ✓ IP address field becomes editable
- ✓ If IP was "127.0.0.1", it changes to local IP
- ✓ User can edit IP address
- ✓ WiFi streaming works when configured correctly

---

## Test Case 5: Metadata Transmission

**Objective**: Verify connection type is sent in metadata

### Setup:
- Monitor desktop listener logs/output

### Steps:
1. Select USB mode
2. Start streaming
3. Check metadata received by desktop listener

### Expected Results:
- ✓ Metadata includes `"connection_type": "usb"`
- ✓ Other metadata fields present (camera_id, resolution, quality, etc.)

### Steps (WiFi):
1. Switch to WiFi mode
2. Start streaming
3. Check metadata received by desktop listener

### Expected Results:
- ✓ Metadata includes `"connection_type": "wifi"`

---

## Test Case 6: USB Mode Error Handling

**Objective**: Verify error handling when ADB forwarding is not set up

### Setup:
- Do NOT set up ADB port forwarding
- Desktop listener not running

### Steps:
1. Select USB mode
2. Tap "Start Streaming"

### Expected Results:
- ✓ App shows "Connection failed" or similar error
- ✓ App handles failure gracefully (no crash)
- ✓ User can try again after fixing setup
- ✓ Status indicator shows error state

---

## Test Case 7: Multiple Resolution/Quality Settings

**Objective**: Verify USB mode works with different settings

### Steps:
1. Select USB mode
2. Set resolution to "Low (640x480)"
3. Set quality to "Battery Saver (60%)"
4. Start streaming
5. Verify stream works
6. Stop streaming
7. Change to "High (1920x1080)" and "High Quality (95%)"
8. Start streaming again

### Expected Results:
- ✓ All resolution options work in USB mode
- ✓ All quality options work in USB mode
- ✓ Video quality reflects selected settings
- ✓ No crashes or errors

---

## Test Case 8: Camera Facing Toggle in USB Mode

**Objective**: Verify camera switching works in USB mode

### Steps:
1. Select USB mode
2. Select "Front" camera
3. Start streaming
4. Verify front camera stream appears
5. While streaming, switch to "Rear" camera
6. Verify rear camera stream appears

### Expected Results:
- ✓ Both front and rear cameras work in USB mode
- ✓ Camera switching works smoothly
- ✓ Stream restarts correctly after switch

---

## Test Case 9: UI Persistence

**Objective**: Verify selected mode persists during app lifecycle

### Steps:
1. Select USB mode
2. Minimize app (press home button)
3. Re-open app from recent apps

### Expected Results:
- ✓ USB mode is still selected
- ✓ IP still shows "127.0.0.1"
- ✓ USB info card still visible

Note: Connection state may reset (this is expected for stopped connections)

---

## Test Case 10: USB Instructions Readability

**Objective**: Verify USB setup instructions are clear and helpful

### Steps:
1. Select USB mode
2. Read the USB info card
3. Verify instructions are:
   - Clear and easy to understand
   - Properly formatted
   - Contain correct ADB command
   - Visible and not cut off

### Expected Results:
- ✓ Instructions are clear
- ✓ ADB command is visible: `adb forward tcp:5000 tcp:5000`
- ✓ Text is legible (not too small)
- ✓ Colors make it stand out (orange/yellow warning style)

---

## Performance Testing

### USB vs WiFi Latency Comparison

**Test Setup**:
1. Same device, same camera settings
2. Test WiFi mode first
3. Test USB mode second
4. Measure FPS and observe latency

**Metrics to Compare**:
- Average FPS
- Visual latency (perceived delay)
- Stream stability (dropped frames)
- Connection reliability

**Expected**:
- USB should have equal or better performance
- USB should be more stable
- USB should work without WiFi

---

## Regression Testing

### Verify No Impact on WiFi

**Objective**: Ensure USB feature doesn't break existing WiFi functionality

### Tests:
1. ✓ WiFi mode still works as before
2. ✓ Multi-camera support still works
3. ✓ Camera controls still work
4. ✓ All quality/resolution options still work
5. ✓ Desktop listener compatibility unchanged
6. ✓ No new crashes or errors in WiFi mode

---

## Edge Cases

### Test Case E1: No USB Debugging
- USB mode selected but USB debugging not enabled
- Should fail to connect gracefully

### Test Case E2: Wrong Port
- User changes port in USB mode
- ADB forward uses different port
- Should fail with clear error

### Test Case E3: Device Unplugged
- Streaming in USB mode
- User unplugs USB cable
- Should detect disconnection and show error

### Test Case E4: ADB Process Killed
- Streaming in USB mode
- Kill ADB server: `adb kill-server`
- Should lose connection, allow retry

---

## Acceptance Criteria

All of the following must pass:

- [ ] WiFi mode works exactly as before (no regression)
- [ ] USB mode can be selected and shows correct UI
- [ ] USB mode successfully streams video with proper setup
- [ ] IP address is automatically set to 127.0.0.1 in USB mode
- [ ] IP field is disabled in USB mode
- [ ] USB info card shows/hides appropriately
- [ ] Connection metadata includes connection type
- [ ] Switching between modes works smoothly
- [ ] Error handling is graceful
- [ ] No crashes or ANRs
- [ ] Documentation is clear and accurate

---

## Bug Reporting

If you find issues during testing, please report with:

1. **Test case number** that failed
2. **Steps to reproduce**
3. **Expected behavior**
4. **Actual behavior**
5. **Screenshots/logs** if available
6. **Device model and Android version**
7. **Connection mode** (WiFi or USB)

---

## Notes for Testers

- USB mode requires technical setup (ADB). This is expected.
- USB mode is Android-only (as per requirements)
- The app cannot automatically set up ADB forwarding
- Users must manually configure ADB on their computer
- Test on multiple Android devices if possible
- Test on different Android versions (API 26+)

---

**Testing Checklist Summary:**
- [ ] Test Case 1: WiFi Mode Default Behavior
- [ ] Test Case 2: Switch to USB Mode
- [ ] Test Case 3: USB Mode Streaming
- [ ] Test Case 4: Switch Back to WiFi
- [ ] Test Case 5: Metadata Transmission
- [ ] Test Case 6: USB Mode Error Handling
- [ ] Test Case 7: Multiple Resolution/Quality Settings
- [ ] Test Case 8: Camera Facing Toggle in USB Mode
- [ ] Test Case 9: UI Persistence
- [ ] Test Case 10: USB Instructions Readability
- [ ] Performance Testing
- [ ] Regression Testing
- [ ] Edge Cases (E1-E4)

---

**Happy Testing! 🧪✅**
