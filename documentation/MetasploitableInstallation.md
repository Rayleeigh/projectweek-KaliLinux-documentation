## Installation Metasploitable

- [Installation Metasploitable](#installation-metasploitable)
    - [Ressources allocated to Metasploitable](#ressources-allocated-to-metasploitable)
    - [Log in credentials for user](#log-in-credentials-for-user)
    - [Log in credentials for root](#log-in-credentials-for-root)
    - [Network Configs](#network-configs)
    - [Installation](#installation)
    - [Navigation](#navigation)

#### Ressources allocated to Metasploitable

Here I will list all of the ressources:

Memory: 512 MB
Processors: 1 Total Core, 1 Logical 1 Processor core
Harddisk: 8GB
Networkcard 1

| Component     | Description                                   |
|---------------|-----------------------------------------------|
| Memory        | 512 MB                                        |
| Processors    | 1 total core, 1 logical core 1 processor core |
| Harddisk      | 8 GB                                          |
| Networkcard 1 | NAT                                           |
| Networkcard 2 | Host-Only                                     |
| Networkcard 3 | Custom Network                                |


#### Log in credentials for user

username: msfadmin
password: msfadmin

#### Log in credentials for root

username: root
password: root

#### Network Configs

|                | network-id    | subnetmask    | fixed-ip-address |
|----------------|---------------|---------------|------------------|
| custom network | 100.100.100.0 | 255.255.255.0 | ———————          |
| Kali VM        | 100.100.100.0 | 255.255.255.0 | ———————          |
| Metasploit VM  | 100.100.100.0 | 255.255.255.0 | 100.100.100.20   |
| Windows 10 VM  | 100.100.100.0 | 255.255.255.0 | 100.100.100.30   |

#### Installation

Fortunately for me the file i donwloaded from here already was the virtual machine config files. So there was no point for me to install all the other additional packages.

#### Navigation

* [Back to README](../README.md)
* [Forward to Metasploit installation](MetasploitableInstallation.md)

---

&copy; Rayan Lee Bopp