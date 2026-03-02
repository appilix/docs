
# Meta SDK Integration

The **Meta SDK** module allows your app to log important **user events** to Meta (Facebook) for analytics, advertising, and monetization purposes.  
This helps you track conversions, optimize ad campaigns, and better understand user behavior.



## Required Information

You need to collect the following credentials from your **Meta App Dashboard**:

| Field | Description | Limit |
|-------|-------------|-------|
| Meta App ID | Unique ID for your Meta app project | Max 200 characters |
| Client Token | Used for secure SDK operations | Max 200 characters |

> 💡 These values can be found in your Meta developer console under your app’s settings.



## JavaScript Bridge for Event Logging

You can log custom events directly from your website using the **Appilix JavaScript bridge**.  
This lets your web code trigger native Meta event logging from inside the app.

### Example: Log an Event from Website to App

```javascript
appilix.postMessage(JSON.stringify({
  type: "meta_log_event",
  props: {
    name: "order_placed", // Event name
    parameters: {         // Event parameters, avoid personal information like email address, name, identity number
      customer_id: "#XXXXXXX",
      order_amount: 117.5,
      country: "US",
    }
  }
}));
```

- `name`: The event name you want to track (e.g., "order_placed", "signup", "purchase")
- `parameters`: Optional metadata for the event (avoid sensitive data)

> 📢 This allows your website (inside the app) to tell the app what events to report to Meta SDK. These events will show up on your Meta Analytics dashboard.



## Summary

| Setting | Required | Description |
|---------|----------|-------------|
| Meta App ID | Yes | Your Meta application ID from the Meta developer portal |
| Client Token | Yes | Token used with the Meta SDK for secure communication |
| JavaScript Event Logging | Optional | Allows your website to instruct the app to log Meta events using the Appilix bridge |



Using the Meta SDK with JavaScript bridge helps combine native and web-based event tracking, providing more accurate attribution and deeper insights across platforms.
