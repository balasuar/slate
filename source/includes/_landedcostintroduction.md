# Landed Cost API 

Landed Cost API provides duty rates, duty calculations and item harmonization information through a RESTful API. 

<aside class="alert"> This API is currently in beta release only. To obtain an account and API Access Key, please contact Avalara directly. </aside>

## Authentication

```plaintext
Authorization: avalaraapikey id:<Your Account Id> key:<Your API Key>
```
All API requests must be accompanied by an API Access Key. During account provisioning, you will be issued an API Key which you must supply with every request. To authenticate your requests, set the HTTP Authorization Header, including both your Account Id and API Key.

### General Notes

#### Timestamps
```plaintext
e.g.: 2015-06-12T09:17:37Z
```
Timestamps should be formatted using ISO-8601 to the nearest second, in UTC.

#### Expiries

All requests will have an associated timestamp. The validity for any request is one minute to account for any clock-skew. 

