# Flutter Stripe Web

A Flutter library for integrating Stripe payment processing in Flutter web applications. This library provides a simple and effective way to handle payments using Stripe's API and web interface.

## Features

- Create payment intents
- Check payment statuses
- Display Stripe payment interface in a web view

## Installation

To use the `flutter_stripe_web` library in your Flutter web application, add the following dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_stripe_web:
    git:
      url: https://github.com/MuhammadUsamaProgrammer/flutter_stripe_web.git
```

Replace `yourusername` with your GitHub username or the appropriate repository URL.

## Usage

### Import the Library

```dart
import 'package:flutter_stripe_web/flutter_stripe_web.dart';
```

### Create a Payment Intent

```dart
final stripeService = StripeWebService();
final paymentIntent = await stripeService.createPaymentIntent(
  amount: '5000', // in cents
  currency: 'usd',
  secretKey: 'sk_test_...', // NEVER expose this in production frontend!
);
```

### Check Payment Status

```dart
final isSuccess = await stripeService.checkPaymentStatus(
  paymentIntentId: paymentIntent['id'],
  secretKey: 'sk_test_...',
);
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

## Example

An example application demonstrating the usage of the `flutter_stripe_web` library can be found in the `example` directory. To run the example, navigate to the `example` folder and execute:

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