# SNMP ROS

Utilities for working with SNMP from ROS.

This package only supports a very small subset of SNMP. Basically, just reading single OIDs from SNMPv1/v2 agents. Notably, the node currently cannot interpret MIBs. Pull requests for additional functionality are welcome. 

## Node snmp\_reader

ROS node that allows reading OID values via SNMP into ROS topics or parameters.

### Parameters
- `~agent_address` (type `string`, default "127.0.0.1"): IP address of the SNMP agent.
- `~agent_port` (type `int`, default 161): Port to connect to.
- `~community` (type `string`, default "public"): The community to connect to.
- `~snmp_v2` (type `bool`, default `True`): If True, v2 is used, otherwise SNMP v1 is used.
- `~topics` (type `dict`, default `{}`): List of OIDs that should be periodically read and published as topics.
  - Each item in `topics` is a dict with the following items:
  - `oid` (type `string`): The OID to read.
  - `type` (type `string`, default `String`): Type of the ROS message to parse the value as. Use ROS message type names
                                              like `Int32`.
  - `topic` (type `string`, defaults to the key of this dictionary entry): The topic to publish the value to.
                                                                           Prepend `~` to publish it as a private topic.
  - `rate` (type `float`, default `1.0`): Publishing rate. If set to 0, the value is only read once and published
                                          latched.
- `~params` (type `dict`, default `{}`): List of OIDs that should be read once and set as ROS parameters.
  - Each item in `params` is a dict with the following items:
  - `oid` (type `string`): The OID to read.
  - `type` (type `string`, default `str`): Type Python type to parse the value as. Use Python type names like `int`.
  - `parameter` (type `string`, defaults to the key of this dictionary entry): The parameter to set the value to.
                                                                               Prepend `~` to set a private parameter.

### Published topics
- configured by the `~topics` parameter.

## Usage

Just run the `snmp_reader` node and pass it the required configuration. Look into the `config` folder for examples of the node configuration.
