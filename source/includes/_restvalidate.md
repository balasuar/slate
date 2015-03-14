## Validate

Normalizes a single US or Canadian address, providing a non-ambiguous address match.

##### URL and Method

Development: `GET https://development.avalara.net/1.0/address/validate?<address>`  
Production: `GET https://avatax.avalara.net/1.0/address/validate?<address>`
    
<aside class='notice'>
    To get an XML response, use `GET /1.0/address/validate.xml?<address>`
</aside>

##### Headers

**Authorization:** header, *required*  
In the format "Basic [account number]:[license key]" encoded to <a href="http://en.wikipedia.org/wiki/Base64" target="_parent">Base64</a>, as per <a href="http://en.wikipedia.org/wiki/Basic_access_authentication" target="_parent">basic access authentication</a>.  
e.g.: `Basic a2VlcG1vdmluZzpub3RoaW5nMnNlZWhlcmU=`

### Validate Request

```shell
curl --user 1234567890:A1B2C3D4E5F6G7H8 \
"https://development.avalara.net/1.0/address/validate?Line1=118+N+Clark+St&Line2=Suite+100&Line3=ATTN+Accounts+Payable&City=Chicago&Region=IL&PostalCode=60602&Country=US"
```

```csharp
Address address = new Address();
address.Line1 = "118 N Clark St";
address.City = "Chicago";
address.Region = "IL";
address.Line2 = "Suite 100";
address.Line3 = "ATTN Accounts Payable";
address.Country = "US";
address.PostalCode = "60602";

// Convert input address data to query string
string querystring = string.Empty;
querystring += (address.Line1 == null) ? string.Empty : "Line1=" + address.Line1.Replace(" ", "+");
querystring += (address.Line2 == null) ? string.Empty : "&Line2=" + address.Line2.Replace(" ", "+");
querystring += (address.Line3 == null) ? string.Empty : "&Line3=" + address.Line3.Replace(" ", "+");
querystring += (address.City == null) ? string.Empty : "&City=" + address.City.Replace(" ", "+");
querystring += (address.Region == null) ? string.Empty : "&Region=" + address.Region.Replace(" ", "+");
querystring += (address.PostalCode == null) ? string.Empty : "&PostalCode=" + address.PostalCode.Replace(" ", "+");
querystring += (address.Country == null) ? string.Empty : "&Country=" + address.Country.Replace(" ", "+");

// Call the service
Uri webAddress = new Uri(svcURL + "address/validate.xml?" + querystring);
HttpWebRequest request = WebRequest.Create(webAddress) as HttpWebRequest;
request.Headers.Add(HttpRequestHeader.Authorization, "Basic " + Convert.ToBase64String(ASCIIEncoding.ASCII.GetBytes(accountNum + ":" + license)));
request.Method = "GET";

WebResponse response = request.GetResponse();
```

```java
Address address = new Address();
address.Line1 = "118 N Clark St";
address.City = "Chicago";
address.Region = "IL";
address.Line2 = "Suite 100";
address.Line3 = "ATTN Accounts Payable";
address.Country = "US";
address.PostalCode = "60602";

//Create query/url
String queryparams = address.toQuery();
String addrval = serviceURL + "address/validate?"+ queryparams;
URL url;

HttpURLConnection conn;

//Connect to specified URL 
//with authorization header
url = new URL(addrval);
conn = (HttpURLConnection)url.openConnection();

//Create auth content
String encoded = "Basic " + new String(Base64.encodeBase64((accountNumber+":"+licenseKey).getBytes()));

//Add authorization header
conn.setRequestProperty ("Authorization", encoded);
conn.disconnect();

//Deserialization object
ObjectMapper mapper = new ObjectMapper();
ValidateResult vres = mapper.readValue(conn.getInputStream(),ValidateResult.class);
```

```php
<?php
$address = new Address();
$address->setLine1("118 N Clark St");
$address->setCity("Chicago");
$address->setRegion("IL");
$address->setLine2("Suite 100");
$address->setLine3("ATTN Accounts Payable");
$address->setCountry("US");
$address->setPostalCode("60602");
$validateRequest = new ValidateRequest();
$validateRequest->setAddress($address);
$url =  $this->config['url'].'/1.0/address/validate?'. http_build_query($validateRequest->getAddress());
$curl = curl_init();
curl_setopt($curl, CURLOPT_HTTPAUTH, CURLAUTH_BASIC);
curl_setopt($curl, CURLOPT_USERPWD, $accountNumber.":".$licenseKey);
curl_setopt($curl, CURLOPT_URL, $url);
curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);

$result = curl_exec($curl);

ValidateResult::parseResult($result);
?>
```

Input to normalize a single US or Canadian address, providing a non-ambiguous address match.

**Line1:** string [50], *required*  
Address line 1

**Line2:** string [50], *optional*  
Address line 2

**Line3:** string [50], *optional*  
Address line 3

**City:** string [50], *optional unless PostalCode is not specified*  
City name

**Region:** string [3], *optional unless PostalCode is not specified*  
State, province, or region name

**Country:** string [50], *optional*  
Country code

**PostalCode:** string [11], *optional unless City and Region are not specified*  
Postal or ZIP code

### ValidateResult

```json
{
"ResultCode": "Success",
"Address": {
    "Line1": "ATTN Accounts Payable",
    "City": "Chicago",
    "Region": "IL",
    "PostalCode": "60602-1304",
    "Country": "US",
    "County": "Cook",
    "FipsCode": "1703100000",
    "CarrierRoute": "C012",
    "PostNet": "606021304990",
    "AddressType": "H",
    "Line2": "118 N Clark St Ste 100"
    }
}
```

Output for address/validate showing the validated address match or address validation errors.

**Line1:** string [50]  
Address line 1

**Line2:** string [50]  
Address line 2

**Line3:** string [50]  
Address line 3

**City:** string [50]  
City name

**Region:** string [3]  
State, province or region name

**Country:** string [2]  
Country code as ISO 3166-1 (Alpha-2) country code (e.g. “US”)

**AddressType:** string [1]  
Address type code.

* F - Firm or company address
* G - General Delivery address
* H - High-rise or business complex
* P - PO Box address
* R - Rural route address
* S - Street or residential address

**PostalCode:** string [11]  
Postal or ZIP code

**County:** string [50]  
County name

**FipsCode:** string [10]  
FIPSCode is a unique 10-digit code representing each geographic combination of state, county, and city. The code is made up of the Federal Information Processing Code (FIPS) that uniquely identifies each state, county, and city in the U.S. Returned for US addresses only.  
Digits represent jurisdiction codes:

* 1-2 State code
* 3-5 County code
* 6-10 City code

**CarrierRoute:** string [4]  
CarrierRoute is a four-character string representing a US postal carrier route. The first character of this property, the term, is always alphabetic, and the last three numeric. For example, "R001" or "C027" would be typical carrier routes. The alphabetic letter indicates the type of delivery associated with this address. Returned for US addresses only.

* B - PO Box
* C - City delivery
* G - General delivery
* H - Highway contract
* R - Rural route

**TaxRegionId:** string  
AvaTax tax region identifier

**PostNet:** string [12]  
POSTNet is a 12-digit barcode containing the ZIP Code, ZIP+4 Code, and the delivery point code, used by the USPS to direct mail. Returned for US addresses only digits represent delivery information:

* 1-5 ZIP code
* 6-9 Plus4 code
* 10-11 Delivery point
* 12 Check digit

**ResultCode:** enum as string [see below]  
Classifies severity of message. One of:

* Success
* Error
* Warning
* Exception

**Messages:** <a href='#errors'>Message[]</a>
Human-readable description of any warning, error, or exception that occured.