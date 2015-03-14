## EstimateTax

Retrieves tax rate details for the supplied geographic coordinates and sale amount.
Since the REST API does not provide an explicit ping function, this method can also be used to test connectivity to the service.

##### URL and Method

Development: `GET https://development.avalara.net/1.0/tax/<location>/get?<saleamount>`  
Production: `GET https://avatax.avalara.net/1.0/tax/<location>/get?<saleamount>`
    
<aside class='notice'>
    To get an XML response, use `GET /1.0/tax/<location>/get.xml?<saleamount>`
</aside>

##### Headers

**Authorization:** header, *required*  
In the format "Basic [account number]:[license key]" encoded to <a href="http://en.wikipedia.org/wiki/Base64" target="_parent">Base64</a>, as per <a href="http://en.wikipedia.org/wiki/Basic_access_authentication" target="_parent">basic access authentication</a>.  
e.g.: `Basic a2VlcG1vdmluZzpub3RoaW5nMnNlZWhlcmU=`

### EstimateTax Request

```shell
curl --user 1234567890:A1B2C3D4E5F6G7H8 \
"https://development.avalara.net/1.0/tax/47.627935,-122.51702/get?saleamount=10"
```

```java
Double latitude = 47.627935;
Double longitude = -122.51702;
Double saleAmount = 10.0;
String queryparams = address.toQuery();
String taxest = svcURL+ "/1.0/tax/" + latitude.toString() + "," + longitude.toString() + "/get?saleamount=" + saleAmount.toString();
URL url;

HttpURLConnection conn;

//Connect to specified URL 
//with authorization header
url = new URL(taxest);
conn = (HttpURLConnection)url.openConnection();

//Create auth content
String encoded = "Basic " + new String(Base64.encodeBase64((accountNumber + ":"+licenseKey).getBytes()));

//Add authorization header
conn.setRequestProperty ("Authorization", encoded);
conn.disconnect();

//Deserialization object
ObjectMapper mapper = new ObjectMapper();
ValidateResult vres = mapper.readValue(conn.getInputStream(),ValidateResult.class);
```

```csharp
decimal latitude = (decimal)47.627935;
decimal longitude = (decimal)-122.51702;
decimal saleAmount = (decimal)10;

Uri address = new Uri(svcURL + "tax/" + latitude.ToString()+ "," + longitude.ToString() + "/get.xml?saleamount=" + saleAmount);
HttpWebRequest request = WebRequest.Create(webAddress) as HttpWebRequest;
request.Headers.Add(HttpRequestHeader.Authorization, "Basic " + Convert.ToBase64String(ASCIIEncoding.ASCII.GetBytes(accountNum + ":" + license)));
request.Method = "GET";

WebResponse response = request.GetResponse();
```

```php
<?php
$latitude = 47.627935;
$longitude = -122.51702;
$saleAmount = 10;

$estimateTaxRequest = new EstimateTaxRequest($latitude, $longitude, $saleAmount);
 
$url =  $this->config['url'].'/1.0/tax/' . $estimateTaxRequest->getLatitude() . "," . $estimateTaxRequest->getLongitude() . '/get?saleamount=' . $estimateTaxRequest->getSaleAmount();
$curl = curl_init();
curl_setopt($curl, CURLOPT_HTTPAUTH, CURLAUTH_BASIC);
curl_setopt($curl, CURLOPT_USERPWD, $this->config['account'] . ":" . $this->config['license']);
curl_setopt($curl, CURLOPT_URL, $url);
curl_setopt($curl, CURLOPT_RETURNTRANSFER,	1);

$curl_response = curl_exec($curl);

EstimateTaxResult::parseResult($curl_response);  
?>    
```

**Latitude:** decimal, *required*  
The latitude of the geographic coordinates to get tax for based on the sale amount

**Longitude:** decimal, *required*  
The longitude of the geographic coordinates to get tax for based on the sale amount

**SaleAmount:** decimal, *required*  
The amount of sale requiring tax calculation, in decimal format

### EstimateTax Result

```json
{
"Rate": 0.087,
"Tax": 0.87,
"ResultCode": "Success",
"TaxDetails": [
        {
            "Country": "US",
            "Region": "WA",
            "JurisType": "State",
            "Rate": 0.065,
            "Tax": 0.65,
            "JurisName": "WASHINGTON",
            "TaxName": "WA STATE TAX"
        },
        {
            "Country": "US",
            "Region": "WA",
            "JurisType": "City",
            "Rate": 0.022,
            "Tax": 0.22,
            "JurisName": "BAINBRIDGE ISLAND",
            "TaxName": "WA CITY TAX"
        }
    ]
}

```

Output for EstimateTax showing the retrieved tax details and calculation.

**Rate:** decimal  
Total effective tax rate

**Tax:** decimal  
Total calculated tax amount

**TaxDetails:** <a href='#taxdetail'>TaxDetail[]</a>  
Tax calculation details for each jurisdiction.

**ResultCode:** enum as string [see below]  
Classifies severity of message. One of:

* Success
* Error
* Warning
* Exception

**Messages:** <a href='#errors'>Message[]</a>
Human-readable description of any warning, error, or exception that occured.

#### TaxDetail

Tax details by jurisdiction.

**Country:** string [2]  
Country of tax jurisdiction

**JurisName:** string [200]  
Name of tax jurisdiction

**JurisType:** string [9]  
Regional type of tax jurisdiction

**Rate:** decimal  
Effective tax rate for tax jurisdiction

**Region:** string [3]  
Region of tax jurisdiction

**Tax:** decimal  
Tax amount

**TaxName:** string [75]  
Tax name