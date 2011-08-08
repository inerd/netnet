--- README.txt ---

=========================
         _           _
 ___ ___| |_ ___ ___| |_
|   | -_|  _|   | -_|  _|
|_|_|___|_| |_|_|___|_|

=========================

1. Introduction:
*===============
netnet[.py] - a simple object-oriented extensible interface for Network Devices (i.e. switches,
routers, etc.), written entirely in Python.

netnet is built from three main components:
i. a device, representing a network device that you can connect to and work with.
Anything that inherits from NetDevice, e.g. Cisco Ethernet Switch (CiscoEthernetSwitch).
ii. a connection, representing a way to connect to a device.
Anything that inherits from Connection, e.g. SSH Connection (SSHConnection).
iii. a command, representing a command that can run on that device.
Commands should, basically, inherit from the Command object, e.g. Cisco Command (CiscoCommand).
However, in the current design, we implement a function which returns a Command object for each
command.

2. Structure:
*============
The project tree is separated into X folders:
- /netnet
  --/core
  --/brands
  --/external

- 'core' directory serves for netnet core files, including device, connection and command sources.
- 'brands' include source for different brands of network equipment, such as Cisco.
- 'external' includes 3rd-party sub-modules, such as paramiko.

Each brand sub-directory should include 3 base files:
1. __init__.py
2. device.py - defines the device, by inheriting from NetDevice (core.devices.NetDevice)
3. commands.py - defines the device commands, by inheriting from Command (core.commands.Command)
In case of need, one can also define a seperate connection object for the device, by inheriting
from Connection (core.connections.Connection).

Features:
*========
netnet currently supports:
[Cisco]: support for Cisco common commands and devices.
[SNMP]: full support for SNMP reading (snmpget) and initialization of object from device SNMP
interface.
