# Biometric Authentication Settings

**Biometric Authentication** enhances your app's security by requiring users to verify their identity using biometric sensors (fingerprint, Face ID) or device credentials (PIN, pattern, password) before accessing sensitive content.

Configure authentication requirements for your entire app or specific pages to protect confidential information.


## Restrict to Face ID and Fingerprint Auth?

Control which authentication methods are allowed when users access protected content.

- **Yes:** Only biometric authentication (Face ID, Fingerprint) is accepted
- **No:** Users can also authenticate using device PIN, pattern, or password lock

**Default:** No (allows all device authentication methods)

> 💡 **Recommendation:** Enable "Yes" for maximum security when protecting highly sensitive information. However, note that some devices may not have biometric sensors, which could prevent access for those users.



## Message to Show in Authentication Screen

Customize the message displayed to users when they're prompted to authenticate.

- **Maximum Length:** 200 characters
- **Default:** "Please authenticate to see the confidential information."

**Example Messages:**

- "Verify your identity to access account settings"
- "Authenticate to view payment information"
- "Please confirm it's you to continue"

> 📝 Use clear, concise language that explains why authentication is required.



## FaceID Usage Description (iOS Only)

**Required for iOS apps using Face ID authentication.**

Provide a clear explanation of why your app needs Face ID access. This description:

- Appears in your app's `Info.plist` file
- Is shown to users when Face ID permission is requested
- Must be reviewed and approved by Apple

**Requirements:**

- **Maximum Length:** 500 characters
- **Default:** "This feature is required to verify the device owner before seeing confidential information."

**Example Descriptions:**

- "We use Face ID to ensure only you can access your sensitive account information"
- "Face ID authentication protects your private data from unauthorized access"
- "This app requires Face ID to verify your identity when viewing confidential content"

> ⚠️ **Apple Review Requirement:** Be specific and honest about why Face ID is needed. Vague descriptions may result in app rejection.



## Require Biometric Auth on These URLs

Specify which pages or sections of your app should require biometric authentication.

- Enter one *domain*, *full URL*, or *URL fragment* per line
- **Supports wildcard patterns (`*`)** for flexible matching
- **Default:** Empty (no authentication required)

**URL Matching Examples:**

| Example Input | Matches |
|---------------|---------|
| `example.com/account` | Any URL containing `example.com/account` |
| `example.com/settings` | Any URL containing `example.com/settings` |
| `[example.com/profile]` | Exact match with `example.com/profile` only |
| `example.com/*/payment` | URLs like `example.com/user/payment`, `example.com/cart/payment`, etc. |

> 🧭 Avoid adding prefixes like `https://` or `https://www.` for proper matching.  
> Use square brackets `[ ... ]` for *exact URL matches*.



## Use Cases

Require authentication when users access Sensitive Pages:

- **Account settings:** `example.com/account`
- **Payment information:** `example.com/payment`
- **Private messages:** `example.com/messages/private`
- **Medical records:** `example.com/health/records`


## JavaScript Bridge for Programmatic Authentication

Your website can trigger biometric authentication directly using the **JavaScript bridge**. This allows you to:

- Trigger authentication on demand (e.g., before form submission, accessing sensitive data)
- Customize authentication messages per context
- Redirect users after successful authentication
- Override global settings for specific scenarios

To trigger the Authentication on your need, execute the following code snippet in your website:

```javascript
appilix.postMessage(JSON.stringify({
  type: "biometric_auth_init",
  props: {
      url: "https://darkmysite.com",        // Optional redirect after success
      description: "Confirm your identity", // Message shown during auth
      force_biometric_only: true            // Only allow biometric methods
  }
}));
```

Also App will response with the result of authentication which you can detect and perform based on that.
To read the response, you can use the following code snippet:

```javascript
appilix.onmessage = function (event) {
  switch (JSON.parse(event.data).response) {
    case 'success':
      console.log('Authentication successful');
      break;
    case 'failed':
      console.log('Authentication failed');
      break;
    case 'missing':
      console.log('Biometric authentication not available');
      break;
    case 'error':
      console.log('Authentication error occurred');
      break;
  }
};
```



## Summary

| Setting | Default | Description |
|---------|---------|-------------|
| Force Biometric Only | No | Restrict to Face ID/Fingerprint only (excludes PIN/pattern) |
| Authentication Message | "Please authenticate..." | Message shown during authentication |
| FaceID Usage Description | "This feature is required..." | iOS-specific explanation for App Store review |
| Protected URLs | Empty | List of URLs requiring authentication |


By configuring **Biometric Authentication**, you add an essential security layer to your app, ensuring that confidential information remains protected while maintaining a smooth user experience.