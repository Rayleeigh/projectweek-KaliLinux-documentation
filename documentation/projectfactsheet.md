## Factsheet - Kali linux | Metasploitable

## Metasploit

#### starting services

Starting services on metasploit differs execptionally from other linux distributions you know as of today, this is mainly due to the version of Metasploit 2. See the version of Metasploit is the second installement and the second installement uses the Linux version 8.04.
Linux distributions that use versions that existed prior to 2011 still use the outdated version of systemd, meaning that the way to start/stop/restart services with systemctl where first introduced when version 3 of systemd was implemented in the each and individual versions of Linux.

So to start services on Linux versions that were realeased prior to the third version of systemd had to use the following command. In the example below I will show how to start the ssh-service on a Linux distribution that funciton on a systemd version prior to the 2011 version.

``` 
sudo /etc/init.d/ssh -- for users with sudo privileges.
     /etc/init.d/ssh -- for users with root privileges.
```
---

## Kali

#### Module Options for ssh_enumusers attack

```
Module options (auxiliary/scanner/ssh/ssh_enumusers):

   Name          Current Setting  Required  Description
   ----          ---------------  --------  -----------
   CHECK_FALSE   false            no        Check for false positives (random username)
   DB_ALL_USERS  false            no        Add all users in the current database to the list
   Proxies                        no        A proxy chain of format type:host:port[,type:host:port][...]
   RHOSTS                         yes       The target host(s), see https://github.com/rapid7/metasploit-framework
                                            /wiki/Using-Metasploit
   RPORT         22               yes       The target port
   THREADS       1                yes       The number of concurrent threads (max one per host)
   THRESHOLD     10               yes       Amount of seconds needed before a user is considered found (timing att
                                            ack only)
   USERNAME                       no        Single username to test (username spray)
   USER_FILE                      no        File containing usernames, one per line


Auxiliary action:

   Name              Description
   ----              -----------
   Malformed Packet  Use a malformed packet
```

This is the output you get when you want to configure an attack, such as the ssh_enumusers.
As stated in my guide for the ssh_enumusers attack I will explain what the each of the individual module options mean.
 
| MODULE OPTION  | DESCRIPTION                                                                                                                                                                                     |
|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `CHECK_FALSE`  | turning on this function will almost rule out 100% of the false positives.                                                                                                                      |
| `DB_ALL_USERS` | turning on this function adds all users in the database while using the ssh_enumusers attack on Metasploit. This Module Option is set to default                                                |
| `Proxies`      | turning on this function adds a proxy chain to your attack making sure that you won't be as easily discovered type it in the following format: type:host:port                                   |
| `RHOSTS`       | turning off this function will remove your targeted server. make sure you set the ip-address of the target server as the RHOSTS                                                                 |
| `THREADS`      | turning off this function will remove any of your attacks. You can have more than 1 Thread adding more makes the attack finish faster.                                                          |
| `THRESHOLD`    | turning off this function will flag every result as an account found/valid.                                                                                                                     |
| `USERNAME`     | turning on this function will take a Single username as a test if it works.                                                                                                                     |
| `USER_FILE`    | turning on this function will take a file containing a multitude of usernames and compate it to the ones in the targets system if one of them match they'll be flagged as a valid user account. |

Now you should know all the module options and what they do. But you also may noticed tha by now there is a section called `auxiliary action`. This section is responsible for the type of attack that will be occuring, there two action types for this attack firstly a `malformed packet` and a `timing attack`. But what is a malformed attack or rather a timing attack. Well let me explain it to you.

#### auxiliary actions for ssh_enumattack

| ACTION OPTION      | DESCRIPTION                                                                                                                                                                                                     |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Malformed Packet` | Upon setting the auxiliary action of the attack as `malformed packet` you will be sending packets that were constructed for malicious usecases such as exploiting weaknesses in software like I'm doing here. |
| `Timing Attack`    | Upon setting the auxiliary action of the attack as `timing attack`. A timing attack is a type of cyber attack that exploits the timing of system processes to gain access to sensitive data. This attack can be used to bypass authentication systems, decrypt data, or gain access to sensitive information. It works by measuring the time it takes for a system to respond to a specific request and using that data to infer information about the system. |


