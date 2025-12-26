# Apple Watch Implementation Guide

## 1. Project Updated Automatically
I have effectively modified the `TimeCube.xcodeproj` to include the **TimeCubeWatch** target.

## 2. Verification
1. Open `TimeCube.xcodeproj` in Xcode.
2. You should see a new scheme **TimeCubeWatch**.
3. Select the **TimeCubeWatch** scheme.
4. Select a **Apple Watch Simulator** (e.g., Apple Watch Series 9).
5. Click **Run** (Cmd + R).

## 3. Data Sync Check
The Watch App is pre-configured to use the same CloudKit container as the iOS App (`iCloud.com.ChildEducation.TimeCube`).
- Ensure you are signed into the same iCloud account on both Simulator (Phone and Watch).
- If tasks do not appear immediately, trigger a generic save (add a task on phone) to push a change.

## 4. Troubleshooting
- If you see "Missing File" errors: The script force-linked shared files. Verfiy `TimeCube/Shared` files are correct in the Xcode file inspector.
- **Entitlements**: Check `TimeCubeWatch.entitlements` in the project settings if CloudKit errors occur.

## 5. Validate
1. Select the `TimeCubeWatch` scheme in Xcode toolbar.
2. Run on a Watch Simulator.
3. You should see the Dashboard.
