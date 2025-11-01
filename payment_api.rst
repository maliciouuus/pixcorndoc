Payment API
===========

Overview
--------

The Pixcorn Payment API allows you to create crypto payment links for your customers. Payments are processed via USDC on Polygon network through PayGate.to.

**Base URL**: ``https://pixcorn.com``

**All API requests require authentication via API Key in the X-API-Key header.**

Creating a Payment
------------------

Create a payment link by sending a POST request to the payment endpoint.

Endpoint
--------

.. code-block:: text

   POST /payments/api/create/

Request Headers
---------------

.. code-block:: text

   Content-Type: application/json
   X-API-Key: YOUR_API_KEY_HERE

Request Body
------------

.. list-table:: Required Fields
   :header-rows: 1

   * - Field
     - Type
     - Description
   * - ``amount``
     - decimal
     - Payment amount (e.g., 100.00)
   * - ``currency``
     - string
     - Currency code (USD, EUR, CAD, etc.)

.. list-table:: Optional Fields
   :header-rows: 1

   * - Field
     - Type
     - Description
   * - ``customer_email``
     - string
     - Customer email address
   * - ``webhook_url``
     - string
     - Custom webhook URL (overrides your account default webhook URL)
   * - ``order_id``
     - string
     - Your internal order ID

.. note::
   Your **wallet address** and **default webhook URL** are configured in your merchant account by the Pixcorn admin. You don't need to provide them in each API request.

Example Request
---------------

.. code-block:: bash

   curl -X POST https://pixcorn.com/payments/api/create/ \
     -H "Content-Type: application/json" \
     -H "X-API-Key: pk_live_abc123xyz" \
     -d '{
       "amount": 100.00,
       "currency": "EUR",
       "customer_email": "customer@example.com",
       "order_id": "order_12345"
     }'

Example Response
----------------

.. code-block:: json

   {
     "success": true,
     "payment_url": "https://checkout.paygate.to/pay.php?address=...",
     "payment_id": "f4a26a32-4300-417d-b8ae-dcfb8996d7d7",
     "message": "Payment created! Redirect your customer to payment_url",
     "details": {
       "amount": "100",
       "currency": "EUR",
       "merchant_will_receive": "94.00 USDC"
     }
   }

Payment URL
-----------

The ``payment_url`` in the response is the PayGate.to checkout page URL. You must redirect your customer to this URL:

.. code-block:: javascript

   // Redirect customer to payment page
   window.location.href = response.payment_url;

   // Or open in new tab
   window.open(response.payment_url, '_blank');

**Important**: Never embed the payment URL in an iframe. Customers must be redirected to the PayGate.to domain directly.

Checking Payment Status
-----------------------

Query the payment status using the payment ID:

.. code-block:: bash

   curl -X GET https://pixcorn.com/payments/api/status/{payment_id}/ \
     -H "X-API-Key: YOUR_API_KEY_HERE"

Response
--------

.. code-block:: json

   {
     "payment_id": "f4a26a32-4300-417d-b8ae-dcfb8996d7d7",
     "status": "paid",
     "amount": "100.00",
     "currency": "EUR",
     "payout_amount": "94.00 USDC",
     "paid_at": "2025-01-15T10:30:00Z"
   }

Payment Statuses
----------------

- ``pending``: Payment created, waiting for customer
- ``processing``: Payment in progress
- ``paid``: Payment completed successfully
- ``failed``: Payment failed
- ``expired``: Payment link expired

Currency Conversion
-------------------

Convert amounts to USDC:

.. code-block:: bash

   curl -X GET "https://pixcorn.com/payments/api/convert/?amount=100&currency=EUR" \
     -H "X-API-Key: YOUR_API_KEY_HERE"

Response
--------

.. code-block:: json

   {
     "amount": "100.00",
     "currency": "EUR",
     "usdc_amount": "108.00",
     "exchange_rate": "1.08"
   }

Commission Structure
-------------------

Commission rates are configured per merchant by the Pixcorn admin. You will receive the exact payout amount specified in the API response and webhook notifications.

Your specific commission rate will be provided when your account is created.

