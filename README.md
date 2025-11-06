![NOKIA](media/logo.png)

---

# Ansible Collection – `nokia.openconfig`

This [collection](https://galaxy.ansible.com/nokia/openconfig) for Ansible by RedHat provides connection plugins and modules to interact with devices that support OpenConfig gRPC API services.

## Status of this project
This collection implements the gRPC Network Management Interface (gNMI) service. The gRPC PROTO interface definition is available from [GitHub](https://github.com/openconfig/gnmi/blob/master/proto/gnmi/gnmi.proto). The gNMI specification can be found [here](https://github.com/openconfig/reference/blob/master/rpc/gnmi/gnmi-specification.md).

Please be aware, that the gNMI connection plugin establishes a dedicated, persistent gRPC session. Therefore transport, connectivity and API service are all collapsed into the connection plugin without the need to have a loader for any sort of vendor specific sub-plugins.

Even this project is supposed to be agnostic to vendors and device families, this collection has only been validated against Nokia SR OS and SRLinux nodes running 25.7 release.

As of today, the gNMI modules of this collection only suppport JSON_IETF (preferred) and JSON encoding. The implementation will run a Capability request during session setup, to determine the list of encodings supported by the networking device (acting as gNMI server). The encoding auto-discovery can be disabled, by setting the required encoding in the playbook, host file or using an environment variable.

## Installation
Distribution is via [ansible-galaxy](https://galaxy.ansible.com/).
To install this collection, please use the following command:
```bash
ansible-galaxy collection install nokia.openconfig
```

If you have already installed a previous version, you can  upgrade to the latest version of this collection, by adding the `--force-with-deps` option:
```bash
ansible-galaxy collection install nokia.openconfig --force-with-deps
```

## Usage
To use the gNMI modules from this collection, please make sure to set `ansible_connection` variable to `nokia.openconfig.gnmi`. Due to the nature of gNMI being vendor agnostic, the `network_os` does not have any impact to the function of this module.

## Requirements
* Ansible 2.9 (or newer)

## Supported vendors
Tested with Nokia SR OS and SRLinux

## Playbooks

Please check examples contained in the `tests/playbooks` folder as part of the CI/CD test automation.

## Modules
* gnmi_capabilities
* gnmi_get
* gnmi_config
* gnmi_subscribe
