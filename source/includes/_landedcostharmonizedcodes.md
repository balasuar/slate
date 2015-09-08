## Harmonized Codes

### Browse Harmonized Codes

Presents the all available Harmonized Codes as a browseable tree. Each request specifies a parent node, and the response lists all child nodes of that parent. If no parent node is specified, all root-level nodes will be returned.

#### Request
```plaintext
GET http://sandbox.landedcost.api.avalara.com/v2/browse?system=HTS&parent=HS_93
```

**system** string, optional  
The classification system you want to browse. Must be one of:

- TARIC 
- SCHEDULEB
- HTS

**parent** string, optional  
The name of the parent node. Note that it is important to use the *name* of the node, as not all nodes have a harmonized code, and the code itself is different than the name.

#### Response
```plaintext
200
Content-Type: application/json
```
```json
[
  {
    "hs_code": "9301",
    "description": "Military weapons, other than revolvers, pistols and the arms of heading 9307",
    "name": "HS_9301"
  },
  {
    "hs_code": "9302",
    "description": "Revolvers and pistols, other than those of heading 9303 or 9304",
    "name": "HS_9302"
  },
  {
    "hs_code": "9303",
    "description": "Other firearms and similar devices which operate by the firing of an explosive charge (for example, sporting shotguns and rifles, muzzle-loading firearms, Very pistols and other devices designed to project only signal flares, pistols and revolvers for firing blank ammunition, captive-bolt humane killers, line-throwing guns)",
    "name": "HS_9303"
  },
  {
    "hs_code": "9304",
    "description": "Other arms (for example, spring, air or gas guns and pistols, truncheons), excluding those of heading 9307",
    "name": "HS_9304"
  },
  {
    "hs_code": "9305",
    "description": "Parts and accessories of articles of headings 9301 to 9304",
    "name": "HS_9305"
  },
  {
    "hs_code": "9306",
    "description": "Bombs, grenades, torpedoes, mines, missiles and similar munitions of war and parts thereof; cartridges and other ammunition and projectiles and parts thereof, including shot and cartridge wads",
    "name": "HS_9306"
  },
  {
    "hs_code": "9307",
    "description": "Swords, cutlasses, bayonets, lances and similar arms and parts thereof and scabbards and sheaths therefor",
    "name": "HS_9307"
  }
]
```

**hs_code** string  
The harmonized code.

**description** string  
The human-readable description of the classification.

**name** string  
The name of the node; this can be used to find the child nodes.

### Search Harmonized Codes

<aside class="alert"> This method is currently in alpha release only. As such, it may be changed without notice. Please plan accordingly. </aside>

Given an item description, returns a set of harmonized codes, and a non-normalized score that indicates how close the computer thinks this match is to the actual answer.

#### Request
```plaintext
GET http://sandbox.landedcost.api.avalara.com/v2/search?term=swords&source=DE&destination=US&type=import
```

**term** string, required  
A product description

**type** string, required  
The type of transaction. Must be one of `import`, `export`

**source** string, optional  
The country you are shipping from. Required if the `type` is `export`

**destination** string, required  
The country you are shipping to.

#### Response
```plaintext
200
Content-Type: application/json
```
```json
{
  "id": "651b8804-4d1e-4550-aee0-1b01d591688b",
  "results": [
    {
      "node": "HS_9307",
      "description": "Swords, cutlasses, bayonets, lances and similar arms and parts thereof and scabbards and sheaths therefor",
      "score": "9.5349",
      "reason": "saved / saved / saved / saved / saved",
      "system": "HS",
      "hs_leafs": "HS_9307",
      "all_leafs": "HS_9307"
    },
    {
      "node": "HTS_0106900110",
      "description": "Worms",
      "score": "0.5227",
      "reason": "freebase / freebase / freebase / freebase / tree attributes",
      "system": "HTS",
      "hs_leafs": "HS_010690",
      "all_leafs": "HTS_0106900110"
    },
    {
      "node": "HTS_9504300010",
      "description": "Video",
      "score": "0.5000",
      "reason": "freebase",
      "system": "HTS",
      "hs_leafs": "HS_950430",
      "all_leafs": "HTS_9504300010"
    },
    {
      "node": "HTS_9506114010",
      "description": "Snowboards",
      "score": "0.4875",
      "reason": "freebase / freebase / freebase / tree attributes",
      "system": "HTS",
      "hs_leafs": "HS_950611",
      "all_leafs": "HTS_9506114010"
    },
    {
      "node": "HTS_76151050",
      "description": "Cast",
      "score": "0.4300",
      "reason": "freebase / freebase / freebase",
      "system": "HTS",
      "hs_leafs": "HS_761510",
      "all_leafs": "2 nodes"
    }
  ]
}
```
**node** string  
The name of the harmonized code

**description** string
The human-readable description of the code.

**score** decimal as string[6]
A measurement of the proximity of the node as a match to the search term.

**system** string
The harmonized code system to which the code belongs. 

**reason, hs_leafs, all_leafs** string
Reserved for internal use only.


### Get Duty Rates for a Harmonized Code

Search for Duty Rates for a harmonized code. Rates are dependant on at least a destination country. 

#### Request
```plaintext
GET http://sandbox.landedcost.api.avalara.com/v2/hscodes?code=93070000&system=HS&destination=US&source=DE
```

**code** string, required  
The harmonized code

**system** string, required  
The classification system to which the code belongs

**destination** string, required  
The destination country for which rate data is desired.

**source** string, optional  
An optional filter for rates that limits results to a specific origin country.

#### Response
```plaintext
200
Content-Type: application/json
```
```json
[
  {
    "hs_code": "9307000000",
    "system": "HTS",
    "codePath": [
      {
        "hs_code": "93",
        "description": "ARMS AND AMMUNITION; PARTS AND ACCESSORIES THEREOF",
        "name": "HS_93",
        "level": 2
      },
      {
        "hs_code": "9307",
        "description": "Swords, cutlasses, bayonets, lances and similar arms and parts thereof and scabbards and sheaths therefor",
        "name": "HS_9307",
        "level": 3
      }
    ],
    "rates": [
      {
        "source_country": null,
        "formula": "rate(2.7%,costbasis())",
        "type": "ad valorem",
        "unit": "",
        "raw": "2.7%",
        "currency": "USD",
        "required": [
          "value"
        ],
        "customs_value": "extended-price"
      },
      {
        "source_country": "AU",
        "formula": "notax()",
        "type": "ad valorem",
        "unit": "",
        "raw": "Free",
        "currency": "USD",
        "required": [
          "value"
        ],
        "customs_value": "extended-price"
      },
      {
        "source_country": "BH",
        "formula": "notax()",
        "type": "ad valorem",
        "unit": "",
        "raw": "Free",
        "currency": "USD",
        "required": [
          "value"
        ],
        "customs_value": "extended-price"
      },
      {
        "source_country": "CA",
        "formula": "notax()",
        "type": "ad valorem",
        "unit": "",
        "raw": "Free",
        "currency": "USD",
        "required": [
          "value"
        ],
        "customs_value": "extended-price"
      },
      {
        "source_country": "CL",
        "formula": "notax()",
        "type": "ad valorem",
        "unit": "",
        "raw": "Free",
        "currency": "USD",
        "required": [
          "value"
        ],
        "customs_value": "extended-price"
      },
      {
        "source_country": "MX",
        "formula": "notax()",
        "type": "ad valorem",
        "unit": "",
        "raw": "Free",
        "currency": "USD",
        "required": [
          "value"
        ],
        "customs_value": "extended-price"
      }
    ]
  }
]
```
**source_country** string  
The two-character ISO code identifying the origin country associated with the duty.

**formula** string  
The formula used to calculate the rate, presented in Avalara-specific format.

**unit** string  
If the rate is assessed at a unit level, the appropriate unit involved. If `type` is not `units`, this value will be an empty string.

**raw** string  
The human-readable version of the rate.

**currency** string  
The three-character ISO code for the currency in which the duty should be assessed.

**required** string  
The required input values to calculate the correct duty amount.

**customs-value** string  
The customs value describes how to apply the duty rate. There are two current types

- extended-price: The rate applies to the following product: Price * Quantity
- net-price: The rate applies to the the following Sum: Price * Quantity + Shipping + Insurance

**type** string  
There are three types of landed cost rates that may be returned.

- ad valorem: this rate applies to the declared `customs-value` This is typically represented as a percentage of the cost.
- units: this is a rate that is tied to unit of measure. This is typically expressed as a monetary value per quantity, such as: $1/kg
- unknown: there is no stored rate data (or no applicable taxes) for the specified combination. Note that these will always have `"formula": "notax()"` 

### Get Rate Data
Allows for the traversal of classification system, harmonized codes, and duty rates, allowing the user to browse the available content.

#### Request
```plaintext
GET http://sandbox.landedcost.api.avalara.com/v2/hscodes/system/code?fullpath=true
```

**system** string, optional  
The classification system. If omitted, the response will include all current classification systems.

**code** string, optional  
The harmonized code within a system. If code is provided, system must also be provided.

**fullpath** boolean, optional  
If present, the response will include the entire chapter, subchapter, etc. and description data for a code.

#### Response
```plaintext
200
Content-Type: application/json
```
```json
[
  {
    "id": 23594,
    "level": 5,
    "is_leaf": 1,
    "is_hs_leaf": 0,
    "system": "HTS",
    "node_id": 23594,
    "parent_node": 23587,
    "hs_code": "5703201000",
    "name": "HTS_5703201000",
    "description": "Hand-hooked, that is, in which the tufts were inserted by hand or by means of a hand tool",
    "rates": [
      {
        "sourceCountry": null,
        "formula": "rate(5.8%,costbasis())",
        "type": "ad valorem",
        "unit": "",
        "raw": "5.8%",
        "currency": "USD",
        "required": [
          "value"
        ]
      },
      {
        "sourceCountry": "AU",
        "formula": "notax()",
        "type": "ad valorem",
        "unit": "",
        "raw": "Free",
        "currency": "USD",
        "required": [
          "value"
        ]
      },
      {
        "sourceCountry": "BH",
        "formula": "notax()",
        "type": "ad valorem",
        "unit": "",
        "raw": "Free",
        "currency": "USD",
        "required": [
          "value"
        ]
      },
      {
        "sourceCountry": "CA",
        "formula": "notax()",
        "type": "ad valorem",
        "unit": "",
        "raw": "Free",
        "currency": "USD",
        "required": [
          "value"
        ]
      },
      {
        "sourceCountry": "CL",
        "formula": "notax()",
        "type": "ad valorem",
        "unit": "",
        "raw": "Free",
        "currency": "USD",
        "required": [
          "value"
        ]
      },
      {
        "sourceCountry": "MX",
        "formula": "notax()",
        "type": "ad valorem",
        "unit": "",
        "raw": "Free",
        "currency": "USD",
        "required": [
          "value"
        ]
      }
    ]
  }
]
```
**rates** array of rates
Rate information by source country, formatted as for retrieval for Duty Rate retrieval.





