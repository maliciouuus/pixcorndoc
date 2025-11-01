Webhooks
========

Pixcorn sends webhook notifications to your configured webhook URL when payment events occur.

Webhook Configuration
--------------------

Your webhook URL is configured by the Pixcorn admin when your merchant account is created. You can also specify a custom webhook URL per payment request.

Webhook Events
--------------

Currently supported events:

- ``payment.paid``: Payment completed successfully

Payment Paid Event
------------------

When a payment is completed, Pixcorn sends a POST request to your webhook URL.

Request Headers
---------------

.. code-block:: text

   Content-Type: application/json
   User-Agent: Pixcorn-Webhook/1.0

Request Body
------------

.. code-block:: json

   {
     "event": "payment.paid",
     "payment_id": "f4a26a32-4300-417d-b8ae-dcfb8996d7d7",
     "merchant_order_id": "order_12345",
     "status": "paid",
     "amount": "100.00",
     "currency": "EUR",
     "payout_amount": "94.00",
     "coin_type": "polygon_usdc",
     "txid": "0x1234567890abcdef...",
     "paid_at": "2025-01-15T10:30:00Z"
   }

Webhook Security
----------------

**Important**: Always verify webhook requests originate from Pixcorn.

Recommended security measures:

1. **Verify the source IP** (if possible)
2. **Implement idempotency** - Process each payment only once
3. **Log all webhook requests** for debugging
4. **Return 200 OK** immediately, then process asynchronously

Example Webhook Handler (Python)
----------------------------------

.. code-block:: python

   from django.http import HttpResponse
   import json
   import logging

   logger = logging.getLogger(__name__)

   def webhook_handler(request):
       if request.method != 'POST':
           return HttpResponse(status=405)
       
       try:
           data = json.loads(request.body)
           event = data.get('event')
           payment_id = data.get('payment_id')
           
           if event == 'payment.paid':
               # Process payment
               order_id = data.get('merchant_order_id')
               payout_amount = data.get('payout_amount')
               
               # Update your database
               # Mark order as paid
               # Send confirmation email
               
               logger.info(f"Payment {payment_id} completed: {payout_amount} USDC")
               
           return HttpResponse(status=200)
           
       except Exception as e:
           logger.error(f"Webhook error: {e}")
           return HttpResponse(status=500)

Example Webhook Handler (PHP)
------------------------------

.. code-block:: php

   <?php
   $data = json_decode(file_get_contents('php://input'), true);
   
   if ($data['event'] === 'payment.paid') {
       $payment_id = $data['payment_id'];
       $order_id = $data['merchant_order_id'];
       $payout_amount = $data['payout_amount'];
       
       // Update your database
       // Mark order as paid
       // Send confirmation email
       
       http_response_code(200);
   }
   ?>

Example Webhook Handler (Node.js)
----------------------------------

.. code-block:: javascript

   app.post('/webhook', (req, res) => {
     const { event, payment_id, merchant_order_id, payout_amount } = req.body;
     
     if (event === 'payment.paid') {
       // Process payment
       // Update database
       // Mark order as paid
       // Send confirmation email
       
       console.log(`Payment ${payment_id} completed: ${payout_amount} USDC`);
     }
     
     res.status(200).send('OK');
   });

Response Requirements
----------------------

Your webhook endpoint must:

1. **Return HTTP 200** within 5 seconds
2. **Handle duplicate requests** (idempotency)
3. **Log all requests** for debugging

If your endpoint doesn't respond within 5 seconds or returns an error, Pixcorn will retry the webhook up to 3 times with exponential backoff.

Testing Webhooks
----------------

You can test your webhook endpoint using tools like:

- `ngrok <https://ngrok.com/>`_ for local development
- `webhook.site <https://webhook.site/>`_ for testing

Questions?
----------

If you need help configuring webhooks or have questions, please contact the Pixcorn admin team.

