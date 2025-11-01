Error Handling
==============

Pixcorn API uses standard HTTP status codes to indicate success or failure.

HTTP Status Codes
-----------------

.. list-table:: Status Codes
   :header-rows: 1

   * - Code
     - Description
   * - ``200 OK``
     - Request successful
   * - ``201 Created``
     - Resource created successfully
   * - ``400 Bad Request``
     - Invalid request parameters
   * - ``401 Unauthorized``
     - Missing or invalid API key
   * - ``404 Not Found``
     - Resource not found
   * - ``500 Internal Server Error``
     - Server error

Error Response Format
--------------------

All error responses follow this format:

.. code-block:: json

   {
     "error": "Error message description",
     "code": "ERROR_CODE"
   }

Common Errors
-------------

Invalid API Key
~~~~~~~~~~~~~~~

.. code-block:: json

   {
     "error": "Invalid or missing API key",
     "code": "UNAUTHORIZED"
   }

**Solution**: Check that your API key is correct and included in the request headers.

Missing Required Field
~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: json

   {
     "error": "Missing required field: amount",
     "code": "VALIDATION_ERROR"
   }

**Solution**: Ensure all required fields are included in your request.

Invalid Wallet Address
~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: json

   {
     "error": "Invalid USDC wallet address (must be 0x... with 42 characters)",
     "code": "VALIDATION_ERROR"
   }

**Solution**: Verify your wallet address format is correct.

Payment Not Found
~~~~~~~~~~~~~~~~~

.. code-block:: json

   {
     "error": "Payment not found",
     "code": "NOT_FOUND"
   }

**Solution**: Check that the payment ID is correct and belongs to your merchant account.

Best Practices
--------------

1. **Always check the status code** before processing responses
2. **Log errors** for debugging and monitoring
3. **Implement retry logic** for transient errors (5xx)
4. **Handle rate limiting** if you make many requests
5. **Validate responses** before processing data

Example Error Handling (Python)
--------------------------------

.. code-block:: python

   import requests

   try:
       response = requests.post(
           'https://pixcorn.com/payments/api/create/',
           headers={
               'Content-Type': 'application/json',
               'X-API-Key': 'YOUR_API_KEY'
           },
           json={
               'amount': 100.00,
               'currency': 'EUR'
           }
       )
       
       response.raise_for_status()
       data = response.json()
       
       if data.get('success'):
           print(f"Payment URL: {data['payment_url']}")
       else:
           print(f"Error: {data.get('error')}")
           
   except requests.exceptions.HTTPError as e:
       if e.response.status_code == 401:
           print("Invalid API key")
       elif e.response.status_code == 400:
           error_data = e.response.json()
           print(f"Validation error: {error_data.get('error')}")
       else:
           print(f"HTTP error: {e}")
           
   except Exception as e:
       print(f"Request failed: {e}")

Example Error Handling (JavaScript)
-----------------------------------

.. code-block:: javascript

   async function createPayment(amount, currency) {
     try {
       const response = await fetch('https://pixcorn.com/payments/api/create/', {
         method: 'POST',
         headers: {
           'Content-Type': 'application/json',
           'X-API-Key': 'YOUR_API_KEY'
         },
         body: JSON.stringify({
           amount: amount,
           currency: currency
         })
       });
       
       if (!response.ok) {
         const error = await response.json();
         throw new Error(error.error || 'Request failed');
       }
       
       const data = await response.json();
       return data;
       
     } catch (error) {
       console.error('Payment creation failed:', error.message);
       throw error;
     }
   }

