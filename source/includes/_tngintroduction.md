# TNG API

<aside class="alert"> This API is currently in beta release only. </aside>

The Tax API is used to calculate tax and record transactions for tax purposes. Tax can be calculated (and transactions can be recorded) on sales, purchaes, and internal transfer transactions.

There are two kinds of records managed by this API: `Calculations` and `Transactions`. When you want to just calculate tax but not include that calculate on a future filing (e.g. to present tax on a quote or pre-sale order), you should use the `Calculations` resource. When you want to record that sale for filing and reporting, you should call the `Transactions` resource.

The request and response formats for both resources is the same, and the response simply adds tax calculation and resolution information to the request format. All formats are documented in the TaxDocument Format section.

When working with this API, care should be taken to reflect your expected document workflow as part of the integration process. The expected workflow and associated calls are diagrammed here:
<img src="images/tng_document_flow.jpg" alt="TNG Document Flow">

## Headers

```plaintext
Authorization: AvalaraAuth : MmVhZDk4YzEtZWNiZi00NzA4LThkODYtYjAxYWY4YmMxM2U1
Accept: application/json; tax-version=1
Content-Type: application/json
User-Agent: Drupal Connector v6.2
```

The following headers are required for all calls to the service.

**Authorization:** *required*  
The Authorization header is used to identify the actor (person or system) making the request. The value is of the format "AvalaraAuth : access info", where access info is the Base64 encoding of the string "id:key" for the actor making the call. The access info is issued by avalara.com when the user registers for an access to a service.

**Accept:** *required*  
The content type header is used by the client to tell the server how to interpret the message body. We set this to application/json, but we also add a parameter called "tax-version" indicating the version of the tax transaction record format. This parameter is required. If this parameter is not specified an error will be returned by the service. 

**Content Type:** *required for requests with payloads*  
Standard content type header, indicating the content type of the request content.

**User-Agent:** *required*  
The user agent header is used to indicate the technology of the client application (or connector). This is a string that is built into a connector or issued to a development partner.