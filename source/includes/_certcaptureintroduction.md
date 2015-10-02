# CertCapture API

> Avalara recommends you have a solid understanding of RESTful APIs before reading this document, a great tutorial and walkthrough can be found <a href="http://www.restapitutorial.com/">here</a>.

The CertCapture API allows you to communicate with CertCapture 6.x and beyond. For documentation on deprecated versions, please see the <a href="https://documentation.certcapture.com/">V1 XML API</a>.

This API is designed so that if an error occurs you should get a reasonable worded response and an error code. If you see something odd, please don't hesitate to let us know at <a href="mailto:support@certcapture.com">support@certcapture.com</a>.
The endpoints defined here will not change, but the data output and input may be subject to minor changes.
All of the generated data provided in this documentation is automatically generated fake data and should only be used as a guide for how to use our API.

## Headers and URLs

### URLs

> https://api.certcapture.com/v2/

Production and testing environments are available, they both use a single URL.

### Authentication

> Authorization: Basic base64(username + ':' + password)

The CertCapture API uses http basic authentication. To get a username and password setup, contact your Customer Account Manager or email <a href="mailto:support@certcapture.com">support@certcapture.com</a>.

### ClientIds

```plaintext
x-client-id: 99
x-client-ids: [1,2,3,99]
```

To access specific client id or multiple client IDs that you have access to, pass the `x-client-id` or `x-client-ids` header. To find your client ID, go to Company Settings -> Company Details in the CertCapture portal.

**NOTE:** Multiple client Ids are only available for GET requests

### Cross Origin Resource Sharing
The CertCapture API supports CORS. Feel free to connect to it from your own domain.


## Key Fields and Data Practices

### Customer Numbers
> /v2/customers/1

By default, the CertCapture API uses our internal ID's for Customer identifiers. In the example to the right, `1` refers to our internal ID for Customer 1.

> x-customer-primary-key: customer_number
> /v2/customers/123abc

If you wish to use the customer_number instead, simply provide the additional header to specify the customer primary key. That allows you to access the customer end points with your defined customer number.

**Note:** Since we support all utf8 characters in the customer_number, the customer_number **MUST** be sent url encoded. For example, if your customer_number is `123/abc`, you would need to call `/v2/customers/123%2Fabc`. If the customer_number is **not** url encoded, e.g. `/v2/customers/123/abc`, you will get a `Customer Not Found` error.

### Filtering 

##### Format
> ?filter=[["id","=",5],["name","=","my name"]]

When accessing a collection, you are able to filter on any field that is shown in the results using this format: `[[FIELD, OPERATOR, VALUE], [FIELD, OPERATOR, VALUE]]`

##### Operators
The following operators are also available, but limited to the field type you are searching on. For example you cannot use `<` with a boolean field. `"=", "<", ">","=<", "=>", "LIKE", "ILIKE", "<>"`

##### Booleans
Filtering by booleans is available with the following case insensitive values: `"yes", "y", "1", "true", 1, true, "false", "no", "n", "0", 0, false`

##### URL Encoding
In some cases URL encoding may be required to make sure the filter JSON is valid.
For example, `?filter=[["name","=","Bob & Nicks Emporium"]]` will cause an `Invalid JSON` error. Encoding the `&` is required: `?filter=[["name","=","Bob %26 Nicks Emporium"]]`

##### Filtering on Null
Filtering by `""` can sometimes cause a PDO error: `?filter=[["calc_id","=",""]]`
The solution is to change from an empty string to `null` value without quotes, i.e. `?filter=[["name","=","Bob %26 Nicks Emporium"]]`

##### Filtering on Relationships
Filtering based on expanded relationships is also available: `?filter=[["relationship.name", "=", "value"]]`

**Note:** NOTE: All of the expanded relationship filters are custom set white listed filters, if you feel you should be able to filter on something but can't, let us know at <a href="mailto:support@certcapture.com">support@certcapture.com</a>.

### Relationships and Saving Data

The CertCapture API has the ability to save or attach related data whenever you do a `POST` or `PUT` request. The way the save is handled is based of what type of relationship occurs between the data (we will get to this later).

##### Associating Related Data

```plaintext
    PUT /v2/exposure-zones/1/
```
```json
	{
        "country": {
            "id": 1,
            "name": "United States",
            "initials": "US"
        }
    }
```

> Both of the below requests are also valid, and would have the same effect:


```json
	{
        "country": {
            "id": 1
        }
    }
```
> Or

```json
	{
        "country": {
            "name": "United States",
            "initials": "US"
        }
    }
```

An association can be created through a `PUT` to the correct resource.

This example would update `Exposure Zone 1` to have the country `United States`. As long as the below criteria is met:

1. The `country` relationship is a valid for the current model and it's not a `read only` relationship.
2. The `country` data provided is valid and exists.

(`United States` exists with `id` of `1` and `initials` of `US`.)

CertCapture will look at **ALL** the data provided for `country` and see if it can find a single matching result, before assigning it to an `Exposure Zone`.

#### Unassociating Related Data

 ```plaintext
    PUT /v2/exposure-zones/1/
 ```
 ```json
    {
        "country": null
    }
```

> Or

```plaintext
    PUT /v2/exposure-zones/1/
```
```json
    {
        "country":
    }
```
To remove an existing data relationship, simply pass that relationship with `null`

**NOTE:** Removing an association will _NOT_ remove the related entity.

#### Associating Non-Existent Data
If you wish to associate a relationship with something that doesn't exist yet, the API call will fail. You will need to create it manually via the API endpoint, then do the association.

**NOTE:** This is not the case for **One to Many** relationships. **One to Many** relationships will ALWAYS create a new entity before associating it.

#### Associated _Many_ Relationships
Some relationships are not able to be modified via a `POST` or `PUT` request on a normal resource. These are usually for relationships that are **One to Many** or **Many to Many** and there are specific API endpoints to handle them.

##### One to Many
Associating an entity with a one to many relationship:

    PUT
    URL: /v2/customers/1/log/
    DATA: {
        "logs": [{
            "account": "Account Name",
            "entry": "Updated customer Information"
        }]
    }

The above request would **CREATE** a log for `Customer 1`, as long as the below criteria is met:

1. Each `log` data provided is valid.

Removing a many to many entity association:

    DELETE
    URL: /v2/customers/1/log/
    DATA: {
        "logs": [{"id": 10}]
    }
The above request would **DELETE** the `Log`, as long as the below criteria is met:

1. The `log` data provided is valid and the relationship exists.

##### Many to Many
Associating an entity with a many to many relationship:

    PUT
    URL: /v2/certificates/1/customers/
    DATA: {
        "customers": [{"id": 10},{"id": 20}]
    }
The above request would associate `Customer 10` and `Customer 20` with `Certificate 1`, as long as the below criteria is met:

1. Each `customer` data provided is valid and exists.

Removing a many to many entity association:

    DELETE
    URL: /v2/certificates/1/customers/
    DATA: {
        "customers": [{"id": 10}]
    }
The above request would remove the associate of `Customer 10` with `Certificate 1`, as long as the below criteria is met:

1. The `customer` data provided is valid and the relationship exists.

**NOTE:** Removing an association will _NOT_ remove the related entity.

##### Many to Many Pivot Data
Some Many to Many relationships have pivot data, E.G. `Customer 1` has a `Custom Field 10` with a `value` of `custom field value`

If you wish to update the value of that, simply do the same action as you would if you were assigning a Many to Many relationship, and pass in the updated `value` field.

    PUT
    URL: /v2/customers/1/custom-fields/
    DATA: {
        "custom_fields": {"id": 10, "value":"update my customer custom field value!"}
    }

## Example Scenarios
Below are some examples of some REST API scenarios

### Common Scenarios

[Example REST API Scenarios](https://documentation.certcapture.com/img/example_rest_apis.png "Example Rest API")

### Sending Requests

[Example REQUEST API Scenarios](https://documentation.certcapture.com/img/example_rest_apis_requests.png "Example Rest API Requests")

## Error Messages
```plaintext
400 Bad Request
```
```json
    {
        "success": false,
        "code": "2005",
        "error": "I am an error message"
    }
```

`success=false` is fairly self explanatory. You will see this whenever there is any type of error.

The `code` is for internal use only, but please provide this value whenever contacting support.

The most important value is the `error` string as this should provide a nice verbose message to help diagnose what went wrong with your request.

### HTTP Status Codes
Below is a list of various actions and the HTTP Response Status Codes you are likely to see:

| Action        | HTTP Code     |
| ------------- |--------------:|
| Valid request, processed synchronously | 200 OK |
| Valid request where no content is expected | 204 No Content |
| Resource no longer exists at that location | 301 Moved Permanently |
| Request with missing required fields | 400 Bad request |
| Request with invalid values | 400 Bad request |
| Request without Auth header | 401 Unauthorized |
| Request with incorrect Auth content/key | 401 Unauthorized |
| Resource does not exist | 404 Not Found |
| Invalid method sent to resource (e.g. PUT where only GET is permitted) | 405 Method Not Allowed |
| Service is down | 503 Service unavailable |
| Internal server error | 503 Service unavailable |


## Frequently Asked Questions

**Question:** How can I just play?

Once you are setup, there are two ways to play and test your CertCapture API

    Follow the code examples provided below for your choice of language.

    Or install one of these free Browser Add-ons:

[Advanced Rest for Chrome](https://chrome.google.com/webstore/detail/advanced-rest-client/hgmloofddffdnphfgcellkdfbfbjeloo?hl=en-US)

[Postman for Chrome](https://chrome.google.com/webstore/detail/postman-rest-client-packa/fhbjgbiflinjbdggehcddcbncdddomop?hl=en)

[RESTClient for Firefox](https://addons.mozilla.org/en-US/firefox/addon/restclient/)

**Question:** I keep getting a 401 error!

    Make sure you:
    1) Have an API account setup and tied to your Avalara CertCapture user account
    2) Are base64 encoding your username:password and sending it as HTTP Basic access authentication.

[See Credentials](#credentials).

**Question:** Do I have to provide all the information when creating or associating a related model?

    No, provide just enough information to find a unique instance. IE: You can provide State with {"initials":"NC"}

**Question:** I am getting this error: "Unable to find user company details"

    Make sure you have access to the client ID you are passing as x-client-id

**Question:** Still not working!

    Sometimes requests don't follow the 302 http redirect so remove the trailing slash from the URL. IE /v2/certificates instead of /v2/certificates/

**Question:** I keep getting "error": "Related data not found in request, must be one of: [\"X\"]"

    Make sure you are POST/PUT with Content-Type application/x-www-form-urlencoded

**Question:** I'm still getting "error": "Related data not found in request, must be one of: [\"X\"]"

    Make sure you are using snake_case


 
