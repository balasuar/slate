
## Nexus

Nexus tells the AvaTax calculation where the business entity is required to collect and remit taxes. If no nexus is selected for a given state, no taxes will be calculated for that state.

### Create Nexus
Adds all nexus jurisdictions triggered by an address. Note that companies created by calling `POST /accounts` start with nexus already designated for the address provided at that time - this method need only be used if additional nexus jurisdictions are required for this business.

#### Request
```shell
curl --include \
     --request POST \
     --header "Content-Type: application/json" \
     --header "Accept: application/json" \
     --header "Client: Agent X Connector v12" \
     --header "Authorization: Basic a2VlcG1vdmluZzpub3RoaW5nMnNlZWhlcmU=" \
     --@/Docs/nexus.json
     'https://onboarding.api.avalara.com/accounts/<accountId>/companies/<companyCode>/nexuses'
```


```json
{
  "NexusAddress":[
    {
    "Country": "US",
    "State": "TX"
    },
    {
    "Country": "US",
    "State": "WA"
    }
  ]
}
```

```xml
<CreateNexusRequest xmlns="https://onboardingapi.avalara.com/DATA/V1">
  <NexusAddress>
    <CompanyAddress xmlns="http://schemas.datacontract.org/2004/07/AvaTaxSelfProcLib.Models">
      <Country>US</Country>
      <State>CA</State>
    </CompanyAddress>
    <CompanyAddress xmlns="http://schemas.datacontract.org/2004/07/AvaTaxSelfProcLib.Models">
      <City>Portland</City>
      <Country>US</Country>
      <State>OR</State>
    </CompanyAddress>
  </NexusAddress>
</CreateNexusRequest>
```

##### CompanyAddress
This should reflect the primary address on which the nexus setting should be based.

**City** string, *optional*  
**Country** string, 2-character ISO country code, *required*  
**Line1** string, *optional*  
**Line2** string, *optional*  
**Line3** string, *optional*  
**State** string, 2-character state/region code *required*  
**Zip** string, *optional*  

#### Response

```xml
<CreateNexusResponse 
    xmlns="https://onboardingapi.avalara.com/DATA/V1" 
    xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <Message>Nexus created successfully</Message>
    <Result i:type="a:AvaTaxNexusInformation" 
        xmlns:a="http://schemas.datacontract.org/2004/07/AvaTaxSelfProcLib.Models">
        <a:CreatedNexus>
            <a:Nexus>
                <a:CompanyId>253105</a:CompanyId>
                <a:Country>US</a:Country>
                <a:EffDate>2014-06-30</a:EffDate>
                <a:EndDate>9999-12-31</a:EndDate>
                <a:ErrorIfAny i:nil="true"></a:ErrorIfAny>
                <a:JurisName>CALIFORNIA</a:JurisName>
                <a:JurisType>STA</a:JurisType>
                <a:LocalNexusType>Selected</a:LocalNexusType>
                <a:NexusId>10686240</a:NexusId>
                <a:NexusType>NonVolunteer</a:NexusType>
                <a:State>CA</a:State>
            </a:Nexus>
            <a:Nexus>
                <a:CompanyId>253105</a:CompanyId>
                <a:Country>US</a:Country>
                <a:EffDate>2014-06-30</a:EffDate>
                <a:EndDate>9999-12-31</a:EndDate>
                <a:ErrorIfAny i:nil="true"></a:ErrorIfAny>
                <a:JurisName>OREGON</a:JurisName>
                <a:JurisType>STA</a:JurisType>
                <a:LocalNexusType>Selected</a:LocalNexusType>
                <a:NexusId>10686241</a:NexusId>
                <a:NexusType>NonVolunteer</a:NexusType>
                <a:State>OR</a:State>
            </a:Nexus>
        </a:CreatedNexus>
    </Result>
    <Status>Success</Status>
</CreateNexusResponse>
```
```json
{
    "Message": "Nexus created successfully",
    "Result": {
        "__type": "AvaTaxNexusInformation:#AvaTaxSelfProcLib.Models",
        "CreatedNexus": [
            {
                "CompanyId": "253105",
                "Country": "US",
                "EffDate": "2014-06-30",
                "EndDate": "9999-12-31",
                "ErrorIfAny": null,
                "JurisName": "UNITED STATES",
                "JurisType": "CNT",
                "LocalNexusType": "Selected",
                "NexusId": 10686235,
                "NexusType": "NonVolunteer",
                "State": "US"
            },
            {
                "CompanyId": "253105",
                "Country": "US",
                "EffDate": "2014-06-30",
                "EndDate": "9999-12-31",
                "ErrorIfAny": null,
                "JurisName": "TEXAS",
                "JurisType": "STA",
                "LocalNexusType": "Selected",
                "NexusId": 10686236,
                "NexusType": "NonVolunteer",
                "State": "TX"
            },
            {
                "CompanyId": "253105",
                "Country": "US",
                "EffDate": "2014-06-30",
                "EndDate": "9999-12-31",
                "ErrorIfAny": null,
                "JurisName": "WASHINGTON",
                "JurisType": "STA",
                "LocalNexusType": "Selected",
                "NexusId": 10686237,
                "NexusType": "NonVolunteer",
                "State": "WA"
            }
        ]
    },
    "Status": "Success"
}

```

For each input address, there will be an array element representing the status outcome for that individual element.

**CompanyId** string  
The unique identifier of the company to which the nexus setting belongs.

**Country** string  
The two-character ISO code for the country in which the nexus jurisdiction is located.

**EffDate** string  
The date on which the nexus setting takes effect.

**EndDate** string  
The expiration date of the nexus setting.

**LocalNexusType** string  
Indicates the inheritance of local nexus, if appropriate. One of: Selected, StateAdministered, All

**JurisName** string  
The colloquial name of the jurisdiction. May not be unique.

**JurisType** string  
Indicates the level of the the nexus jurisdiction. One of CNT, CTY, CIT, STA, STJ

**NexusId** string  
The unique AvaTax assigned record Id for the nexus setting.

**NexusType** string  
One of Volunteer or Non-Volunteer. Indicates if Sales and Seller's use tax or just Sales Tax will be calcluated (respsectively).

**State** string, 2 characters  
The state in which the nexus jurisdiction is located. Note that for country level nexus this will be the country code.


### Get Nexus Settings
#### Request
```shell
curl --include \
     --header "Accept: application/json" \
     --header "Client: Agent X Connector v12" \
     --header "Authorization: Basic a2VlcG1vdmluZzpub3RoaW5nMnNlZWhlcmU=" \
  'https://onboarding.api.avalara.com/accounts/<accountId>/companies/<companyCode>/nexuses'
```
**AccountId** string, *required*
The AvaTax-assigned account number of the account that owns the company for which you would like to retrieve nexus.

**CompanyCode** string, *required*  
The CompanyCode of the company for which you would like to retrieve nexus.

#### Response

```xml
<GetNexusResponse 
    xmlns="https://onboardingapi.avalara.com/DATA/V1" 
    xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <Message>Nexus fetched successfully</Message>
    <Result i:type="a:AvaTaxNexusInformation" 
        xmlns:a="http://schemas.datacontract.org/2004/07/AvaTaxSelfProcLib.Models">
        <a:CreatedNexus>
            <a:Nexus>
                <a:CompanyId>253105</a:CompanyId>
                <a:Country>US</a:Country>
                <a:EffDate>2014-06-30</a:EffDate>
                <a:EndDate>9999-12-31</a:EndDate>
                <a:ErrorIfAny i:nil="true"></a:ErrorIfAny>
                <a:JurisName>UNITED STATES</a:JurisName>
                <a:JurisType>CNT</a:JurisType>
                <a:LocalNexusType>Selected</a:LocalNexusType>
                <a:NexusId>10686235</a:NexusId>
                <a:NexusType>NonVolunteer</a:NexusType>
                <a:State>US</a:State>
            </a:Nexus>
            <a:Nexus>
                <a:CompanyId>253105</a:CompanyId>
                <a:Country>US</a:Country>
                <a:EffDate>2014-06-30</a:EffDate>
                <a:EndDate>9999-12-31</a:EndDate>
                <a:ErrorIfAny i:nil="true"></a:ErrorIfAny>
                <a:JurisName>TEXAS</a:JurisName>
                <a:JurisType>STA</a:JurisType>
                <a:LocalNexusType>Selected</a:LocalNexusType>
                <a:NexusId>10686236</a:NexusId>
                <a:NexusType>NonVolunteer</a:NexusType>
                <a:State>TX</a:State>
            </a:Nexus>
            <a:Nexus>
                <a:CompanyId>253105</a:CompanyId>
                <a:Country>US</a:Country>
                <a:EffDate>2014-06-30</a:EffDate>
                <a:EndDate>9999-12-31</a:EndDate>
                <a:ErrorIfAny i:nil="true"></a:ErrorIfAny>
                <a:JurisName>WASHINGTON</a:JurisName>
                <a:JurisType>STA</a:JurisType>
                <a:LocalNexusType>Selected</a:LocalNexusType>
                <a:NexusId>10686237</a:NexusId>
                <a:NexusType>NonVolunteer</a:NexusType>
                <a:State>WA</a:State>
            </a:Nexus>
        </a:CreatedNexus>
    </Result>
    <Status>Success</Status>
</GetNexusResponse>
```
```json
{
    "Message": "Nexus fetched successfully",
    "Result": {
        "__type": "AvaTaxNexusInformation:#AvaTaxSelfProcLib.Models",
        "CreatedNexus": [
            {
                "CompanyId": "253105",
                "Country": "US",
                "EffDate": "2014-06-30",
                "EndDate": "9999-12-31",
                "ErrorIfAny": null,
                "JurisName": "UNITED STATES",
                "JurisType": "CNT",
                "LocalNexusType": "Selected",
                "NexusId": 10686235,
                "NexusType": "NonVolunteer",
                "State": "US"
            },
            {
                "CompanyId": "253105",
                "Country": "US",
                "EffDate": "2014-06-30",
                "EndDate": "9999-12-31",
                "ErrorIfAny": null,
                "JurisName": "TEXAS",
                "JurisType": "STA",
                "LocalNexusType": "Selected",
                "NexusId": 10686236,
                "NexusType": "NonVolunteer",
                "State": "TX"
            },
            {
                "CompanyId": "253105",
                "Country": "US",
                "EffDate": "2014-06-30",
                "EndDate": "9999-12-31",
                "ErrorIfAny": null,
                "JurisName": "WASHINGTON",
                "JurisType": "STA",
                "LocalNexusType": "Selected",
                "NexusId": 10686237,
                "NexusType": "NonVolunteer",
                "State": "WA"
            }
        ]
    },
    "Status": "Success"
}
``` 
Retrieving nexus produces the same as the response format for creating nexus.
