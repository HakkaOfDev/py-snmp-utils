# SNMP-UTILS

[![heart](https://img.shields.io/static/v1?label=Build%20With&message=❤&color=darkred&labelColor=red&style=for-the-badge)]()
[![foryou](https://img.shields.io/static/v1?label=For&message=You&color=aqua&labelColor=blue&style=for-the-badge)]()
[![license](https://img.shields.io/static/v1?label=License&message=OPENSOURCE&color=green&labelColor=darkgreen&style=for-the-badge)]()
<br><br>
An opensource library to use SNMP get/bulk/set/walk in Python

## Features

* Work with OIDS json list [Find Here](#OIDS List)
* [GET](#GET) command
* [SET](#SET) command
* [WALK](#WALK) command
* [BULK](#BULK) command
* [CHECK IF DEVICE CONNECTED](#CHECK)

## OIDS List

Change `PATH_TO_LIST` to your OIDS list if you want to use it.

Example for `OIDS.json`

```
{
    "system": {
        "name": "1.3.6.1.2.1.1.5",
        "uptime": "1.3.6.1.2.1.1.3",
        "mac_address": "1.3.6.1.2.1.2.2.1.6",
        "temperature": "1.3.6.1.4.1.6296.9.1.1.2.5.1.3"
    }
}
```

When constructor `SnmpUtils()` is called, the method `defineOIDsList()` is automaticaly called. So you can use the list
like this:

```
switch = SnmpUtils("10.0.0.1")
print(switch.oids.system.name) #return 1.3.6.1.2.1.1.5
```

## GET

GET SNMP Command return the value of a specific OID. \
`get(oid)`

```
switch = SnmpUtils("10.0.0.1")
switch_name = switch.get(switch.oids.system.name)
```

You can also use `getByID(oid, id)` which returns the value of the inferior OID.

```
switch = SnmpUtils("10.0.0.1")
switch_interface_3_description = switch.getByID(switch.oids.interfaces.description, 3) # return the description of the third interface
```

## SET

SET SNMP is use for set value of a specific OID. \
`set(oid, value)`

```
switch = SnmpUtils("10.0.0.1")
switch_name = switch.set(switch.oids.system.name, "Test")
```

## WALK

WALK SNMP Command return a dict of all values of inferiors OIDs. \
`walk(oid, numberOfIterations, dotPrefix)`

You can specify the number of value do you want in second parameter.
`dotPrefix` is used for add . in front of OID.

```
switch = SnmpUtils("10.0.0.1")
switch_10_interfaces_description = switch.walk(switch.oids.interfaces.description, 10) # return a dict with key/value
for k,v in switch_10_interfaces_description.items():
    print(k,v)
```

## BULK

BULK SNMP returns all following items up to a limit for an/several item(s). \
`bulk(*oids_list)`

```
switch = SnmpUtils("10.0.0.1")
switch_interfaces_description = switch.bulk(switch.oids.interfaces.description) #return a dict with description for all interfaces
```

## CHECK

You can easily check if a device is online \
`isConnected()`

```
switch = ("10.0.0.1")
if switch.isConnected():
    print("Switch online")
```

## Dependencies

* [PySNMP](https://pysnmp.readthedocs.io/en/latest/)

## Contributors

* [Alexandre GOSSARD](https://www.github.com/HakkaOfDev)
* [Alexis LEBEL](https://www.github.com/Alestrio)