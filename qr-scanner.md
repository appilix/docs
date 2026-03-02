
# QR Scanner

The QR Scanner module allows users to scan QR codes using their device's camera directly from your website. The scanner can be triggered via JavaScript and returns the scanned data back to your web application.

## Starting the QR Scanner

To open the QR Scanner, execute the following JavaScript code on your website:

```javascript
appilix.postMessage(JSON.stringify({
    type: "qr_scanner_init",
    props: {
        enable_confirmation_popup: true, // Show scanned data in a confirmation popup
    }
}));
```
### Configuration Options
- **`enable_confirmation_popup`**: `boolean`
    - `true`: After scanning, the QR scanner will display the scanned data in a confirmation dialog. The user must click the "OK" button to send the data to your website.
    - `false`: After scanning, the QR scanner will automatically send the scanned data to your website without showing a confirmation dialog.


## Receiving Scanned Data

To receive the scanned QR code data in your website, use the following JavaScript:

```javascript
appilix.onmessage = function(event) {
    
    let data = JSON.parse(event.data);
    
    if (data.response.status === "success") {
        console.log("Scanned QR Code:", data.response.result);
        // Handle the scanned data
    } else if (data.response.status === "camera_permission_missing") {
        alert("Please grant camera permission to scan QR codes");
    } else if (data.response.status === "cancel") {
        console.log("User cancelled scanning");
    } else {
        console.error("Scan error:", data.response.status);
    }
    
    // Clean up listener
    appilix.onmessage = null; // Clean up listener after first response
};
```


### Response Format

The response will be a JSON object with the following structure:


| Property | Type | Description |
|----------|------|-------------|
| `type` | `string` | Always returns `"qr_scanner_init"` |
| `response.status` | `string` | Status of the scan: `"success"`, `"error"`, `"camera_permission_missing"`, or `"cancel"` |
| `response.result` | `string` | The scanned QR code data (only present when `status` is `"success"`) |




### Status Values

- **`success`**: QR code was successfully scanned. The `result` field contains the scanned data.
- **`error`**: An error occurred during scanning.
- **`camera_permission_missing`**: The user hasn't granted camera permissions to the app.
- **`cancel`**: The user canceled the scanning operation.


## Page Title

Set the title that appears at the top of your QR Scanner page.

- **Default:** `QR Scan`
- **Limit:** Up to 50 characters
- **Usage:** Helps users understand the purpose of the page instantly.



## Scanning Frame Color

Customize the color of the rectangular scanning frame visible on the camera preview.

| Mode | Default Color | Format |
|------|----------------|--------|
| Light Mode | #186E62 | HEX code |
| Dark Mode | #186E62 | HEX code |

> This frame guides the user to align the QR code correctly for fast and accurate detection.



## Animated Scanning Line Color

This is the animated horizontal line that moves up and down while scanning.

| Mode | Default Color | Format |
|------|----------------|--------|
| Light Mode | #186E62 | HEX code |
| Dark Mode | #186E62 | HEX code |



## Animated Scanning Line Shadow Color

This optional shadow color adds a soft, glowing line effect for better visibility.

| Mode | Default Shadow Color | Format |
|------|------------------------|--------|
| Light Mode | #186E62B3 | HEX code |
| Dark Mode | #186E62B3 | HEX code |

> The shadow color adds depth and makes the scanning animation stand out.



# Result Dialog Customization

When a QR code is scanned, a dialog appears showing the decoded text or URL.  
You can fully customize its **background**, **title**, **content area**, and both **Light/Dark mode** appearances.



## Dialog Background Color

Set the background color of the entire dialog container.

| Mode | Default | Format |
|------|----------|--------|
| Light Mode | #ffffff | HEX |
| Dark Mode | #1C1C1E | HEX |



## Dialog Title

Choose a custom title that appears at the top of the result dialog.

- **Default:** `QR Result`
- **Limit:** Up to 70 characters



## Dialog Title Color

| Mode | Default | Format |
|------|----------|--------|
| Light Mode | #000000 | HEX |
| Dark Mode | #ffffff | HEX |



## Content Background Color

Set the background color for the inner content section of the result dialog.

| Mode | Default | Format |
|------|----------|--------|
| Light Mode | #f9f9f9 | HEX |
| Dark Mode | #323232 | HEX |



## Content Text Color

Control the text color used to display the scanned QR result.

| Mode | Default | Format |
|------|----------|--------|
| Light Mode | #0d0d0d | HEX |
| Dark Mode | #ebebeb | HEX |



## Content Copy Icon Color

This icon allows users to copy the scanned text instantly.

| Mode | Default | Format |
|------|----------|--------|
| Light Mode | #5d5d5d | HEX |
| Dark Mode | #c8c8c8 | HEX |



# Result Dialog Icons

You can customize three icons displayed in the result dialog:

- **Success Icon** (indicates a successful scan)
- **Re-scan Icon** (scan again without closing dialog)
- **Cancel Icon** (close the dialog)

Each icon has independent **color** and **background color** settings for Light and Dark themes.



## Success Icon Colors

| Type | Light Mode | Dark Mode |
|------|------------|------------|
| Icon Color | #4caf50 | #4caf50 |
| Icon Background | #4caf501a | #4caf501a |



## Re-scan Icon Colors

| Type | Light Mode | Dark Mode |
|------|------------|------------|
| Icon Color | #000000DD | #9e9e9e |
| Icon Background | #9e9e9e1a | #ffffff1a |



## Cancel Icon Colors

| Type | Light Mode | Dark Mode |
|------|------------|------------|
| Icon Color | #F44336 | #F44336 |
| Icon Background | #f443361a | #f443361a |



# Summary

| Setting | Default | Description |
|---------|----------|-------------|
| Page Title | `QR Scan` | Title shown on the QR Scanner page |
| Scanning Frame Color | #186E62 | Frame guiding user where to position QR code |
| Scan Line Color | #186E62 | Animated line for scanning effect |
| Scan Line Shadow | #186E62B3 | Soft shadow for scan line |
| Dialog Background | Light: #ffffff, Dark: #1C1C1E | Background of result dialog |
| Dialog Title | `QR Result` | Title shown in scan result dialog |
| Dialog Content Background | Light: #f9f9f9, Dark: #323232 | Background of result content box |
| Dialog Content Text Color | Light: #0d0d0d, Dark: #ebebeb | Color of scanned result text |
| Copy Icon Color | Light: #5d5d5d, Dark: #c8c8c8 | Color of copy-to-clipboard icon |
| Success Icon Colors | Green tones | Indicates successful scan |
| Re-scan Icon Colors | Gray tones | Button to scan again |
| Cancel Icon Colors | Red tones | Button to close dialog |



This configuration allows you to build a **beautiful, modern, and fully themed QR Scanner** that feels native and consistent across all appearances.