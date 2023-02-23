## Installation Windows 10

- [Installation Windows 10](#installation-windows-10)
    - [Ressources allocated to Windows 10](#ressources-allocated-to-windows-10)
    - [Log in credentials for user](#log-in-credentials-for-user)
    - [Network Configs](#network-configs)
    - [Installation](#installation)
    - [navigation](#navigation)

#### Ressources allocated to Windows 10

Here I will list all of the ressources:

| Component     | Description                                       |
|---------------|---------------------------------------------------|
| Memory        | 4GB                                               |
| Processors    | 16 total cores 4 Logical cores, 4 Processor Cores |
| Harddisk      | 60GB                                              |
| Networkcard 1 | NAT                                               |
| Networkcard 2 | Custom Network                                    |


#### Log in credentials for user

Username: KRATHE
Password: KRATHE

#### Network Configs

|                | network-id    | subnetmask    | fixed-ip-address |
|----------------|---------------|---------------|------------------|
| custom network | 100.100.100.0 | 255.255.255.0 | ———————          |
| Kali VM        | 100.100.100.0 | 255.255.255.0 | ———————          |
| Metasploit VM  | 100.100.100.0 | 255.255.255.0 | 100.100.100.20   |
| Windows 10 VM  | 100.100.100.0 | 255.255.255.0 | 100.100.100.30   |

#### Installation

I downloaded the imagefile from the [official microsoft page](https://go.microsoft.com/fwlink/?LinkID=799445).

I then made a new Virtual Machine in VMware Workstation PRO 16 and made the usuals steps to install a new virtual machine.

In the installer menu I set my preferred option, such as keyboard layout, language and region/timezone.

Then I chose my Windows version I chose Windows 10 Pro edition. Partitioned the hard drive and made my account.

#### navigation

* [Back to README](../README.md)
* [Back to Metasploit installation](KaliLinuxInstallation.md)
* [Back to Metasploit installation](MetasploitableInstallation.md)

---

&copy; Rayan Lee Bopp