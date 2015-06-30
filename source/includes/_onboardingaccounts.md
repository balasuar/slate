## Accounts
An account represents a single AvaTax client. Note that a single account may have multiple company profiles, each representing a single legal entity under the single AvaTax client contract.

### Create an Account
```plaintext
POST https://onboarding.api.avalara.com/v1/accounts
```
This resource creates an account with a functional but minimal company profile setup. It creates a single account with: 

- one Account Admin-level user
- one default company profile
- one defined location
- nexus designated for the single location

#### Request

```shell
curl --include \
     --request POST \
     --header "Content-Type: application/json" \
     --header "Accept: application/json" \
     --header "Client: Agent X Connector v12" \
     --header "Authorization: Basic a2VlcG1vdmluZzpub3RoaW5nMnNlZWhlcmU=" \
     --@/Docs/account.json
     'https://onboarding.api.avalara.com/v1/accounts'
```

```json
{ 
  "ProductRatePlan":[ 
      "ZT - 500 - Pro - Monthly",
      "ZT - 500 - Pro (Usage)",
      "ZT - Pay As You Go"
  ],
  "ConnectorName":"QuickBooks Online",
  "CampaignId":"70141000001LVUZ",
  "LeadSourceMostRecent":"test",
  "EffDate":"2015-01-01",
  "EndDate":"2018-04-12",
  "Company": {
  	"BIN":"0123456789",
  	"CompanyCode":"ABC",
  	"CompanyName":"Amalgamated Branding Co.",
    "TIN": "0123456789",
    "CompanyContact": {
    	"Email":"jim.smith@amalgamatedbranding.com",
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
**ProductRatePlans** array of ProductRatePlan string, *required*  
Rate plans to be used for the account. This is an Avalara-specific value that determines at what billable rate the client will be charged. For free trial accounts, only a single array element is required (e.g. "SDK - Free Trial - Non-Developer"). For paid accounts, two array elements are expected: one to describe the standard rate plan and one to describe the overage rate plan.  Possible rate plan combinations are:

- "QBOSC - 300 -  Pro - Annual", "QBOSC - 300 - Pro (Usage)"
- "QBOSC - 300 -  Pro - Monthly", "QBOSC - 300 - Pro (Usage)"
- "QBOSC - 1000 -  Pro - Annual", "QBOSC - 1000 - Pro (Usage)"
- "QBOSC - 1000 -  Pro - Monthly", "QBOSC - 1000 - Pro (Usage)"
- "QBOSC - 3000 -  Pro - Annual", "QBOSC - 3000 - Pro (Usage)"
- "QBOSC - 3000 -  Pro - Monthly", "QBOSC - 3000 - Pro (Usage)"

A third element may be included for paid accounts to indicate filing services ("QBOSC Pay As You Go").

**ConnectorName** string, *required*  
The connector that will be the primary method of access used to call the account created.

**CampaignId** string, *required*  
SalesForce campaign ID under which the new account is being created. This is provided per connector by Avalara.

**LeadSourceMostRecent** string, *required*  
Most recent lead source; will associate the specified Avalara-internal SalesForce record for the newly created account.

**EffDate** string, *required*  
The date on which the account should take effect.

**EndDate** string, *required*  
The date on which the account should expire. This can be changed at a later time if the account is renewed.

**Company** company, *required*  
The company details for the company to be created.

##### Company

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

```plaintext
200 OK
```

```json
{
    "Message": "Account created successfully!\n\rUser created successfully!\n\rCompany created successfully!\n\rLocation created successfully!\n\rNexus created successfully!\n\r",
    "Result": {
        "__type": "AccountSubscription:#AvaTaxSelfProcLib.Models",
        "AccountId": "1100170105",
        "CampaignId": "70141000001LVUZ",
        "Company": {
            "BIN": "",
            "CompanyAddr": {
              "City":"Seattle",
              "Country":"US",
              "Line1":"1100 2nd Ave",
              "Line2":"Suite 300",
              "Line3":"ATTN: Accounting",
              "State":"WA",
              "Zip":"98101"
            },
            "CompanyCode": "ABC",
            "CompanyContact": {
              "Email":"jim.smith@amalgamatedbranding.com",
              "Fax":"555-555-1234",
              "FirstName":"Jim",
              "LastName":"Smith",
              "MobileNumber":"333-555-1234",
              "PhoneNumber":"800-555-1234 x222",
              "Title":"Comptroller"
            },
            "CompanyName":"Amalgamated Branding Co.",
            "TIN":"0123456789"
        },
        "ConnectorName": "QuickBooks Online",
        "EffDate": "2014-04-12",
        "EndDate": "2018-04-12",
        "LeadSourceMostRecent": "test",
        "LicenseKey": "4ADE973B1671EFFB",
        "ProductRatePlans": [
            "ZT - 500 - Pro - Monthly",
            "ZT - 500 - Pro (Usage)",
            "ZT - Pay As You Go"
        ],
        "User": {
            "TempPwd": "xhXH63-@",
            "UserName": "jim.smith@amalgamatedbranding.com"
        }
    },
    "Status": "Success"
}
```

```xml
TBD
```

The response upon creating an account is the same as the request, with some additional parameters:

NOTE: If there's a better name for the root element in the XML form, great.

**Errors** array of output elements  
Provides debug information on the account creation process. Because multiple operations are performed, there may be multiple array elements (instead of a single, root-level element). For more information on the format of these elements, and an example, see the Errors section. Note that this element will only be included in the response if errors occurred during processing.

**AccountId** string  
The AvaTax-assigned account id for the newly created company.

**LicenseKey** string  
The license key for the account - this value should be saved to authenticate subsequent tax calculation calls.

**TempPwd** string  
The temporary password associated with the primary Account Admin user.

**UserName** string  
The username associated with the primary Account Admin user.


### Get an Account
```plaintext
GET https://onboarding.api.avalara.com/v1/accounts/{accountId}
```
<aside class="warning"> NOTE: It looks like this has the SOAP filters hardcoded to leave out Company and User data, and the access level doesn't allow subscription information to be shown, which leaves this call pretty meaningless? Is there a particular use case you're addressing with this? Or can we change the default filters to include Company and User data on the response? </aside>

Retrieves the account details for a single specified account.

#### Request
```shell
curl --include \
     --header "Accept: application/json" \
     --header "Client: Agent X Connector v12" \
     --header "Authorization: Basic a2VlcG1vdmluZzpub3RoaW5nMnNlZWhlcmU=" \
  'https://onboarding.api.avalara.com/accounts/1100012345'
```
**AccountId** string, *required*
The AvaTax-assigned account number of the account you would like to get.

#### Response

```json
{
    "Message": "Account fetched successfully",
    "Result": {
        "__type": "AvaTaxAccountInformation:#AvaTaxSelfProcLib.Models",
        "AccountId": "1100012345",
        "AccountName": "Innovative Mattress Solutions",
        "AccountStatus": "Active",
        "EffDate": "2014-06-28",
        "EndDate": "2114-06-28"
    },
    "Status": "Success"
}
```
```xml
<GetAccountResponse 
    xmlns="https://onboardingapi.avalara.com/DATA/V1" 
    xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <Message>Account fetched successfully</Message>
    <Result i:type="a:AvaTaxAccountInformation" 
        xmlns:a="http://schemas.datacontract.org/2004/07/AvaTaxSelfProcLib.Models">
        <a:AccountId>1100012345</a:AccountId>
        <a:AccountName>Innovative Mattress Solutions</a:AccountName>
        <a:AccountStatus>Active</a:AccountStatus>
        <a:EffDate>2014-06-28</a:EffDate>
        <a:EndDate>2114-06-28</a:EndDate>
    </Result>
    <Status>Success</Status>
</GetAccountResponse>

```

**accountId** string  
The AvaTax-assigned account id for the newly created company.

**accountName** string  
The company name associated with the account.

**accountStatus** string  
The status of the account. One of: Inactive, Active, Test, New

**effDate** string  
The effective date of the account.

**endDate** string  
The expiration date of the account.