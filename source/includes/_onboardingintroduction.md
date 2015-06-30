# Onboarding API

<aside class="alert">The Onboarding API is available upon special request only; you must contact Avalara directly to be whitelisted for use of this service. </aside>

The Onboarding API is designed to allow partners to automatically provision individual customer accounts and assist with company profile setup on those accounts, allowing for a quick, automated account setup for these customers. For a basic company profile, only a single call to <a href="#create-an-account">POST /accounts</a> is required.

To call this service in a sandbox environment, use the base service URL `https://sandbox.onboarding.api.avalara.com/`

## Headers

**Authorization:** header, *required*  
In the format "Basic [username]:[password]" encoded to <a href="http://en.wikipedia.org/wiki/Base64" target="_parent">Base64</a>, as per <a href="http://en.wikipedia.org/wiki/Basic_access_authentication" target="_parent">basic access authentication</a>. Note that username and password must be used for this service, and calls cannot be authenticated with account number/license key.  
e.g.: `Basic a2VlcG1vdmluZzpub3RoaW5nMnNlZWhlcmU=`

**Accept:** header, *required*  
Determines the format of response data. Either `application/json` or `application/xml`.

**Client:** header, *required*  
Identifies the client system calling the service, used for debugging. e.g. `Drupal Connector v6.2`

**Content Type:** header, *required for POST methods only*  
Standard content type header, indicating the content type of the request content. Either `application/json` or `application/xml`.

**Content Length:** header, *required for POST methods only*  
Standard content length header, indicating the size of the request content.

NOTE: All dates are formatted like <a href='http://xml2rfc.ietf.org/public/rfc/html/rfc3339.html#anchor14'>2015-11-24</a>

