
# XProxy.IO - Build your self mobile proxies

This repository introduce information of XProxy device. Xproxy device can help you make 3G/4G proxies for MMO users who don't know much about mobile proxy setup or technical.

You can use any 3G/LTE dongles, Android phones on the world to makes proxies. It's easy, just plug dongles and proxies make automatically!


### Table of contents

  * [The list of dongles support by XProxy Device ](#the-list-of-dongles-support-by-xproxy-device)
  * [REST API document](#rest-api-document)
 
## The list of dongles support by XProxy Device
- All Huawei dongles support Hilink interface such as: E3372h, E3372s, E8372h, E303h, E353h, E3276, E3276s, E3272, E3131, E3531, E3351, E3251, E392, E398, E397, E8278, E323S, K5005, K5007, K5150, W5101
- All Huawei dongles support Stick mode with AT command: MS3372NA, E303s-1, E173, E3131, E367
- All ZTE dongles support Hilink interface such as: MF861, MF832G, MF831, MF833, MF832u, MF832s, MF827, MF826, MF79, MF75, MF820, MF820D, MF820T, MF820S2, MF880, MF821, MF821D, MF821S2, MF822, MF823, MF825, MF825C, MF831, MF170, MF730M, MF667
- All ZTE dongles support Stick mode such as: MF190, MF190S, MF820B, E173Eu-1
- Another stick model universal: Qualcomm MDM9K, D-link-156, Mobily, HSPA Data Card

## Rest API document


#### <span style="color:blue">Modem & Proxy REST API</span>


#### Get list devices and proxies information

<details>
 <summary><code>GET</code> <code><b>/v1/info_list</b></code> </summary>

##### Parameters

> | name      |  type     | data type               | description                                                           |
> |-----------|-----------|-------------------------|-----------------------------------------------------------------------|
> | page      |  optional | integer                 | A number of current page to fetch info                                |
> | limit     |  optional | integer                 | A number of items to get per page                                     |


##### Responses

<details>
  <summary>Click to expand</summary>
  
```javascript
{
  "status: True,
  "data": [
    {
      "position": 1,
      "host": "192.168.177.133",
      "proxy_port": 4201,
      "proxy_port_v6": 6201,
      "socks5_port": 5201,
      "socks5_port_ipv6": 7201,
      "public_ip": "171.255.118.95",
      "public_ip_ipv6": null,
      "last_rotation": null,
      "last_updated_ip": 1623331226.473283,
      "device_manufacture": "HW-Hilink",
      "device_imei": "866785034707108",
      "device_number": "11",
      "device_ip": "192.168.11.1",
      "device_rebooting": false,
      "device_resetting": false,
      "device_extra_info": {
        "rssi_info": "N/A",
        "name": "E3372",
        "serial": "Y4Q7S19510000205",
        "imei": "866785034707108",
        "imsi": "452040320937808",
        "wan": "undefined",
        "connected": true,
        "network_mode": "LTE_4G",
        "sim_live": true,
        "signal_strength": "5",
        "swver": "22.333.63.00.143",
        "hwver": "CL2E3372HM",
        "provider_id": "45204",
        "provider": "Viettel"
      }
    },
    {
      "position": 2,
      "host": "192.168.177.133",
      "proxy_port": 4202,
      "proxy_port_v6": 6202,
      "socks5_port": 5202,
      "socks5_port_ipv6": 7202,
      "public_ip": "103.199.70.155",
      "public_ip_ipv6": "2402:9d80:38a:dda0:c0e:ee4:933:907",
      "last_rotation": 1623330956.916284,
      "last_updated_ip": 1623331189.96525,
      "device_manufacture": "XProxy-Hilink",
      "device_imei": "869383054786694",
      "device_number": "1",
      "device_ip": "192.168.1.1",
      "device_rebooting": false,
      "device_resetting": false,
      "device_extra_info": {
        "connected": true,
        "sim_live": true,
        "signal_strength": 4,
        "network_mode": "4G",
        "name": "XH20",
        "rssi_info": 44,
        "imei": "869383054786694",
        "swver": "1.0",
        "hwver": "1.0",
        "imsi": "8984012002134231827f",
        "provider_id": "Mobifone",
        "provider": "Mobifone"
      }
    }
  ],
  "total": 2
}
```
</details>

##### Example cURL

```javascript
curl -X GET -H "Content-Type: application/json" http://192.168.1.100/api/v1/info_list
```

</details>

------------------------------------------------------------------------------------------

#### Rotation IP with specific proxy or position
 
<details>
<summary><code>GET</code> <code><b>/v1/rotation/proxy/<< proxy >></b></code> <code>[rotation IP with specific proxy]</code> </summary>

##### Parameters

> | name      |  type     | data type               | description                                                                            |
> |-----------|-----------|-------------------------|----------------------------------------------------------------------------------------|
> | proxy     |  required | string                  | A proxy or socks in format <code>ip:port</code> to indicate the device to rotation IP  |

##### Responses

> | field      |   data type    |  description                                                                                              	  |
> |------------|----------------|--------------------------------------------------------------------------------------------------------------|
> | status     |   boolean      |  `True` if sent command successfully, `False` if another reason                                           	  |
> | msg        |   string       |  `slot_not_found` could not find the slot attached with the proxy                                            |
> |            |                |  `modem_disconnected` modem disconnected, could not rotation                                                 |
> |            |                |  `command_sent` sent successfully                                                                            | 

- Send rotation command successfully

```javascript
{
  "status": true,
  "msg": "command_sent"
}
```

- Another status  

```javascript
{
  "status": false,
  "msg": "modem_disconnected"
}
```

##### Example cURL

 > send a command to rotation IP of device for proxy <code>192.168.1.100:4001</code>
 
```javascript
curl -X GET -H "Content-Type: application/json" http://192.168.1.100/api/v1/rotation/192.168.1.100:4001
```

</details>


<details>
<summary><code>GET</code> <code><b>/v1/rotation/position/<< position >></b></code> <code>[rotation IP with specific position]</code> </summary>

##### Parameters

> | name      |  type     | data type               | description                                                                                  |
> |-----------|-----------|-------------------------|----------------------------------------------------------------------------------------------|
> | position  |  required | number                  | A position number of modem in device list from 1 to N	to indicate the device to rotation IP 	|


##### Responses

Same as <i>rotation IP with specific proxy</i>

##### Example cURL

> send a command to rotation IP of modem in position 1
```javascript
curl -X GET -H "Content-Type: application/json" http://192.168.1.100/api/v1/rotation/1
```

</details>


------------------------------------------------------------------------------------------

#### Get status of proxy or position
 
<details>
<summary><code>GET</code> <code><b>/v1/status/proxy/<< proxy >></b></code> <code>[get status of specific proxy]</code> </summary>

##### Parameters

> | name      |  type     | data type               | description                                                                           |
> |-----------|-----------|-------------------------|---------------------------------------------------------------------------------------|
> | proxy     |  required | string                  | A proxy or socks in format <code>ip:port</code> to indicate the device to get status  |

##### Responses

> | field      |   data type    |  description                                                                                              	  |
> |------------|----------------|-----------------------------------------------------------------------------------------------------------------|
> | status     |   boolean      |  `True` if modem ready, `False` if modem busy or offline                                                  	  |
> | msg        |   string       |  `MODEM_READY` when modem normally, `MODEM_NOT_FOUND` when not found modem attached to this position            |
> |            |                |  `MODEM_DISCONNECTED` when modem disconnected, `COLLISION_IP` when modem met collision IP with before rotation  | 

- Modem ready 

```javascript
{
  "status": true,
  "msg": "MODEM_READY"
}
```

- Another status  

```javascript
{
  "status": false,
  "msg": "MODEM_DISCONNECTED"
}
```

##### Example cURL

 > send a command to get status of device for proxy <code>192.168.1.100:4001</code>
 
```javascript
curl -X GET -H "Content-Type: application/json" http://192.168.1.100/api/v1/status/192.168.1.100:4001
```

</details>


<details>
<summary><code>GET</code> <code><b>/v1/status/position/<< position >></b></code> <code>[get status of specific position]</code> </summary>

##### Parameters

> | name      |  type     | data type               | description                                                                           |
> |-----------|-----------|-------------------------|---------------------------------------------------------------------------------------|
> | position  |  required | number                  | A position number of modem in device list from 1 to N								    |


##### Responses

Same as <i>get status of specific proxy</i>

##### Example cURL

 > send a command to get status of device at position 1

```javascript
curl -X GET -H "Content-Type: application/json" http://192.168.1.100/api/v1/status/1
```

</details>

------------------------------------------------------------------------------------------

#### Reboot dongle with specific proxy or position
 
<details>
<summary><code>GET</code> <code><b>/v1/reboot/proxy/<< proxy >></b></code> <code>[reboot dongle with specific proxy]</code> </summary>

##### Parameters

> | name      |  type     | data type               | description                                                                            |
> |-----------|-----------|-------------------------|----------------------------------------------------------------------------------------|
> | proxy     |  required | string                  | A proxy or socks in format <code>ip:port</code> to indicate the device to reboot       |

##### Responses

> | field      |   data type    |  description                                                                                                 |
> |------------|----------------|--------------------------------------------------------------------------------------------------------------|
> | status     |   boolean      |  `True` if sent command successfully, `False` if another reason                                              |
> | msg        |   string       |  `modem_disconnected` modem disconnected, could not rotation                                                 |

- Send reboot command successfully

```javascript
{
  "status": true,
  "msg": "Modem reboot successfully!"
}
```

- Another status  

```javascript
{
  "status": false,
  "msg": "modem_disconnected"
}
```

##### Example cURL

 > send a command to reboot device for proxy <code>192.168.1.100:4001</code>
 
```javascript
curl -X GET -H "Content-Type: application/json" http://192.168.1.100/api/v1/reboot/192.168.1.100:4001
```

</details>


<details>
<summary><code>GET</code> <code><b>/v1/reboot/position/<< position >></b></code> <code>[reboot dongle with specific position]</code> </summary>

##### Parameters

> | name      |  type     | data type               | description                                                                                  |
> |-----------|-----------|-------------------------|----------------------------------------------------------------------------------------------|
> | position  |  required | number                  | A position number of modem in device list from 1 to N	to indicate the device to reboot       |


##### Responses

Same as <i>reboot dongle with specific proxy</i>

##### Example cURL

> send a command to reboot modem in position 1
```javascript
curl -X GET -H "Content-Type: application/json" http://192.168.1.100/api/v1/reboot/1
```

</details>

#### <span style="color:blue">Selling platform REST API</span>

#### Get list shared socks/proxies 

<details>
 <summary><code>GET</code> <code><b>/selling/shared_proxies</b></code> </summary>

##### Parameters

> | name               |  type     | data type               | description                                                                                              |
> |--------------------|-----------|-------------------------|----------------------------------------------------------------------------------------------------------|
> | page               |  optional | integer                 | A number of current page to fetch info                                                                   |
> | limit              |  optional | integer                 | A number of items to get per page                                                                        |
> | modemPosition      |  optional | integer                 | A filter parameter to get only shared socks/proxies belong to device in position number  `modemPosition` |
> | proxyPort          |  optional | integer                 | A filter parameter to get only shared socksproxy with port number `proxyPort`                            |


##### Responses

A list of json object in `data` section 

 
> | name                        |  type       					  | description                                                                                             |
> |-----------------------------|-------------------------------- |---------------------------------------------------------------------------------------------------------|
> | id                          |  integer    					  | ID of shared socks/proxy                                                                 				|
> | position                    |  integer    					  | Position of dongle which shared                                                                       	|
> | shared_port                 |  integer    					  | A port number of socks/proxy																			|
> | port_type                   |  enum [`HTTP`,`SocksV5`]        | An enum indicate this port is `HTTP` is a proxy or `SocksV5` is a socks v5                              |
> | ip_type                     |  enum [`IPv4`,`IPv6`]           | An enum indicate this port will produced type of IP: `IPv4` or `IPv6`	                                |
> | auth_ip_enabled             |  boolean                        | Authentication IP enabled? `true` if enabled else `false`                                               |
> | auth_ip_list                |  string                         | Authentication IP list separate by comma like `128.123.1.38,1.211.12.125`                              	|
> | auth_user_enabled           |  boolean                        | Authentication user/password enabled? `true` if enabled else `false`                                    |
> | auth_user_list              |  string                         | Authentication user/password list separate by comma like `user1:pass1,user2:pass2`                     	|
> | web_blacklist_enabled       |  boolean                        | Website blacklist enabled? `true` if enabled else `false`                                     			|
> | web_blacklist               |  string                         | Website blacklist list separate by comma like `*.blacklist.com,facebook.com,*.facebook.com`             |        > | web_whitelist_enabled       |  boolean                        | Website whitelist enabled? `true` if enabled else `false`                                     	         |
> | web_whitelist               |  string                         | Website whitelist list separate by comma like `*.whitelist.com,facebook.com,*.facebook.com`             |        
> | expired_at                  |  string                         | A day present the expired date of this port, format `dd/MM/yyyy`             							|
> | remaining                   |  float                          | Present the number days remaining to use this port              										|  
> | counter_dl_limit            |  enum [`unlimited`,`limited`]   | An enum indicate this port is `limited` or `unlimited` download data usage 								|
> | counter_dl_limit_by			|  enum [`DAILY`,`WEEKLY`, 		  | An enum indicate this port is `limited` download data usage by:											|
> |								|	`MONTHLY`,`END_QUOTA`,`NONE`] | `DAILY`: counter will reset daily																		|
> | 							|   							  | `WEEKLY`: counter will reset weekly																		|
> | 							|   							  | `MONTHLY`: counter will reset monthly																	|
> | 							|   							  | `END_QUOTA`: counter will reset when met `counter_dl_limit_quota` limited 								|
> | 							|   							  | `NONE`: `ulimited` without limit data usage																|
> | counter_dl_limit_quota      | integer  						  | A number of MB (Megabytes) to limit download data when `counter_dl_limit` enabled as `limited`			|
> | 							|   							  | And it will be caused this proxy can not use when reach the end of `counter_dl_limit_quota` MB in 		|
> | 							|   							  | `counter_dl_limit_by` period.																			|
> | counter_dl_used_bytes		| integer 				 		  | An integer indicate number of `bytes` data downloaded of this proxy										|
> | counter_dl_used_mb			| double 				 		  | A double indicate number of `MB (Megabyte)` data downloaded of this proxy								|
> | counter_dl_reset			| string 				 		  | A time indicate latest reset counter data of this proxy, format `dd/MM HH:mm:ss`						|
> | counter_dl_updated			| string 				 		  | A time indicate latest updated counter data of this proxy, format `dd/MM HH:mm:ss`						|
> | counter_ul_limit            |  enum [`unlimited`,`limited`]   | An enum indicate this port is `limited` or `unlimited` upload data usage 								|
> | counter_dl_limit_by			|  enum [`DAILY`,`WEEKLY`, 		  | An enum indicate this port is `limited` upload data usage by:											|
> |								|	`MONTHLY`,`END_QUOTA`,`NONE`] | `DAILY`: counter will reset daily																		|
> | 							|   							  | `WEEKLY`: counter will reset weekly																		|
> | 							|   							  | `MONTHLY`: counter will reset monthly																	|
> | 							|   							  | `END_QUOTA`: counter will reset when met `counter_ul_limit_quota` limited 								|
> | 							|   							  | `NONE`: `ulimited` without limit data usage																|
> | counter_ul_limit_quota      | integer  						  | A number of MB (Megabytes) to limit upload data when `counter_ul_limit` enabled as `limited`			|
> | 							|   							  | And it will be caused this proxy can not use when reach the end of `counter_ul_limit_quota` MB in 		|
> | 							|   							  | `counter_ul_limit_by` period.																			|
> | counter_ul_used_bytes		| integer 				 		  | An integer indicate number of `bytes` data uploaded of this proxy										|
> | counter_ul_used_mb			| double 				 		  | A double indicate number of `MB (Megabyte)` data uploaded of this proxy								    |
> | counter_ul_reset			| string 				 		  | A time indicate latest reset counter data of this proxy, format `dd/MM HH:mm:ss`						|
> | counter_ul_updated			| string 				 		  | A time indicate latest updated counter data of this proxy, format `dd/MM HH:mm:ss`						|
> | bw_limit_enabled            | boolean                         | Limit bandwidth download/upload? `true` if enabled else `false`                                     	|
> | bw_limit_rate               | integer                         | A maximum of Mbps (Megabit per second) could be reached	to download/upload     	                    	|
> | created_at		            | string                          | A string present the date created socks/proxy								 	                    	|
> | custom_dns                  | string                          | A list of custom name server separate by comma for HTTP/HTTPs proxy  	       			             	|
> | memo			            | string                          | A noted text for this share socks/proxy									     	                    	|

<details>
  <summary>Example data. Click to expand</summary>
  
```javascript
{
  "data": [
    {
      "id": 1,
      "position": 1,
      "shared_port": 20001,
      "port_type": "HTTP",
      "ip_type": "IPv4",
      "auth_ip_enabled": true,
      "auth_ip_list": "171.226.0.32,171.226.0.33",
      "auth_user_enabled": true,
      "auth_user_list": "user1:pass1,user2:pass2",
      "web_blacklist_enabled": false,
      "web_blacklist": "",
      "web_whitelist_enabled": true,
      "web_whitelist": "instagram.com,*.instagram.com",
      "expired_at": "09/07/2021",
      "remaining": 28.2,
      "counter_dl_limit": "limited",
      "counter_dl_limit_by": "DAILY",
      "counter_dl_limit_quota": 2000,
      "counter_dl_used_bytes": 0,
      "counter_dl_used_mb": 0.0,
      "counter_dl_updated": null,
      "counter_dl_reset": "11/06 05:55:31",
      "counter_ul_limit": "limited",
      "counter_ul_limit_by": "DAILY",
      "counter_ul_limit_quota": 2000,
      "counter_ul_used_bytes": 0,
      "counter_ul_used_mb": 0.0,
      "counter_ul_updated": null,
      "counter_ul_reset": "11/06 05:55:31",
      "bw_limit_enabled": true,
      "bw_limit_rate": 25,
      "memo": "share for user1",
      "created_at": "19/01/1970",
      "custom_dns": "74.125.41.7 74.125.41.8"
    },
    {
      "id": 2,
      "position": 2,
      "shared_port": 20002,
      "port_type": "HTTP",
      "ip_type": "IPv4",
      "auth_ip_enabled": true,
      "auth_ip_list": "171.226.0.32,171.226.0.33",
      "auth_user_enabled": true,
      "auth_user_list": "user1:pass1,user2:pass2",
      "web_blacklist_enabled": true,
      "web_blacklist": "facebook.com,*.facebook.com",
      "web_whitelist_enabled": false,
      "web_whitelist": "",
      "expired_at": "09/07/2021",
      "remaining": 28.2,
      "counter_dl_limit": "limited",
      "counter_dl_limit_by": "DAILY",
      "counter_dl_limit_quota": 2000,
      "counter_dl_used_bytes": 0,
      "counter_dl_used_mb": 0.0,
      "counter_dl_updated": null,
      "counter_dl_reset": "11/06 05:55:31",
      "counter_ul_limit": "limited",
      "counter_ul_limit_by": "DAILY",
      "counter_ul_limit_quota": 2000,
      "counter_ul_used_bytes": 0,
      "counter_ul_used_mb": 0.0,
      "counter_ul_updated": null,
      "counter_ul_reset": "11/06 05:55:31",
      "bw_limit_enabled": true,
      "bw_limit_rate": 25,
      "memo": "share for user2",
      "created_at": "19/01/1970",
      "custom_dns": "74.125.41.7 74.125.41.8"
    }
  ],
  "total": 2,
  "status": true
}
```
</details>

##### Example cURL

```javascript
curl 'http://192.168.1.100/selling/shared_proxies?page=1&limit=20' 
```

</details>


> Contact information:
 > * Website: [http://xproxy.io](http://xproxy.io])
 > * Telegram: @phunguyen_hcmus
