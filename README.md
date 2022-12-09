# erl-feconf-protocol

The FECONF service is an ACNET service which can be queried for front-end configuration information. It uses the [protocol compiler](https://cdcvs.fnal.gov/redmine/projects/protocol-compiler/wiki) to serialize the request and reply messages. This library holds the generated code for Erlang.

ACSys/FE programmers don't need to directly use this library; the ACSys/FE framework implements a process that listens to ACNET requests and uses this library to understand the messages.

To add more messages, you need to edit the `FECONFv1.proto` file in the console repo (`uls/ul_feconf_protocol`.) The `Makefile` in this repo pulls the latest version, via a CVS link, when building (i.e. the `.proto` file is not managed by this project.)

## Build Dependencies

To build this project, your system needs access to the CVSWeb service (so, only onsite machines), you need the protocol compiler and Erlang OTP 21 installed locally.

## API

The following messages are supported. Contact the Front-end Group if you would like other information to be queriable.

### `GetAddress`

```
request GetAddress {
    binary ssdn;
}

reply DeviceAddress {
    string hostname;
}
```

Returns the IP hostname/address of the hardware associated with a driver instance. Some ACNET devices control Ethernet-based hardware and it's useful to be able to determine this association programmatically. The request specifies the SSDN of a device on the front-end. If the underlying driver talks to Ethernet equipment, the reply will contain the hostname or IP address of it.