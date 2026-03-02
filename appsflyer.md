# AppsFlyer Settings

The **AppsFlyer** module integrates the **AppsFlyer SDK** into your app for advanced **analytics**, **user attribution**, and **marketing campaign tracking**.  
With this integration, you can track **installs**, **in-app events**, and **user engagement**, all visible from your AppsFlyer Dashboard.



## Overview

**AppsFlyer** is a leading SaaS platform that helps you measure and optimize your mobile marketing campaigns.  
By connecting your app to AppsFlyer, you can monitor key metrics like installs, sessions, retention, and user behavior.

Once integrated:
- AppsFlyer will automatically record installs and app opens.
- You can trigger **custom events** from your website using a simple JavaScript bridge.
- These events appear directly in your **AppsFlyer dashboard** for deeper analysis.



## Dev Key

Enter the **Dev Key** obtained from your **AppsFlyer Dashboard**.

- **Required:** ✅ Yes
- **Default:** Empty
- **Where to find:**
    1. Log in to your [AppsFlyer Dashboard](https://www.appsflyer.com).
    2. Navigate to your app’s **Settings** page.
    3. Copy your **Dev Key**.

> 💡 The Dev Key uniquely identifies your AppsFlyer account and links your app to it.



## App ID

Enter your **App ID** as provided in your **AppsFlyer Dashboard**.

- **Required:** ✅ Yes
- **Default:** Empty
- **Notes:**
    - For **iOS**, enter only the numeric part of your App ID (exclude the `id` prefix).
        - Example: if your App ID is `id123456789`, enter `123456789`.
    - For **Android**, use the package name (e.g., `com.example.myapp`).

> 🧩 Make sure this matches the exact App ID listed in your AppsFlyer project.


## JavaScript Bridge for Recording Events

Your website can communicate directly with the app using a **JavaScript bridge**. This allows you to trigger AppsFlyer **in-app events** from your website that’s loaded inside the app.

You can use this bridge to:
- Track **purchase events** (`order_placed`, `subscription_started`, etc.)
- Track **user actions** (e.g., button clicks, sign-ups)
- Track **custom goals** (e.g., content viewed, video played)



You can add this JavaScript snippet to your website to trigger an AppsFlyer event in the app:

```javascript
appilix.postMessage(JSON.stringify({
  type: "appsflyer_log_event",
  props: {
    name: "order_placed", // Event name
    parameters: {         // Event parameters, avoid personal information like email, name, or IDs
      customer_id: "#XXXXXXX",
      order_amount: 117.5,
      country: "US",
    }
  }
}));
```

### Explanation

-   **type**: Must always be `"appsflyer_log_event"`.
-   **name**: The event name you want to log (`purchase`, `signup`,
    `order_placed`).
-   **parameters**: Additional event details (avoid personal or
    sensitive data).

### Data Privacy Note

AppsFlyer follows strict data protection policies.
To stay compliant:
- Do not include any personal information in event parameters (such as user names, email addresses, or IDs).
- Only include **non-personal data** relevant to the event (e.g., order total, country, or product ID).
- This ensures compliance with **GDPR** and **AppsFlyer’s data privacy policies**.


## Summary

| Setting | Required | Description |
|---------|-----------|-------------|
| **Dev Key** | Yes | Unique key that connects your app to your AppsFlyer account. |
| **App ID** | Yes | Your app’s AppsFlyer App ID (iOS numeric ID or Android package name). |
| **JavaScript Event Bridge** | Optional | Allows your website to trigger native AppsFlyer in-app events using JavaScript. |


By enabling this module, you gain full visibility into user behavior and
conversions, combining the flexibility of your website with the power of
native tracking using the **AppsFlyer SDK**.
