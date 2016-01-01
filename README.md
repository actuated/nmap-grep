# nmap-grep
Comprehensive parsing script for grepable Nmap output files. Provides a summary table, split hosts files, and URLs for web and SMB hosts.

# Usage
`nmap-grep.sh` is meant for parsing grepable Nmap output files (-oG). The file must be the first parameter. **--out-dir** can be used to specify a custom output directory. If not output directory is given, nmap-grep-YYYY-MM-DD-HH-MM-SS will be created.

```
./nmap-grep.sh [inputfilename] [--out-dir [outputdirectory]] [[options]]
```

This script performs the following actions, which each have different options to flag them as disabled.
* Create a summary table for open ports as summary.txt, including the IP, port, tcp/udp, protocol, and any version information. This can be disabled with **--no-summary**.
* Create files for each open port, listing each IP with that port open on a separate line. By default, these files will be named [port]-[tcp/udp]-hosts.txt. This can be disabled with **--no-split**.
* Rename split hosts files for common ports and services. For example, 21-tcp-hosts.txt becomes ftp-hosts.txt. This can be disabled with **--no-label-split**.
* Create web-urls.txt, with URLs for every open TCP 80, 443, 8080, and 8443 service. This can be disabled with **--no-web-urls**.
* Create smb-urls.txt, with URLs for every open TCP 445 service. This can be disabled with **--no-smb-urls**.
* Create up-hosts.txt, listing every host that reported as "up". This can be disabled with **--no-up**.

# Example
```
# ./nmap-grep.sh test.txt --no-up

===========[ nmap-grep.sh - Ted R (github: actuated) ]===========

Input File: test.txt
Output Path: nmap-grep-2015-12-29-16-33-31/

Functions:
- Create summary.txt
- Create [port]-[tcp/udp]-hosts.txt for each open port
- Rename split hosts files for common services
- Create web-urls.txt
- Create smb-urls.txt

Press Enter to confirm...

===========================[ results ]===========================

summary.txt exists
smb-urls.txt exists
web-urls.txt exists

*-hosts.txt in nmap-grep-2015-12-29-16-33-31/:

1 1025-tcp-hosts.txt
1 1031-tcp-hosts.txt
1 1043-tcp-hosts.txt
1 1052-tcp-hosts.txt
1 1145-tcp-hosts.txt
1 135-tcp-hosts.txt
1 137-udp-hosts.txt
1 139-tcp-hosts.txt
1 3268-tcp-hosts.txt
1 3269-tcp-hosts.txt
1 464-tcp-hosts.txt
1 5666-tcp-hosts.txt
1 593-tcp-hosts.txt
1 88-tcp-hosts.txt
2 dns-tcp-hosts.txt
2 dns-udp-hosts.txt
1 http-hosts.txt
1 https-hosts.txt
1 ldap-hosts.txt
1 ldaps-hosts.txt
2 ntp-hosts.txt
1 rdp-hosts.txt
1 smb-hosts.txt
2 ssh-hosts.txt

Enter 'y' if you want to display summary.txt before ending... y

=============================[ fin ]=============================


+------------------+--------------+-----------------------------------------------------+
| HOST             | OPEN PORT    | PROTOCOL - SERVICE                                  | 
+------------------+--------------+-----------------------------------------------------+
| 172.24.44.1      | 22 / tcp     | ssh                                                 | 
| 172.24.44.1      | 53 / tcp     | domain                                              | 
| 172.24.44.1      | 80 / tcp     | http                                                | 
| 172.24.44.1      | 443 / tcp    | https                                               | 
| 172.24.44.1      | 53 / udp     | domain                                              | 
| 172.24.44.1      | 123 / udp    | ntp                                                 | 
+------------------+--------------+-----------------------------------------------------+
| 172.24.45.32     | 22 / tcp     | ssh                                                 | 
+------------------+--------------+-----------------------------------------------------+
| 172.24.254.4     | 53 / tcp     | domain                                              | 
| 172.24.254.4     | 88 / tcp     | kerberos-sec                                        | 
| 172.24.254.4     | 135 / tcp    | msrpc                                               | 
| 172.24.254.4     | 139 / tcp    | netbios-ssn                                         | 
| 172.24.254.4     | 389 / tcp    | ldap                                                | 
| 172.24.254.4     | 445 / tcp    | microsoft-ds                                        | 
| 172.24.254.4     | 464 / tcp    | kpasswd5                                            | 
| 172.24.254.4     | 593 / tcp    | http-rpc-epmap                                      | 
| 172.24.254.4     | 636 / tcp    | ldapssl                                             | 
| 172.24.254.4     | 1025 / tcp   | NFS-or-IIS                                          | 
| 172.24.254.4     | 1031 / tcp   | iad2                                                | 
| 172.24.254.4     | 1043 / tcp   | boinc                                               | 
| 172.24.254.4     | 1052 / tcp   | ddt                                                 | 
| 172.24.254.4     | 1145 / tcp   | x9-icue                                             | 
| 172.24.254.4     | 3268 / tcp   | globalcatLDAP                                       | 
| 172.24.254.4     | 3269 / tcp   | globalcatLDAPssl                                    | 
| 172.24.254.4     | 3389 / tcp   | ms-wbt-server                                       | 
| 172.24.254.4     | 5666 / tcp   | nrpe                                                | 
| 172.24.254.4     | 53 / udp     | domain                                              | 
| 172.24.254.4     | 123 / udp    | ntp                                                 | 
| 172.24.254.4     | 137 / udp    | netbios-ns                                          | 
+------------------+--------------+-----------------------------------------------------+
```
