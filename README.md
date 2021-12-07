# SNMP-UTILS

[![heart](https://img.shields.io/static/v1?label=Build%20With&message=❤&color=darkred&labelColor=red&style=for-the-badge)]()
[![foryou](https://img.shields.io/static/v1?label=For&message=You&color=aqua&labelColor=blue&style=for-the-badge)]()
[![license](https://img.shields.io/static/v1?label=License&message=OPENSOURCE&color=green&labelColor=darkgreen&style=for-the-badge)]()
<br><br>
An opensource library to use SNMP get/set/bulk/walk/table more easily in Python

## Features
* [GET](#GET) command
* [SET](#SET) command
* [WALK](#WALK) command
* [BULK](#BULK) command
* [TABLE](#TABLE) command
* [CHECK IF DEVICE IS ONLINE](#CHECK)

## Link with oids.json

```python
import json
oids = None
with open('OIDS.json', 'r') as file:
    oids = json.load(file)
```

## GET

GET SNMP Command return the value of a specific OID. \
`get(oid)`

```python
switch = SnmpUtils("10.0.0.1")
switch_name = switch.get(oids['system']['name']) # return name of device
```

You can also use `get_by_id(oid, id)` which returns the value of the inferior OID.

```python
switch = SnmpUtils("10.0.0.1")
switch_interface_3_description = switch.get_by_id(oids['interfaces']['description'], 3) # return the description of the third interface
```

## SET

SET SNMP is use for set value of a specific OID. \
`set(oid, value_type, value)` \
*value_type can be one of i/u/t/a/o/s/x/d/b*
```python
switch = SnmpUtils("10.0.0.1")
switch_name = switch.set(oids['system']['name'], 's', "Test")
```

## WALK

WALK SNMP Command return a dict of all values of inferiors OIDs. \
`walk(oid)`

```
switch = SnmpUtils("10.0.0.1")
switch_interfaces_description = switch.walk(oids['interfaces']['description']) # return a dict with key/value
for k,v in switch_interfaces_description.items():
    print(k,v)
```

## BULK

BULK SNMP returns all following items up to a limit for an/several item(s). \
`bulk(*oids_list)`

```
switch = SnmpUtils("10.0.0.1")
switch_interfaces_description = switch.bulk(oids['interfaces']['description']) #return a dict with description for all interfaces
```

## TABLE

TABLE SNMP returns list of dicts \
`get_table(oid, sort_key)`

```
switch = SnmpUtils("10.0.0.1")
switch_interfaces = switch.get_table('1.3.6.1.2.1.2.2') # return list of dicts
```


## CHECK

You can easily check if a device is online \
`is_online()`

```
switch = ("10.0.0.1")
if switch.is_online():
    print("Switch online")
```

## Dependencies

* [PySNMP](https://pysnmp.readthedocs.io/en/latest/)
* [SNMP-CMDS](https://snmp-cmds.readthedocs.io/en/latest/)

## Contributors

* [Alexandre GOSSARD](https://www.github.com/HakkaOfDev)
* [Alexis LEBEL](https://www.github.com/Alestrio)