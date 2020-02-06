# SSP Documentation

This guide covers the latest version of the SoundCast Real-time Bidding Protocol based on the latest [OpenRTB Protocol Specification V2.5](https://wiki.iabtechlab.com/index.php?title=OpenRTB_2.5). 

## Request

The invitation to participate in an auction is sent using the POST method in JSON format (Content-Type: application/json) encoded in GZIP (Accept-Encoding: gzip).

### Header

The request header contains the OpenRTB Protocol Version (x-openrtb-version: 2.5).

### Body

The request body contains the Bid Request object. Its parameters describe the site, endpoint device, and consumer. These characteristics help the DSP select an ad and a bid.

## Bid Request Model (V2.5)

Bid request model for OpenRTB Protocol 2.5 is shown below.

### Bid Object

This is the top level object that is sent to the Buyer. Each bid request sent from BLIINK to a Buyer will contain the following fields.

| Key | Type | Description |
| --- | ---- | ----------- |
| id | string | Unique ID of the bid request. |
| cur | array of strings | Array of allowed currencies for bids on this bid request using ISO-4217 alpha codes. |
| allimps | integer  | A flag to indicate if the Supplier can verify that the impressions offered represent all of the impressions available in context to support road-blocking. |
| tmax | integer | Maximum time in milliseconds the exchange allows for bids to be received to avoid timeout, including internet latency |
| bcat | array of strings | Blocked Advertiser Categories, using the IAB taxonomy. |
| at | integer | Auction type. |
| device | object | 	Device object with details about the device to which the impression will be delivered, for more information, see the [Device Object](#device-object) section. |
| user | object | User Object which describes the user, for more information, see the [User Object](#user-object) section. |
| source | object | Indicates the entity responsible for the final impression sale decision, for more information, see the [Source Object](#source-object). |
| ext | object | Ext Object used for Supplier specific properties, for more information, see the [Ext Object](#ext-object) section. |
| imp | array of objects | Array of objects representing the impressions offered, for more information, see the [Impression Object](#impression-object) section. |
| site | object | The Site Object describing the site, for more information, see the [Site Object](#site-object) section.  |


#### Device Object


| Key | Type | Description |
| --- | ---- | ----------- |
| js | integer | 1 if the device supports JavaScript; otherwise 0. |
| ip | string | Specifies the IPv4 address closest to the device. |
| geo | object | Geo Object as derived from the device’s location services, or supplied by the Supplier if the device IP is missing. For more information, see the [Geo Object](#geo-object) section. |
| language | string | Alpha-2/ISO 639-1 code of browser language. |
| ua | string | Browser or application user agent string. |
| osv | string | Device operating system version |
| devicetype | integer | Device type as defined by OpenRTB. |
| w | integer | Physical height of the screen in pixels. |
| h | integer | Physical width of the screen in pixels. |
| pxratio | float | The ratio of physical pixels to device independent pixels. |
| ipv6 | string | IP address in IPv6. |


##### Geo Object


| Key | Type | Description |
| --- | ---- | ----------- |
| type | integer | Source of location data as defined by OpenRTB. |
| lat | double | Latitude from -90 to 90. South is negative. |
| lon | double | Longitude from -180 to 180. West is negative. |
| region | string | Region using ISO-3166-2 or FIPS region codes. |
| country | string | Country using ISO-3166-1 Alpha-2. |
| city | string | City name as provided by GeoIP. |
| zip | integer | Zip/postal code. |
| utcoffset | integer | Local time as the number +/- of minutes from UTC. |


#### User Object


| Key | Type | Description |
| --- | ---- | ----------- |
| id | string | Unique BLIINK ID of this user |
| consent | string | The binary encoding scheme that is passed in base64 URL/web safe format known as daisybit. |


#### Source Object


| Key | Type | Description |
| --- | ---- | ----------- |
| fd | integer | Indicates the entity responsible for the final impression sale decision |


#### Ext Object


| Key | Type | Description |
| --- | ---- | ----------- |
| ads_txt.status | integer | Indicates what information the ads.txt file contained regarding this Suppliers selling relationship with the publisher |
| ads_txt.auth_id | string | Passes the TAG ID if present in the ads.txt file |
| ads_txt.pub_id | string | Publisher ID |
| is_secure | integer | 0 for non-secure pages; 1 for secure pages. |
| ssp | string | The Supplier identification string |
| media_src | string | The Supplier identification string |


#### Impression object


| Key | Type | Description |
| --- | ---- | ----------- |
| id | string | ID of the impression being shown, unique within the bid request. |
| bidfloor | float | Bid floor in CPM as set by the Supplier |
| bidfloorcur | string | Bid floor currency specified using ISO-4217 alpha codes. |
| instl | integer | Specifies if the ad is an interstitial. |
| exp | integer | Impression expiry timeout, in seconds. |
| displaymanager | string | Name of the ad mediation partner, SDK technology. |
| displaymanagerver | string | Version of the ad mediation partner, SDK technology. |
| tagid | integer | Identifier for specific ad placement or ad tag that was used to initiate the auction. |
| banner | object | The Banner Object, for more information, see the [Banner Object](#banner-object) section. |
| pmp | object | The Banner Object, for more information, see the [PrivateMarket Object](#privatemarket-object) section. |
| secure | integer | Specifies if the page is SSL compliant. |


##### Banner Object


| Key | Type | Description |
| --- | ---- | ----------- |
| id | string | Unique identifier for the banner object |
| topframe | integer | Indicates if the banner is in the top frame as opposed to an iframe. |
| battr | array of integers | Blocked creative attributes as defined in the OpenRTB protocol. |
| btype | array of integers | Blocked banner ad types as defined in the OpenRTB protocol. |
| pos | integer | Ad Position as defined in the OpenRTB protocol. |
| mimes | array of strings | Specifies the content MIME types supported. |
| h | integer | Height of the impression in pixels. |
| w | integer | Width of the impression in pixels. |
| format | array of objects | Array of objects denoting the alternative sizes that may be used for bidding, for more information, see the [BannerFormat Object](#bannerformat-object) section. |


###### BannerFormat Object


| Key | Type | Description |
| --- | ---- | ----------- |
| h | integer | Height of the impression in pixels. |
| w | integer | Width of the impression in pixels. |


##### PrivateMarket Object


| Key | Type | Description |
| --- | ---- | ----------- |
| deals | array of objects | Array of Deal objects, for more information, see the [Deal Object](#deal-object) section. |
| private_auction | integer | A value of 1 indicates that only bids submitted inside pmp.deals will take part in the auction. A value of 0 indicates that bids without deal information may also be considered for serving. |


###### Deal Object


| Key | Type | Description |
| --- | ---- | ----------- |
| id | string | Deal ID |
| bidfloorcur | string | Bid floor currency specified using ISO-4217 alpha codes. |
| bidfloor | float | Deal price in CPM. |
| at | integer | Auction type. |


#### Site Object


| Key | Type | Description |
| --- | ---- | ----------- |
| id | string | An exchange specific identifier |
| publisher | object | Publisher object, for more information, see the [Publisher Object](#publisher-object) section. |
| domain | string | Domain of the site, used for advertiser side blocking. |
| ref | string | Referrer URL that caused navigation to the current page. |
| page | string | URL of the page where the impression will be shown. |
| name | string | Site name. |


##### Publisher Object


| Key | Type | Description |
| --- | ---- | ----------- |
| id | string | An exchange specific identifier. |
| domain | string | The highest level domain of the publisher. |
| name | string | Publisher name. |


## Bid Request Sample

```
{
   "id":"309195a0-1f21-11e9-9049-51b6556831b6",
   "allimps":0,
   "tmax":120,
   "cur":[
      "EUR"
   ],
   "bcat":[
      "IAB26",
      "IAB25",
      "IAB24",
      "IAB23",
      "IAB23",
      "IAB14-3"
   ],
   "at":2,
   "device":{
      "js":1,
      "ip":"62.23.198.190",
      "geo":{
         "type":2,
         "lat":48.8846,
         "lon":2.2697,
         "region":"ID",
         "country":"FR",
         "city":"Neuilly-sur-Seine",
         "utcoffset":60
      },
      "ua":"PostmanRuntime/7.6.0",
      "osv":"0.0.0",
      "devicetype":2,
      "w":"1024",
      "h":"2123",
      "pxratio":1.2,
      "ipv6":"fe80:0:0:0:200:f8ff:fe21:67cf"
   },
   "user":{
      "id":"035911ea467d4056"
   },
   "source":{
      "fd":1
   },
   "ext":{
      "ads_txt":{
         "status":1,
         "auth_id":"",
         "pub_id":""
      },
      "ssp":"SOUNDCAST",
      "media_src":"SOUNDCAST"
   },
   "imp":[
      {
         "bidfloor":8,
         "bidfloorcur":"EUR",
         "instl":0,
         "exp":120,
         "displaymanager":"SOUNDCAST",
         "displaymanagerver":"SOUNDCAST",
         "id":"3091bcb0-1f21-11e9-9049-51b6556831b6",
         "tagid":1,
         "audio":{
            "mimes":[
               "audio/mpeg"
            ],
            "startdelay":1,
            "maxseq":1,
            "sequence":1,
            "feed":3,
            "battr":[
               1,
               2
            ],
            "nvol":3,
            "minbitrate":32,
            "maxbitrate":320,
            "maxextended":0,
            "delivery":[
               1
            ],
            "companiontype":[
               null
            ],
            "companionad":[
               {
                  "topframe":0,
                  "battr":[
                     3,
                     4,
                     5,
                     8,
                     9,
                     14,
                     17
                  ],
                  "btype":[
                     3,
                     4
                  ],
                  "pos":0,
                  "mimes":[
                     "text/html",
                     "image/gif",
                     "image/jpg",
                     "application/javascript"
                  ],
                  "id":"3091bcb1-1f21-11e9-9049-51b6556831b6",
                  "h":300,
                  "w":500,
                  "format":[
                     {
                        "h":300,
                        "w":500
                     },
                     {
                        "h":100,
                        "w":500
                     }
                  ],
                  "ext":{
                     "extra_sizes":[
                        {
                           "h":31,
                           "w":300
                        },
                        {
                           "h":30,
                           "w":292
                        },
                        {
                           "h":50,
                           "w":300
                        },
                        {
                           "h":60,
                           "w":468
                        }
                     ]
                  }
               }
            ]
         },
         "pmp":{
            "deals":[
               {
                  "bidfloorcur":"EUR",
                  "bidfloor":23,
                  "at":2,
                  "ext":{

                  }
               },
               {
                  "bidfloorcur":"EUR",
                  "bidfloor":23,
                  "at":2,
                  "ext":{

                  }
               }
            ],
            "private_auction":1
         }
      }
   ],
   "site":{
      "publisher":{
         "id":"5c3df0e009c24",
         "name":"Test site1"
      },
      "id":"5c3df0e0044ff",
      "name":"Test network"
   }
}
```

## Any Questions
Please contact our support team.

