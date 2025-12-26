# Apple Watch Implementation Guide

## 1. Project Updated Automatically
I have effectively modified the `TimeCube.xcodeproj` to include the **TimeCubeWatch** target.

## 2. Verification
1. Open `TimeCube.xcodeproj` in Xcode.
2. You should see a new scheme **TimeCubeWatch**.
3. Select the **TimeCubeWatch** scheme.
4. Select a **Apple Watch Simulator** (e.g., Apple Watch Series 11).
5. Click **Run** (Cmd + R).

## 3. Data Sync Check (Dual-Mode)

The Watch App uses **two synchronization mechanisms**:

### CloudKit (Primary - Real Devices)
- The Watch App is pre-configured to use the same CloudKit container as the iOS App (`iCloud.com.ChildEducation.TimeCube`).
- Ensure you are signed into the same iCloud account on both devices.
- This is the "source of truth" for data.

### WatchConnectivity (Secondary - Real-Time & Simulator)
- Provides instant data sync between iOS and Watch.
- Works in **Simulator** where CloudKit doesn't function properly.
- iOS app sends task updates to Watch automatically.
- Watch requests fresh data when app appears.

**Files:**
- iOS: `Shared/Managers/WatchConnectivityManager.swift`
- Watch: `Managers/WatchSessionManager.swift`

## 4. Simulator Pairing (IMPORTANT!)

For WatchConnectivity to work in the Simulator:

1. **Launch the iPhone Simulator first**
2. **Open "Window" → "Devices and Simulators" (Cmd + Shift + 2)**
3. **Check that the Watch Simulator is paired with the iPhone Simulator**
   - In the Watch Simulator device, under "Paired iPhone" it should show your iPhone Simulator
4. **Run BOTH apps simultaneously**:
   - Run `TimeCube` scheme on an iPhone Simulator
   - Run `TimeCubeWatch` scheme on the paired Watch Simulator
5. **Wait for connection** - Look for these logs:
   - iOS: `[WatchSync] Session activated with state: 2`
   - Watch: `[WatchSession] Session activated with state: 2`
   
## 5. Troubleshooting
- If you see "Missing File" errors: The script force-linked shared files. Verify `TimeCube/Shared` files are correct in the Xcode file inspector.
- **Entitlements**: Check `TimeCubeWatch.entitlements` in the project settings if CloudKit errors occur.
- **"WCSession has not been activated"**: Make sure both apps are running.
- **"Phone not reachable"**: The iPhone Simulator may not be running, or they aren't paired.

## 6. Validate
1. Select the `TimeCubeWatch` scheme in Xcode toolbar.
2. Run on a Watch Simulator (paired with iPhone Simulator).
3. You should see the Dashboard with task progress.
4. Add/complete tasks on iPhone → Watch should update via WatchConnectivity.

## 7. Console Log Debugging
Look for these key logs:
- `[WatchSync]` - iOS side WatchConnectivity
- `[WatchSession]` - Watch side WatchSession
- `[Watch]` - General Watch app logs

