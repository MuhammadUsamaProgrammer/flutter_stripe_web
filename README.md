# Flutter Stripe Web

A Flutter library for integrating Stripe payment processing in Flutter web applications. This library provides a simple and effective way to handle payments using Stripe's API and web interface.

## Features

- Create payment intents
- Check payment statuses
- Display Stripe payment interface in a web view

## Installation

To use the `stripe_web_flutter` library in your Flutter web application, add the following dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  stripe_web_flutter:
    git:
      url: https://github.com/MuhammadUsamaProgrammer/stripe_web_flutter.git
```

Replace `yourusername` with your GitHub username or the appropriate repository URL.

## Usage

### Import the Library

```dart
import 'package:stripe_web_flutter/stripe_web_flutter.dart';
```

### Display the Payment Interface

```dart
final paymentId = await stripeService.makePaymentService(
  context: context,
  amountInCents: '5000',
  currency: 'usd',
  secretKey: 'sk_test_...', // NEVER expose this in production frontend!
  publishableKey: 'pk_test_...',
  stripeWebviewUrl: 'http://localhost:5500/web/stripe/stripe_webview.html', // or your deployed HTML
);
```

### Important: Serving the `stripe_webview.html` File

> **Note:**  
> The `stripe_webview.html` file is included in this package under `example/web/stripe/stripe_webview.html`.  
> To use the payment interface, you must serve this file from your own web server or hosting (e.g., GitHub Pages, Vercel, Netlify, or a local server) and provide its public URL to the `stripeWebviewUrl` parameter.
>
> **Recommended:**  
> For easiest integration with Flutter web, copy `stripe_webview.html` into your own project's `/web/stripe/stripe_webview.html` path.  
> This way, it will be available at `/stripe/stripe_webview.html` when you run or build your Flutter web app.
>
> **Example (local development):**
> 1. Copy `stripe_webview.html` to your Flutter project's `web/stripe/stripe_webview.html`.
> 2. Run your Flutter web app as usual:
>    ```sh
>    flutter run -d chrome
>    ```
> 3. Use `http://localhost:PORT/stripe/stripe_webview.html` as the `stripeWebviewUrl` (replace `PORT` with the port your app runs on, e.g. `5270`).
>
> For production, upload it to your hosting and use the public URL.


### Check Payment Status

```dart
final isSuccess = await stripeService.checkPaymentStatus(
  paymentIntentId: paymentIntent['id'],
  secretKey: 'sk_test_...',
);
```

### To create a just Payment Intent

```dart
final stripeService = StripeWebService();
final paymentIntent = await stripeService.createPaymentIntent(
  amount: '5000', // in cents
  currency: 'usd',
  secretKey: 'sk_test_...', // NEVER expose this in production frontend!
);
```

## Example

An example application demonstrating the usage of the `stripe_web_flutter` library can be found in the `example` directory. To run the example, navigate to the `example` folder and execute:

```bash
flutter run -d chrome
```

## API Reference

- `StripeWebService`: Class for interacting with the Stripe API.
  - `createPaymentIntent({required String amount, required String currency, required String secretKey})`
  - `checkPaymentStatus({required String payment_intent_id, required String secretKey})`
  - `makePaymentService({required BuildContext context, required String amountInCents, required String currency, required String secretKey, required String publishableKey, required String stripeWebviewUrl})`

## Security Warning

**Never expose your Stripe secret key in production frontend code.**  
Always use a backend to create payment intents and check payment status in production.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.