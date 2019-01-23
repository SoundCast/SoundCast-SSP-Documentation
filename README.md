# SoundCast SSP Documentation
SoundCast Supply Side Documentation

This guide covers the latest version of the SoundCast Supplier Protocol. It is based on the latest OpenRTB 2.5, and helps to integrate with the SoundCast SSP.

## Data format
The SoundCast SSP supports JSON and Compressed JSON (gzip) as data formats for bid requests and bid responses. It is recommended to use Compressed JSON to minimize the amount of data exchanged between you and the SoundCast SSP as this reduces latency times between servers, and traffic listening costs for all parties involved. 

## Bid Request Format
As stated before we are fully compatible with the [OpenRTB 2.5 Format](https://wiki.iabtechlab.com/index.php?title=OpenRTB_2.5). 

Bid Request Sample:
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

