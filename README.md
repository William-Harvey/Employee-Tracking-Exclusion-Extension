# Employee Tracking Exclusion Extension

## Overview

This browser extension excludes internal employee activity from analytics and user behaviour tracking. It sets a cookie (`EMP_TRACKING_EXCLUSION=true`) that tools like Google Tag Manager (GTM) can use to block tracking for employees. Only employees with the extension installed will be blocked, and it will only work on the domains listed in `manifest.json`.

## How It Works

- The extension sets a cookie on specific domains.
- GTM or other analytics tools use this cookie to exclude employee data from being recorded.

## Installation

### 1. Download the Extension Files

1. Download the repository as a ZIP file and extract it.
2. The extracted folder will be called `BlockEmployeeTrackingPlugin`.

### 2. Customize the Extension

#### Modify `manifest.json`

1. Open the `BlockEmployeeTrackingPlugin` folder.
2. Open the `manifest.json` file in a text editor.
3. **If you have one domain**: Update both the `host_permissions` and `matches` fields as follows:
```
"host_permissions": ["://.yourcompanydomain.com/" ]
```
and
```
"matches": [ "://.yourcompanydomain.com/" ]
```
4. **If you have multiple domains**: List each domain individually for both `host_permissions` and `matches`:
```
"host_permissions": [
    "://.yourcompanydomain.com/",
    "://.anotherdomain.com/" ]
```
and
```
"matches": [
    "://.yourcompanydomain.com/",
    "://.anotherdomain.com/" ]
```

   Add as many domains as necessary, following the same format.

### 3. Install the Extension on Chrome or Edge

#### For Chrome:

1. Open Chrome and type `chrome://extensions/` in the address bar.
2. Toggle **Developer Mode** on in the top-right corner.
3. Click **Load unpacked** and select the `BlockEmployeeTrackingPlugin` folder you extracted.
4. Click **Details** on the installed extension and enable **Allow in Incognito**.

#### For Edge:

1. Open Edge and type `edge://extensions/` in the address bar.
2. Toggle **Developer Mode** on the left-hand side.
3. Click **Load unpacked** and select the `BlockEmployeeTrackingPlugin` folder.
4. Click **Details** on the installed extension and enable **Allow in InPrivate**.

### 4. Google Tag Manager Setup

1. **Create a Variable**:
   - Go to **Variables** > **New** > **1st Party Cookie** in GTM.
   - Name the variable `Tracking Exclusion Cookie` and set the cookie name to `EMP_TRACKING_EXCLUSION`.

2. **Create a Trigger**:
   - Go to **Triggers** > **New** > **Page View** > **Some Page Views**.
   - Set the condition: `Tracking Exclusion Cookie equals true`.
   - Name the trigger **Block Employee Tracking**.

3. **Apply the Trigger**:
   - Open each tracking tag (e.g., Google Analytics).
   - Add **Block Employee Tracking** as an **Exception**.

## License

MIT License

