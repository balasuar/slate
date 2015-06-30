
## Locations
Locations belong to a specific company profile and represent physical locations associated with the business, for example, office locations, retail locations, or warehouses. Locations are uniquely identified by the user-defined LocationCode within the context of their parent company. 

### Create a Location
Allows for the creation of one or more locations associated with a single company profile. Note that if the account/company was created with `POST /accounts`, a default location has already been created for the initial company. 

#### Request
```shell
curl --include \
     --request POST \
     --header "Content-Type: application/json" \
     --header "Accept: application/json" \
     --header "Client: Agent X Connector v12" \
     --header "Authorization: Basic a2VlcG1vdmluZzpub3RoaW5nMnNlZWhlcmU=" \
     --@/Docs/locations.json
     'https://onboarding.api.avalara.com/accounts/<accountId>/companies/<companyCode>/locations'
```

```json
{ "companyLocations": [
{    
     "City":"Bainbridge Island",
     "Country":"US",
     "Line1":"9, Winslow way",
     "Line2":"",
     "Line3":"",
     "State":"WA",
     "Zip":"98110",
     "AddressCategory":"MAINOFFICE",
     "AddressType":"LOCATION",
     "Description":"Testing",
     "EndDate":"05-31-2016",
     "IsDefault": true,
     "LocationCode":"Loc1",
     "StartDate":"05-31-2014"
},
{
     "City":"Seattle",
     "Country":"US",
     "Line1":"15, Main Road",
     "Line2":"",
     "Line3":"",
     "State":"WA",
     "Zip":"98110",
     "AddressCategory":"WAREHOUSE",
     "AddressType":"LOCATION",
     "Description":"Testing",
     "EndDate":"05-31-2017",
     "IsDefault": false,
     "LocationCode":"Loc2",
     "StartDate":"05-31-2014"
}]}
```
```xml
TBD
```
**City** string, *required*  
The city where the location is located.

**Country** string, *required*  
The country where the location is located.

**Line1** string, *required*  
The first line of the address of the location.

**Line2** string, *optional*  
The second line of the address of the location.

**Line3** string, *optional*  
The third line of the address of the location.

**State** string, *required*  
The state of the address of the location.

**Zip** string, *required*  
The zip or postal code of the location.

**AddressCategory** string, *required*  
A human-readable indicator of the address category.

**AddressType** string, *required*  
A human-readable indicator of the address type.

**Description** string, *required*  
A description of the location.

**EndDate** datetime, *required*  
The expiration date of the record.

**IsDefault** boolean, *required*
Indicates if the location is the default location for the company.

**LocationCode** string, *required*  
The company-wide unique, user defined identifier of the location.

**StartDate** datetime, *required*  
The effective date of the location record.

#### Response
```json
{
    "Message": "Location created successfully",
    "Result": {
        "__type": "AvaTaxCompanyLocation:#AvaTaxSelfProcLib.Models",
        "CompanyLocations": [
            {
                "City": "Bainbridge Island",
                "Country": "US",
                "Line1": "9, Winslow way",
                "Line2": "",
                "Line3": "",
                "State": "WA",
                "Zip": "98110",
                "AddressCategory": "MAINOFFICE",
                "AddressType": "LOCATION",
                "Description": "Testing",
                "EndDate": "05-31-2016",
                "ErrorIfAny": "",
                "IsDefault": "true",
                "LocationCode": "Loc1",
                "LocationId": "87626",
                "StartDate": "05-31-2014"
            },
            {
                "City": "Seattle",
                "Country": "US",
                "Line1": "15, Main Road",
                "Line2": "",
                "Line3": "",
                "State": "WA",
                "Zip": "98110",
                "AddressCategory": "WAREHOUSE",
                "AddressType": "LOCATION",
                "Description": "Testing",
                "EndDate": "05-31-2017",
                "ErrorIfAny": "",
                "IsDefault": "false",
                "LocationCode": "Loc2",
                "LocationId": "87627",
                "StartDate": "05-31-2014"
            }
        ]
    },
    "Status": "Success"
}
```
```xml
TBD
```
For each input location, there will be an array element representing the status outcome for that individual element. Note that each element is evaluated individually, so some may succeed and others may fail. The response upon creating an account is the same as the request, with one additional parameter:

**LocationId** string  
The unique, Avatax-assigned LocationId of the created location. 

<aside class="warning"> NOTE: I assume this is the value in the curent return payload?</aside>


### Get a Location
Retrieves a single specified location entry.

```
GET https://onboarding.api.avalara.com/accounts/<accountId>/companies/<companyCode>/locations/<locationCode>
```

#### Request
```shell
curl --include \
     --header "Accept: application/json" \
     --header "Client: Agent X Connector v12" \
     --header "Authorization: Basic a2VlcG1vdmluZzpub3RoaW5nMnNlZWhlcmU=" \
  'https://onboarding.api.avalara.com/accounts/1234567890/companies/ABC/locations/Loc1'
```
**AccountId** string, *required*
The AvaTax-assigned account number of the account that owns the company and location you would like to retrieve.

**CompanyCode** string, *required*  
The CompanyCode of the company that owns the location you would like to retrieve.

**LocationCode** string, *required*
The LocationCode of the location you would like to retrieve.

#### Response
```plaintext
200 (OK)
Content-Type: application/json
```
```json
{
    "Message": "Location fetched successfully",
    "Result": {
        "__type": "AvaTaxCompanyLocation:#AvaTaxSelfProcLib.Models",
        "CompanyLocations": [
            {
                "City": "Bainbridge Island",
                "Country": "US",
                "Line1": "9, Winslow way",
                "Line2": "",
                "Line3": "",
                "State": "WA",
                "Zip": "98110",
                "AddressCategory": "MAINOFFICE",
                "AddressType": "LOCATION",
                "Description": "",
                "EndDate": "2016-05-31",
                "ErrorIfAny": null,
                "IsDefault": "True",
                "LocationCode": "Loc1",
                "LocationId": "87626",
                "StartDate": "2014-05-31"
            }
        ]
    },
    "Status": "Success"
}
```
```xml
<GetLocationResponse 
    xmlns="https://onboardingapi.avalara.com/DATA/V1" 
    xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <Message>Location fetched successfully</Message>
    <Result i:type="a:AvaTaxCompanyLocation" 
        xmlns:a="http://schemas.datacontract.org/2004/07/AvaTaxSelfProcLib.Models">
        <a:CompanyLocations>
            <a:CompanyLocation>
                <a:City>Bainbridge Island</a:City>
                <a:Country>US</a:Country>
                <a:Line1>9, Winslow way</a:Line1>
                <a:Line2></a:Line2>
                <a:Line3></a:Line3>
                <a:State>WA</a:State>
                <a:Zip>98110</a:Zip>
                <a:AddressCategory>MAINOFFICE</a:AddressCategory>
                <a:AddressType>LOCATION</a:AddressType>
                <a:Description></a:Description>
                <a:EndDate>2016-05-31</a:EndDate>
                <a:ErrorIfAny i:nil="true"></a:ErrorIfAny>
                <a:IsDefault>True</a:IsDefault>
                <a:LocationCode>Loc1</a:LocationCode>
                <a:LocationId>87626</a:LocationId>
                <a:StartDate>2014-05-31</a:StartDate>
            </a:CompanyLocation>
        </a:CompanyLocations>
    </Result>
    <Status>Success</Status>
</GetLocationResponse>
```
##### AvaTaxCompanyInformation  
Getting a company produces the same as the request format for <a href="#request163">creation of a location.</a>.