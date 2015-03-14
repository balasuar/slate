## Errors

The TaxRates API uses the following error codes and messages:

Error Code | Message 
---------- | ------- 
400 | Unable to resolve one or more document addresses
400 | Value cannot be null. Parameter name: address
400 | The postal code you provided was not valid. Please check your postal code before re-trying.
401 | No authorization was provided. Please check the documentation to determine proper type for this API
401 | The HTTP Authorization header you provided used an invalid scheme or the credentials were missing.
401 | The credentials you provided were not accepted.
401 | Your request provided two forms of authentication. Please check the documentation for the API to determine which form to use.
429 | Rate limiting has been exceeded. Try again later.