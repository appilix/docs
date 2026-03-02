# Apple In-App Purchase

Apple In-App Purchase (IAP) allows you to sell **digital products and services** directly inside your iOS app.

This module supports:

- **In-App Purchase:** Consumable, Non-Consumable
- **In-App Subscription:** Auto-renewable subscriptions



## When Is This Module Needed?

Apple In-App Purchase is **required only for iOS apps** when you are selling:

- Digital content
- Premium features
- Subscriptions
- Virtual items
- In-app upgrades

If you are selling **physical products or real-world services**, you can use your website’s own payment gateway inside the app. Apple does not require In-App Purchase for physical goods.



## Supported Purchase Types

| Product Type | Description |
|--------------|-------------|
| Consumable | Can be purchased multiple times. Examples: Coins, Credits, Game lives, Temporary boosts. Use this when the product gets “used up” and can be bought again. |
| Non-Consumable | Purchased once and does not expire. Examples: Remove Ads, Lifetime Premium, Unlock Feature. Use this when the user should permanently own the product. |
| Subscription (Auto-Renewable) | Renews automatically until canceled. Examples: Monthly membership, Yearly premium access, Streaming access. Use this for recurring access to content or services. |



## Create and Attach In-App Purchase

1. Log in to **App Store Connect** and open your app from **My Apps**.
2. Create the product:
    - Go to **In-App Purchases** → Click **Create** → Choose:
        - Consumable, or
        - Non-Consumable
    - Or go to **Subscriptions** → Create **Auto-Renewable Subscription**
3. Enter Product ID in this format:  
   bundle_id.product_slug  
   Example: com.example.app.product_1
4. Set pricing, availability, and localization. Save the product.
5. Go to your **App Version** page → Scroll to **In-App Purchases** → Click **Add** → Select the created product.



## JavaScript Bridge for Apple In-App Purchase

If your website already uses its own payment gateway, the purchase
button normally processes payments directly on the website. However, when the website is opened inside the iOS app, digital
purchases must use Apple In-App Purchase instead of the website payment
system.

To handle this, you must use the JavaScript Bridge provided by the app.



### Step 1: Trigger Purchase from Website

When the user clicks the purchase button, execute:

``` javascript
appilix.postMessage(JSON.stringify({
  type: "apple_iap_init",
  props: {
    product_id: "com.thembey.bazar.product1",
    product_type: "consumable",
    app_account_token: "550e8400-e29b-41d4-a716-446655440000",  // Optional UUID
  }
}));
```

#### Parameters

-   **product_id:** Must match exactly the Product ID created in App Store Connect.

-   **product_type**: `consumable` or `non-consumable` or `subscription`

-   **app_account_token (Optional)**: A UUID string. If provided, it will be included in the purchase notification payload as `appAccountToken`. Useful for linking purchases with your internal user system.



### Step 2: Listen for Purchase Response

After triggering the purchase, register a listener on your website:

``` javascript
appilix.onmessage = function(event) {
  const data = event.data;

  if (!data || data.type !== "apple_iap_init") return;

  const response = data.response;

  if (response.status) {
    // ✅ Purchase Success
    console.log("Purchase Successful:", response.product);

    // Deliver product here
    // Example:
    // sendToServer(response.product);

  } else {
    // ❌ Purchase Failed
    console.log("Purchase Failed:", response.message);
  }

  // Remove listener after handling
  appilix.onmessage = null;
};
```

#### When Purchase is Successful

-   `status` will be `true`
-   Product details will be returned
-   Verify the purchase on your backend
-   Deliver the digital product

#### When Purchase Fails

-   `status` will be `false`
-   A `message` will explain the reason
-   Do not deliver the product




## Important Notes

- In-App Purchase is mandatory for digital goods on iOS.
- Physical goods can use your website payment system.
- Product ID must match exactly between App Store Connect and the App Dashboard.
- Always test purchases using Apple Sandbox environment before publishing.


## Final Note

Implementing Apple In-App Purchase using the JavaScript bridge requires proper website development knowledge.

You may need to:

- Modify your purchase button logic
- Handle JavaScript events correctly
- Process purchase responses securely
- Validate purchases on your backend server

If you are not familiar with JavaScript or backend development, it is recommended to involve a developer to ensure correct and secure implementation.