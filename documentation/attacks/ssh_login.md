## Metasploit 2 ssh exploit
- [Metasploit 2 ssh exploit](#metasploit-2-ssh-exploit)
    - [functionality](#functionality)
    - [starting the attack](#starting-the-attack)
    - [solving this exploit](#solving-this-exploit)
    - [Explaination of solutions](#explaination-of-solutions)
    - [Sources](#sources)

#### functionality

The SSH Login exploit enables users to gain access to a remote system by providing valid SSH credentials. This exploit works by attempting to authenticate against the target system using a variety of different username and password combinations. If one of the combinations is successful, the attacker will have access to the system and will be able to perform malicious activities.
In order to use the SSH Login exploit in MSF, the user must have the correct information about the target system, such as the IP address, username, and password. Once the user provides this information, the exploit can be configured to attempt to authenticate against the target. If successful, the user will have access to the system and will be able to use it to perform malicious activities.
The advantage of using the SSH Login exploit in MSF is that it is a relatively simple exploit to use and can be used to gain access to a variety of systems. Furthermore, the exploit can be used in conjunction with other tools and exploits to increase the attacker’s access to the system.

#### starting the attack

As I previously mentioned, inorder to launch such an attack we must have the correct information about the target system such as the ip address, username and password. since we have neither of the three mentioned requirements we will have to provide these informations ourselves. We can do this by using following things a network scan that searches for a ip address with an open ssh port. In case your wondering what the port number for ssh is 22. For more information please refer to my list of standardized ports you can find it here [🗎 standardized ports](../standardizedports.md).

Starting off with providing the ip address. This can be done by performing a network sweep or rather sweeping the network after open ssh ports. As I already said the port for ssh is the port 22. Now armed with that knowledge we can now start inputing the command.

``
nmap -sT -p 22 192.158.236.0/24
``

After the conclusion of the network sweep we can now proceed with an attack that will enumarate a user. As you may already have guessed I've already done such a attack/exploit. This exploit is called ssh_enumusers. To know how it works please refer to my ssh_enumuser guide right here. [🗎 ssh_enumuser guide](shh_enumusers.md#starting-the-attack). This attack is also associated with ssh as the name of the exploit may already endows. This exploit is used to ilicit responses from the ssh server, for more information please refer to my guide on ssh_enumusers. [🗎 ssh_enumusers guide](shh_enumusers.md#functionality)


#### solving this exploit

You can prevent the ssh_login exploit by implementing following points. These several steps are crucial to ensure safety on your SSH-server. This can all be done in the config file of the SSH file. In order to do this go to the /etc directory and then to the following subdirectories, /ssh and then open the file ssh configuration file with following command.

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

[![](https://i.ytimg.com/vi/XalbmfxFie4/maxresdefault.jpg)](https://www.youtube.com/watch?v=XalbmfxFie4 "")