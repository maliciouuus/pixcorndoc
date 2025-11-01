Authentication
==============

API Key Authentication
----------------------

All API requests must be authenticated using an API key provided by the Pixcorn admin team.

Getting Your API Key
--------------------

**Important**: Your API key is created automatically by the Pixcorn admin when your merchant account is set up.

When your account is created, you will receive:

- **API Key**: A unique authentication token (e.g., `pk_live_abc123xyz...`)
- **Merchant ID**: Your public merchant identifier (`public_id`)
- **USDC Wallet Address**: Your Polygon USDC wallet address for receiving payments
- **Commission Rate**: Your affiliate commission rate (if applicable)

Using Your API Key
------------------

Include your API key in the request headers:

.. code-block:: bash

   curl -X POST https://pixcorn.com/payments/api/create/ \
     -H "Content-Type: application/json" \
     -H "X-API-Key: YOUR_API_KEY_HERE" \
     -d '{...}'

Or using the `Authorization` header:

.. code-block:: bash

   curl -X POST https://pixcorn.com/payments/api/create/ \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer YOUR_API_KEY_HERE" \
     -d '{...}'

Supported Headers
----------------

Both header formats are supported:

- ``X-API-Key: YOUR_API_KEY``
- ``Authorization: Bearer YOUR_API_KEY``

Security Best Practices
----------------------

1. **Never expose your API key** in client-side code or public repositories
2. **Store API keys securely** using environment variables or secure key management systems
3. **Use different keys** for test and production environments (if provided)
4. **Rotate keys** if you suspect they have been compromised

Invalid API Key Response
------------------------

If your API key is missing or invalid, you will receive a ``401 Unauthorized`` response:

.. code-block:: json

   {
     "error": "Invalid or missing API key",
     "code": "UNAUTHORIZED"
   }

Questions?
----------

If you need an API key or have questions about your account, please contact the Pixcorn admin team.

