# Pixcorn Payment Gateway API Documentation

Official API documentation for Pixcorn Payment Gateway.

## 📚 Documentation

The full documentation is available at: **[docs.pixcorn.com](https://pixcorn-api-docs.readthedocs.io/)**

## 🚀 Quick Start

```bash
curl -X POST https://pixcorn.com/payments/api/create/ \
  -H "Content-Type: application/json" \
  -H "X-API-Key: YOUR_API_KEY_HERE" \
  -d '{
    "amount": 100.00,
    "currency": "EUR",
    "customer_email": "customer@example.com"
  }'
```

## 📖 Contents

- **Authentication**: API key authentication
- **Payment API**: Create and manage payments
- **Webhooks**: Receive payment notifications
- **Error Handling**: Error codes and responses

## 🔧 Building Locally

```bash
pip install -r requirements.txt
make html
```

The documentation will be generated in `_build/html/`.

## 🌐 Website

- **Main Site**: https://pixcorn.com
- **API Docs**: https://pixcorn-api-docs.readthedocs.io/
- **Support**: Contact via Pixcorn admin panel

## 📝 License

© 2025 Pixcorn Digital Solutions. All rights reserved.
