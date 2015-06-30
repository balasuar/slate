## Companies
A company represents a single legal or reporting entity within an Account. An account may have many companies.
Note that if you have created an account with `POST /accounts`, a single default company profile has already been created on the account.

### Create a Company
#### Request
```shell
curl --include \
     --request POST \
     --header "Content-Type: application/json" \
     --header "Accept: application/json" \
     --header "Client: Agent X Connector v12" \
     --header "Authorization: Basic a2VlcG1vdmluZzpub3RoaW5nMnNlZWhlcmU=" \
     --@/Docs/company.json
     'https://onboarding.api.avalara.com/accounts/<accountId>/companies'
```

```json
{ 
 "Company": {
    "BIN":"123456789",
    "CompanyCode":"ABC44",
    "CompanyName":"Amalgamated Branding Co.",
    "TIN":"123456789",
    "CompanyContact": {
      "Email":"jim.smith44@amalgamatedbranding.com",
      "Fax":"555-555-1234",
      "FirstName":"Jim",
      "LastName":"Smith",
      "MobileNumber":"333-555-1234",
      "PhoneNumber":"800-555-1234 x222",
      "Title":"Comptroller"
    },
    "CompanyAddr":{
      "City":"Seattle",
      "Country":"US",
      "Line1":"1100 2nd Ave",
      "Line2":"Suite 300",
      "Line3":"ATTN: Accounting",
      "State":"WA",
      "Zip":"98101"
    }
  }
}
```
```xml
TBD
```


**BIN** string, *optional*  
The VAT registration ID for the business, if VAT registered.

**CompanyCode** string, *required*  
A user-defined identifier for the company profile. Must be unique within a single account.

**CompanyName** string, *required*  
The legal name of the company.

**TIN** string, *required*  
The tax registration number for the company. 

**CompanyAddr** streetAddress, *required*  
The primary address for the business.

**CompanyContact** companyContact, *required*  
The contact details for the user to be created.

##### CompanyAddr
This should reflect the primary business address for the company being created. It will be used as the company contact address, the address associated with the default location, and the starting nexus.

**City** string, *required*  
**Country** string, 2-character ISO country code, *required*  
**Line1** string, *required*  
**Line2** string, *optional*  
**Line3** string, *optional*  
**State** string, 2-character state/region code *required*  
**Zip** string, *required* 

##### CompanyContact

**Email** string, *required*  
A primary contact email for the company profile. This will also be the username assigned to the AccountAdmin-level user associated wiht the account.

**Fax** string, *optional*  
A contact fax for the company.

**FirstName** string, *required*  
The first name of the primary contact for the company.

**LastName** string, *required*  
The last name of the primary contact for the company.

**MobileNumber** string, *optional* 
A cell phone number for the primary contact for the company.
 
**PhoneNumber** string, *required*  
A main phone number fo the primary contact for the company.

**Title** string, *optional*  
The title of the primary contact for the company.

#### Response

```json
{
    "Message": "Company created successfully",
    "Result": {
        "__type": "Company:#AvaTaxSelfProcLib.Models",
        "BIN": "123456789",
        "CompanyAddr": {
            "City": "Seattle",
            "Country": "US",
            "Line1": "1100 2nd Ave",
            "Line2": "Suite 300",
            "Line3": "ATTN: Accounting",
            "State": "WA",
            "Zip": "98101"
        },
        "CompanyCode": "ABC",
        "CompanyContact": {
            "Email": "jim.smith44@amalgamatedbranding.com",
            "Fax": "555-555-1234",
            "FirstName": "Jim",
            "LastName": "Smith",
            "MobileNumber": "333-555-1234",
            "PhoneNumber": "800-555-1234 x222",
            "Title": "Comptroller"
        },
        "CompanyName": "Amalgamated Branding Co.",
        "TIN": "123456789"
    },
    "Status": "Success"
}
```
```xml
TBD
```
The response upon creating an account is the same as the request.


### Get a Company
```plaintext
GET https://onboarding.api.avalara.com/accounts/{accountId}/companies/{companyCode}
```

Retrieves the company details for a single specified company on an account.

#### Request
```shell
curl --include \
     --header "Accept: application/json" \
     --header "Client: Agent X Connector v12" \
     --header "Authorization: Basic a2VlcG1vdmluZzpub3RoaW5nMnNlZWhlcmU=" \
  'https://onboarding.api.avalara.com/accounts/<accountId>/companies/<companyCode>'
```
**AccountId** string, *required*
The AvaTax-assigned account number of the account that owns the company you would like to retrieve.

**CompanyCode** string, *required*  
The CompanyCode of the company you would like to retrieve.
 
#### Response
```json
{
    "Message": "Company fetched successfully",
    "Result": {
        "__type": "Company:#AvaTaxSelfProcLib.Models",
        "BIN": null,
        "CompanyAddr": {
            "City": "Seattle",
            "Country": "US",
            "Line1": "1100 2nd Ave",
            "Line2": "Suite 300",
            "Line3": "ATTN: Accounting",
            "State": "WA",
            "Zip": "98101"
        },
        "CompanyCode": "ABC",
        "CompanyContact": {
            "Email": "jim.smith44@amalgamatedbranding.com",
            "Fax": "555-555-1234",
            "FirstName": "Jim",
            "LastName": "Smith",
            "MobileNumber": "333-555-1234",
            "PhoneNumber": "800-555-1234 x222",
            "Title": "Comptroller"
        },
        "CompanyName": "Amalgamated Branding Co.",
        "TIN": "123456789"
    },
    "Status": "Success"
}
```
```xml
<GetCompanyResponse 
    xmlns="https://onboardingapi.avalara.com/DATA/V1" 
    xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <Message>Company fetched successfully</Message>
    <Result i:type="a:Company" 
        xmlns:a="http://schemas.datacontract.org/2004/07/AvaTaxSelfProcLib.Models">
        <a:BIN i:nil="true"></a:BIN>
        <a:CompanyAddr>
            <a:City>Seattle</a:City>
            <a:Country>US</a:Country>
            <a:Line1>1100 2nd Ave</a:Line1>
            <a:Line2>Suite 300</a:Line2>
            <a:Line3>ATTN: Accounting</a:Line3>
            <a:State>WA</a:State>
            <a:Zip>98101</a:Zip>
        </a:CompanyAddr>
        <a:CompanyCode>ABC</a:CompanyCode>
        <a:CompanyContact>
            <a:Email>jim.smith44@amalgamatedbranding.com</a:Email>
            <a:Fax>555-555-1234</a:Fax>
            <a:FirstName>Jim</a:FirstName>
            <a:LastName>Smith</a:LastName>
            <a:MobileNumber>333-555-1234</a:MobileNumber>
            <a:PhoneNumber>800-555-1234 x222</a:PhoneNumber>
            <a:Title>Comptroller</a:Title>
        </a:CompanyContact>
        <a:CompanyName>Amalgamated Branding Co.</a:CompanyName>
        <a:TIN>123456789</a:TIN>
    </Result>
    <Status>Success</Status>
</GetCompanyResponse>
```

Getting a company produces the same as the response format for <a href="#request156">creation of a company.</a>.
