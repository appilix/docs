# Push Notification

The Push Notification page allows you to send real-time notifications to
users who have installed your mobile app. Notifications appear on the
user's device and can be used to share updates, promotions, reminders,
or announcements.

You can send notifications to **all users** or **specific users**.


## Send Notification To

Choose who should receive the notification.

- **All App Users** – Sends the notification to all users of your app.
- **Specific App User** – Sends the notification only to selected users.

Selecting **Specific App User** will show the **Notification Recipients** field.


## Notification Recipients

This field appears only when **Specific App User** is selected.

It allows you to choose the exact user/device that should receive the
notification. If the system cannot identify the user, it may appear as
**Unknown User** along with the device identifier.

### Identifying Users for Targeted Notifications

The app does not automatically know which **website user** is using the device, so it may appear as **Unknown User**.

To identify the user, send the user's identity from your website **after the user logs in**.

When your website runs inside the app, a JavaScript bridge allows the website to communicate with the app. Using this bridge you can pass the user identity.

``` javascript
appilix.postMessage(JSON.stringify({
  type: "firebase_record_user_identity",
  props: {
    user_identity: "user@email.com"
  }
}));
```

This code should run **after the user logs into your website**.

You can send identifiers such as:

-   User email
-   User ID
-   Username
-   Customer ID

Once recorded, the identity will appear in the **Notification
Recipients** list and can also be used when sending notifications via
API.


## Notification Click Action

Defines what happens when the user taps the notification. Available options:

-   **Open App Home Page** -- Opens the main screen of the app.
-   **Open Specific Webpage URL** -- Opens a specific webpage inside the
    app.


## Notification Title

The main heading shown in the notification. Keep it short and clear.

Examples:

-   Big Sale Today
-   New Update Available
-   Your Order Has Shipped


## Notification Image URL (Optional)

You can include an image in the notification by providing a direct image
URL. Example:

    https://example.com/images/sale-banner.png

Notes:

-   The image must be publicly accessible.
-   Supported on **Android notifications**.
-   For **iOS apps**, this field has no effect.


## Notification Body

The main message content of the notification. Examples:

-   Get 30% off on all products today. Tap to explore the offer.
-   Your order has been shipped and will arrive soon.



## Sending Push Notifications via API

You can also send push notifications automatically from your website or
backend using the Appilix API. This is useful for dynamic events such
as:

-   New order placed
-   User registration
-   Payment received
-   New content published
-   Promotional campaigns


### API Endpoint

```
POST https://appilix.com/api/push-notification
```


### Required Parameters

| Parameter | Description |
|----------|-------------|
| app_key | Your app key |
| api_key | Your API key |
| notification_title | Notification title |
| notification_body | Notification message |



### Optional Parameters

| Parameter | Description |
|----------|-------------|
| open_link_url | URL to open when the notification is tapped |
| notification_image | Image URL for the notification (Android only) |
| user_identity | Send notification to specific user/device |
| secondary_app_key | App key for another platform (e.g., iOS) |
| secondary_api_key | API key for the secondary app |



### Sending to Android and iOS Together

If you have separate Android and iOS apps, you can send notifications to both using one request.

- **app_key / api_key** → Primary app
- **secondary_app_key / secondary_api_key** → Second app



### Sending Notification to Specific Users

Use the **user_identity** parameter.

For Multiple users, use :: separator to separate the user_identity:

```
user1::user2::user3
```



### Example API Request

```
app_key=YOUR_APP_KEY
api_key=YOUR_API_KEY
notification_title=New Order Received
notification_body=A new order has been placed on your store
open_link_url=https://example.com/orders
notification_image=https://example.com/order-banner.png
```
