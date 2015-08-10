# TaxRates API
The TaxRates API provides a free rates lookup tool to allow merchants to retreive tax rates by location. You can use this REST API to get the sales tax rate for a five digit zip code in the United State or get the sales tax rate for a specific street address in the United States. <a href="http://taxratesapi.avalara.com/" target="_parent">Register for an API Key</a> to get started.

<aside class='notice'> To ensure that the service is available for as many people as possible, we have a rate limit of 15 tax rate requests every 1 minute. If you get a response that you've exceeded the rate limit, we suggest waiting 60 seconds before making your next request. </aside>

## Authentication
Avalara uses API keys to allow access to the API. 
The API key is issued upon <a href="http://taxratesapi.avalara.com/" target="_parent">registering</a> for an account. 

### Authorization Header
Avalara expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: AvalaraApiKey {apikey}`

where `{apikey}` is replaced with your personal API key.

### Alternate Method 
You can pass the API key in the querystring as one of the parameters instead of 
passing it in a header. i.e:

 `https://taxrates.api.avalara.com/address?Line1=435+Ericksen+Ave+NE&City=Bainbridge%20Island&Region=WA&PostalCode=98110&apikey={apikey}`
