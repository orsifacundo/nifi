# Apache NiFi

## Introduction

For a quick introduction on Apache NiFi you can read the [this article](https://www.freecodecamp.org/news/nifi-surf-on-your-dataflow-4f3343c50aa2/).

## Repo structure

This repository contains 2 folders: one with some **templates** that I find very useful for learning how some things can be achieved and the other with **examples** that I've made.

## Development

### JSON_conversions

This dataflow shows how to manage JSON objects (in this example a generated response from a REST API) and convert them into some other formats.
It selects some fields and builds a different looking output.

So, from an input that looks like this:

<details><summary>JSON Object</summary>
<p>

```json
{
  "version" : "3.0",
  "timestamp_utc" : "2020/22/05 02:05:11",
  "errorCode" : 0,
  "errorMessage" : "Request executed correctly",
  "payload" : {
    "account" : {
      "email" : "info@wi-access.com",
      "identifier" : "PA-00000002",
      "networks" : [ {
        "label" : "Cliente 2",
        "devices" : null
      }, {
        "label" : "WiAccess",
        "devices" : [ {
          "public_ip_address" : "WW.WW.WW.WW",
          "add_date" : "2020/18/02 16:02:12",
          "label" : "AP-0001",
          "id" : 4004005106,
          "mac_address" : "F4:EC:38:FD:92:29",
          "mac_addresses" : [ "F4:EC:38:FD:92:29", "16:21:42:F6:FE:F8", "F4:EC:38:FD:92:2A" ],
          "ssids" : [ {
            "label" : "WiAccess",
            "clients" : null
          } ],
          "status" : "offline",
          "last_timestamp" : -1,
          "last_uptime" : 0,
          "last_bytes_rx" : 0,
          "last_bytes_tx" : 0,
          "last_pkts_rx" : 0,
          "last_pkts_tx" : 0,
          "last_load_percentage" : 0,
          "last_total_ram" : 0,
          "last_free_ram" : 0,
          "last_used_ram" : 0,
          "last_used_ram_percentage" : 0
        }, {
          "public_ip_address" : "XX.XX.XX.XX",
          "add_date" : "2020/29/02 15:02:15",
          "label" : "AP-0002",
          "id" : 4004023971,
          "mac_address" : "F4:EC:38:D0:FA:03",
          "mac_addresses" : [ "F4:EC:38:D0:FA:03", "F4:EC:38:D0:FA:04", "FA:89:64:EF:75:61" ],
          "ssids" : [ {
            "label" : "Netwotk2",
            "clients" : null
          } ],
          "status" : "online",
          "last_timestamp" : 1590113157,
          "last_uptime" : 74763,
          "last_bytes_rx" : 5831858,
          "last_bytes_tx" : 7097640,
          "last_pkts_rx" : 66016,
          "last_pkts_tx" : 63755,
          "last_load_percentage" : 0,
          "last_total_ram" : 29835264,
          "last_free_ram" : 7958528,
          "last_used_ram" : 21876736,
          "last_used_ram_percentage" : 73
        }, {
          "public_ip_address" : "YY.YY.YY.YY",
          "add_date" : "2020/01/03 23:03:35",
          "label" : "AP-0003",
          "id" : 4004024920,
          "mac_address" : "C4:E9:84:F7:9B:20",
          "mac_addresses" : [ "C4:E9:84:F7:9B:20", "C4:E9:84:F7:9B:20" ],
          "ssids" : [ {
            "label" : "Network3",
            "clients" : null
          } ],
          "status" : "online",
          "last_timestamp" : 1590113171,
          "last_uptime" : 74777,
          "last_bytes_rx" : 5579578,
          "last_bytes_tx" : 6994784,
          "last_pkts_rx" : 67923,
          "last_pkts_tx" : 62077,
          "last_load_percentage" : 0,
          "last_total_ram" : 29564928,
          "last_free_ram" : 7831552,
          "last_used_ram" : 21733376,
          "last_used_ram_percentage" : 74
        }, {
          "public_ip_address" : "ZZ.ZZ.ZZ.ZZ",
          "add_date" : "2020/20/02 23:02:38",
          "label" : "AP-0004",
          "id" : 4004010184,
          "mac_address" : "64:70:02:EE:00:76",
          "mac_addresses" : [ "64:70:02:EE:00:76", "64:70:02:EE:00:78", "64:70:02:EE:00:77" ],
          "ssids" : [ {
            "label" : "Network4",
            "clients" : null
          } ],
          "status" : "online",
          "last_timestamp" : 1590113159,
          "last_uptime" : 74764,
          "last_bytes_rx" : 36258929,
          "last_bytes_tx" : 13754775,
          "last_pkts_rx" : 167288,
          "last_pkts_tx" : 114481,
          "last_load_percentage" : 0,
          "last_total_ram" : 129368064,
          "last_free_ram" : 102699008,
          "last_used_ram" : 26669056,
          "last_used_ram_percentage" : 21
        } ]
      } ]
    }
  }
}
```

</p>
</details>

We can get the following different outputs:

1. One CSV with all the information

```
public_ip_address;label;status;mac_address
WW.WW.WW.WW;AP-0001;offline;F4:EC:38:FD:92:29
XX.XX.XX.XX;AP-0002;online;F4:EC:38:D0:FA:03
YY.YY.YY.YY;AP-0003;online;C4:E9:84:F7:9B:20
ZZ.ZZ.ZZ.ZZ;AP-0004;online;64:70:02:EE:00:76
```

2. Multiple CSVs each with a piece of information

```
public_ip_address;label;status;mac_address
WẀ.WW.WW.WW;AP-0001;offline;F4:EC:38:FD:92:29
```

3. Multiple JSONs each with a piece of information

```json
{
  "public_ip_address" : "WW.WW.WW.WW",
  "label" : "AP-0001",
  "status" : "offline",
  "mac_address" : "F4:EC:38:FD:92:29"
}
```

