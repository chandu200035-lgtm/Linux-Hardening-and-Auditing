\# Linux-Security-Hardening-Project





\## Enterprise-Grade Linux Server Hardening Lab



\## This project is my first Linux security hardening lab. I learned how to secure an Ubuntu server step by step using real-world security engineering methods. This includes SSH hardening, firewall configuration, Fail2Ban, audit logs, and automatic security updates.





\## Project Overview



\- I updated and patched my Ubuntu system

\- I created a separate admin user for security

\- I hardened SSH configuration

\- I set up and enabled the UFW firewall

\- I installed and configured Fail2Ban to stop brute-force attacks

\- I set up auditd to log user actions and login events

\- I enabled automatic security updates





\## Skills Demonstrated



\- Basic Linux administration

\- User and permission management

\- SSH security configuration

\- Network security using UFW firewall

\- Configuring Fail2Ban to block attacks

\- Setting up audit logs with auditd

\- Automatic patching and updates





\## Architecture



\- The host machine is my Windows laptop using VirtualBox.

\- Inside VirtualBox, I created an Ubuntu Linux virtual machine.

\- I installed and configured multiple security tools inside the VM.



```

+---------------------------+

|       Host Machine        |

|  Windows / VirtualBox     |

+------------+--------------+

             |

             | Virtual Network (NAT / Host-Only)

             |

+------------v------------------------------+

|        Ubuntu Security Lab VM             |

|-------------------------------------------|

|   SSH Hardening                           |

|     - Disable root login                  |

|     - AllowUsers chandu, secengineer      |

|                                           |

|   UFW Firewall                            |

|     - Deny incoming traffic               |

|     - Allow SSH only                      |

|                                           |

|   Fail2Ban                                |

|     - Protects SSH from brute-force       |

|                                           |

|   auditd                                  |

|     - Logs login events \& sudo actions    |

|                                           |

|   Auto Security Updates                   |

|     - unattended-upgrades                 |

+-------------------------------------------+



```





\## Hardening Steps Performed





\### 1. System update and upgrade


I updated the Linux system to make sure it had the latest patches. This included updating packages and upgrading the system to fix security vulnerabilities.



\### 2. Creating a Secure Admin User



I created a new user called 'secengineer' and added it to the sudo group. This helps avoid using the main account or root for administration.



\### 3. SSH Hardening



I edited the /etc/ssh/sshd\_config file to disable root login and limit SSH access only to my two users. This reduces the attack surface for brute-force attacks.



\### 4. Firewall Configuration (UFW)



I enabled the Ubuntu firewall and allowed only SSH through it. All other incoming connections are blocked by default.



\### 5. Installing Fail2Ban



I installed Fail2Ban and configured it to monitor SSH login attempts. It bans IP addresses that try too many wrong passwords.



\### 6. auditd System Logging



I installed auditd to track important security events like logins and admin commands. This helps in monitoring and incident investigation.



\### 7. Automatic Security Updates



I enabled unattended-upgrades so the server installs critical security patches automatically.





\## Validation and Testing



\### 1. SSH Hardening Validation



I checked the SSH configuration using the sshd command to verify that root login is disabled and only my users are allowed.

```
sudo sshd -T | grep -E "permitrootlogin|maxauthtries|allowusers"

```



\### 2. Firewall (UFW) Validation



I verified that the firewall is active and only OpenSSH is allowed.

```

sudo ufw status verbose

```



\### 3. Fail2Ban Validation



I checked the Fail2Ban jail status to make sure the SSH jail was enabled and monitoring login attempts.

```

sudo fail2ban-client status sshd

```



\### 4. auditd Validation



I tested auditd by checking login and sudo activity logs.

```

sudo ausearch -m USER\_LOGIN --start today

sudo ausearch -m USER\_CMD --start today

```



\### 5. Automated Security Updates Validation



I verified that unattended-upgrades was running and tested a dry-run update.

```

sudo systemctl status unattended-upgrades

sudo unattended-upgrade --dry-run --debug

```

