Pixcorn Payment Gateway API Documentation
==========================================

Welcome to the Pixcorn Payment Gateway API documentation. This documentation will help you integrate Pixcorn into your application to process high-risk payments with instant USDC settlements.

Getting Started
---------------

Pixcorn is a high-ticket payment gateway designed for enterprise businesses processing $10M+ annually. It provides instant USDC settlements on Polygon network with zero KYC requirements.

How It Works
-----------

1. **Account Creation**: The Pixcorn admin will create your merchant account and provide you with:
   - Your unique API key
   - Your merchant ID (`public_id`)
   - Your USDC wallet address for receiving payments
   - Your commission rate (if applicable)

2. **API Integration**: Use your API key to authenticate all API requests

3. **Payment Processing**: Create payment links and redirect customers to PayGate.to checkout

4. **Webhooks**: Receive instant notifications when payments are completed

Quick Start
-----------

Once you receive your API key from the Pixcorn admin, you can start processing payments immediately:

.. code-block:: bash

   curl -X POST https://pixcorn.com/payments/api/create/ \
     -H "Content-Type: application/json" \
     -H "X-API-Key: YOUR_API_KEY_HERE" \
     -d '{
       "amount": 100.00,
       "currency": "EUR",
       "customer_email": "customer@example.com"
     }'

Contents
--------

.. toctree::
   :maxdepth: 2

   authentication
   payment_api
   webhooks
   error_handling
