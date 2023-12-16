## Objectives: Exam 201
### Topic 200: Capacity Planning

#### [[200.1 Measure and Troubleshoot Resource Usage]]
| | |
|---|---|
|**Weight**|6|
|**Description**|Candidates should be able to measure hardware resource and network bandwidth, identify and troubleshoot resource problems.|

#### [[200.2 Predict Future Resource Needs]]
| | |
|---|---|
|**Weight**|2|
|**Description**|Candidates should be able to monitor resource usage to predict future resource needs.|

### _Topic 201: Linux Kernel_

#### [[201.1 Kernel components]]
| | |
|---|---|
|**Weight**|2|
|**Description**|Candidates should be able to utilise kernel components that are necessary to specific hardware, hardware drivers, system resources and requirements. This objective includes implementing different types of kernel images, understanding stable and longterm kernels and patches, as well as using kernel modules.|

#### [[201.2 Compiling a Linux kernel]]
| | |
|---|---|
|**Weight**|3|
|**Description**|Candidates should be able to properly configure a kernel to include or disable specific features of the Linux kernel as necessary. This objective includes compiling and recompiling the Linux kernel as needed, updating and noting changes in a new kernel, creating an initrd image and installing new kernels.|

#### [[201.3 Kernel runtime management and troubleshooting]]
| | |
|---|---|
|**Weight**|4|
|**Description**|Candidates should be able to manage and/or query a 2.6.x, 3.x or 4.x kernel and its loadable modules. Candidates should be able to identify and correct common boot and run time issues. Candidates should understand device detection and management using udev. This objective includes troubleshooting udev rules.|

### _Topic 202: System Startup_

#### [[202.1 Customizing system startup]]
| | |
|---|---|
|**Weight**|3|
|**Description**|Candidates should be able to query and modify the behaviour of system services at various targets / run levels. A thorough understanding of the systemd, SysV Init and the Linux boot process is required. This objective includes interacting with systemd targets and SysV init run levels.|

#### [[202.2 System recovery]]
| | |
|---|---|
|**Weight**|4|
|**Description**|Candidates should be able to properly manipulate a Linux system during both the boot process and during recovery mode. This objective includes using both the init utility and init-related kernel options. Candidates should be able to determine the cause of errors in loading and usage of bootloaders. GRUB version 2 and GRUB Legacy are the bootloaders of interest. Both BIOS and UEFI systems are covered.|

#### [[202.3 Alternate Bootloaders]]
| | |
|---|---|
|**Weight**|2|
|**Description**|Candidates should be aware of other bootloaders and their major features.|

### _Topic 203: Filesystem and Devices_

#### [[203.1 Operating the Linux filesystem]]
| | |
|---|---|
|**Weight**|4|
|**Description**|Candidates should be able to properly configure and navigate the standard Linux filesystem. This objective includes configuring and mounting various filesystem types.|

#### [[203.2 Maintaining a Linux filesystem]]
| | |
|---|---|
|**Weight**|3|
|**Description**|Candidates should be able to properly maintain a Linux filesystem using system utilities. This objective includes manipulating standard filesystems and monitoring SMART devices.|

#### [[203.3 Creating and configuring filesystem options]]
| | |
|---|---|
|**Weight**|2|
|**Description**|Candidates should be able to configure automount filesystems using AutoFS. This objective includes configuring automount for network and device filesystems. Also included is creating filesystems for devices such as CD-ROMs and a basic feature knowledge of encrypted filesystems.|

### _Topic 204: Advanced Storage Device Administration_

#### [[204.1 Configuring RAID]]
| | |
|---|---|
|**Weight**|3|
|**Description**|Candidates should be able to configure and implement software RAID. This objective includes using and configuring RAID 0, 1 and 5.|

#### [[204.2 Adjusting Storage Device Access]]
| | |
|---|---|
|**Weight**|2|
|**Description**|Candidates should be able to configure kernel options to support various drives. This objective includes software tools to view & modify hard disk settings including iSCSI devices.|

#### [[204.3 Logical Volume Manager]]
| | |
|---|---|
|**Weight**|3|
|**Description**|Candidates should be able to create and remove logical volumes, volume groups, and physical volumes. This objective includes snapshots and resizing logical volumes.|

### _Topic 205: Networking Configuration_

#### [[205.1 Basic networking configuration]]
| | |
|---|---|
|**Weight**|3|
|**Description**|Candidates should be able to configure a network device to be able to connect to a local, wired or wireless, and a wide-area network. This objective includes being able to communicate between various subnets within a single network including both IPv4 and IPv6 networks.|

#### [[205.2 Advanced Network Configuration]]
| | |
|---|---|
|**Weight**|4|
|**Description**|Candidates should be able to configure a network device to implement various network authentication schemes. This objective includes configuring a multi-homed network device and resolving communication problems.|

#### [[205.3 Troubleshooting network issues]]
| | |
|---|---|
|**Weight**|4|
|**Description**|Candidates should be able to identify and correct common network setup issues, to include knowledge of locations for basic configuration files and commands.|

### _Topic 206: System Maintenance_

#### [[206.1 Make and install programs from source]]
| | |
|---|---|
|**Weight**|2|
|**Description**|Candidates should be able to build and install an executable program from source. This objective includes being able to unpack a file of sources.|

#### [[206.2 Backup operations]]
| | |
|---|---|
|**Weight**|3|
|**Description**|Candidates should be able to use system tools to back up important system data.|

#### [[206.3 Notify users on system-related issues]]
| | |
|---|---|
|**Weight**|1|
|**Description**|Candidates should be able to notify the users about current issues related to the system.|

## Objectives: Exam 202 
### Topic 207: Domain Name Server
#### [[207.1 Basic DNS server configuration]]
| | |
|---|---|
|**Weight**|3|
|**Description**|Candidates should be able to configure BIND to function as an authoritative and as a recursive, caching-only DNS server. This objective includes the ability to manage a running server and configuring logging.|

#### [[207.2 Create and maintain DNS zones]]
| | |
|---|---|
|**Weight**|3|
|**Description**|Candidates should be able to create a zone file for a forward or reverse zone and hints for root level servers. This objective includes setting appropriate values for records, adding hosts in zones and adding zones to the DNS. A candidate should also be able to delegate zones to another DNS server.|

#### [[207.3 Securing a DNS server]]
| | |
|---|---|
|**Weight**|2|
|**Description**|Candidates should be able to configure a DNS server to run as a non-root user and run in a chroot jail. This objective includes secure exchange of data between DNS servers.|

### _Topic 208: HTTP Services_

#### [[208.1 Basic Apache configuration]]
| | |
|---|---|
|**Weight**|4|
|**Description**|Candidates should be able to install and configure a web server. This objective includes monitoring the server's load and performance, restricting client user access, configuring support for scripting languages as modules and setting up client user authentication. Also included is configuring server options to restrict usage of resources. Candidates should be able to configure a web server to use virtual hosts and customize file access.|

#### [[208.2 Apache configuration for HTTPS]]
| | |
|---|---|
|**Weight**|3|
|**Description**|Candidates should be able to configure a web server to provide HTTPS.|

#### [[208.3 Implementing Squid as a caching proxy]]
| | |
|---|---|
|**Weight**|2|
|**Description**|Candidates should be able to install and configure a proxy server, including access policies, authentication and resource usage.|

#### [[208.4 Implementing Nginx as a web server and a reverse proxy]]
| | |
|---|---|
|**Weight**|2|
|**Description**|Candidates should be able to install and configure a reverse proxy server, Nginx. Basic configuration of Nginx as a HTTP server is included.|

### _Topic 209: File Sharing_

#### [[209.1 Samba Server Configuration]]
| | |
|---|---|
|**Weight**|5|
|**Description**|Candidates should be able to set up a Samba server for various clients. This objective includes setting up Samba as a standalone server as well as integrating Samba as a member in an Active Directory. Furthermore, the configuration of simple CIFS and printer shares is covered. Also covered is a configuring a Linux client to use a Samba server. Troubleshooting installations is also tested.|

#### [[209.2 NFS Server Configuration]]
| | |
|---|---|
|**Weight**|3|
|**Description**|Candidates should be able to export filesystems using NFS. This objective includes access restrictions, mounting an NFS filesystem on a client and securing NFS.|

### _Topic 210: Network Client Management_

#### [[210.1 DHCP configuration]]
| | |
|---|---|
|**Weight**|2|
|**Description**|Candidates should be able to configure a DHCP server. This objective includes setting default and per client options, adding static hosts and BOOTP hosts. Also included is configuring a DHCP relay agent and maintaining the DHCP server.|

#### [[210.2 PAM authentication]]
| | |
|---|---|
|**Weight**|3|
|**Description**|The candidate should be able to configure PAM to support authentication using various available methods. This includes basic SSSD functionality.|

#### [[210.3 LDAP client usage]]
| | |
|---|---|
|**Weight**|2|
|**Description**|Candidates should be able to perform queries and updates to an LDAP server. Also included is importing and adding items, as well as adding and managing users.|

#### [[210.4 Configuring an OpenLDAP server]]
| | |
|---|---|
|**Weight**|4|
|**Description**|Candidates should be able to configure a basic OpenLDAP server including knowledge of LDIF format and essential access controls.|

### _Topic 211: E-Mail Services_

#### [[211.1 Using e-mail servers]]
| | |
|---|---|
|**Weight**|4|
|**Description**|Candidates should be able to manage an e-mail server, including the configuration of e-mail aliases, e-mail quotas and virtual e-mail domains. This objective includes configuring internal e-mail relays and monitoring e-mail servers.|

#### [[211.2 Managing E-Mail Delivery]]
| | |
|---|---|
|**Weight**|2|
|**Description**|Candidates should be able to implement client e-mail management software to filter, sort and monitor incoming user e-mail.|

#### [[211.3 Managing Mailbox Access]]
| | |
|---|---|
|**Weight**|2|
|**Description**|Candidates should be able to install and configure POP and IMAP daemons.|

### _Topic 212: System Security_

#### [[212.1 Configuring a router]]
| | |
|---|---|
|**Weight**|3|
|**Description**|Candidates should be able to configure a system to forward IP packet and perform network address translation (NAT, IP masquerading) and state its significance in protecting a network. This objective includes configuring port redirection, managing filter rules and averting attacks.|

#### [[212.2 Managing FTP servers]]
| | |
|---|---|
|**Weight**|2|
|**Description**|Candidates should be able to configure an FTP server for anonymous downloads and uploads. This objective includes precautions to be taken if anonymous uploads are permitted and configuring user access.|

#### [[212.3 Secure shell]]
| | |
|---|---|
|**Weight**|4|
|**Description**|Candidates should be able to configure and secure an SSH daemon. This objective includes managing keys and configuring SSH for users. Candidates should also be able to forward an application protocol over SSH and manage the SSH login.|

#### [[212.4 Security tasks]]
| | |
|---|---|
|**Weight**|3|
|**Description**|Candidates should be able to receive security alerts from various sources, install, configure and run intrusion detection systems and apply security patches and bugfixes.|

#### [[212.5 OpenVPN]]
| | |
|---|---|
|**Weight**|2|
|**Description**|Candidates should be able to configure a VPN (Virtual Private Network) and create secure point-to-point or site-to-site connections.|

## Future Change ConsiderationsFuture changes to the objective will/may include:[[Extend the amount of NetworkManager covered, i.e. including the CLI]]
[[lighttpd would have been too much coverage of web services. Perhaps reduce Apache next revision to make room.]]
[[host level IDS (tripwire, AIDE, etc) to be covered in future LPIC-1.]]
[[introduction (or more) to FreeIPA]]
[[add coverage of mod_security and mod_evasive to Apache HTTP (maybe as a separate topic: Web Application Firewall)]]
[[add coverage of a higher-level firewall package like firewalld or ufw]]
[[Reconsider mod_perl]]
[[Add firewall-cmd and /etc/firewalld/firewalld.conf related to firewalld to LPIC-2]]
[[Awareness of firewalld]]
[[Add nmcli and nmtui to LPIC-2]]
[[Full coverage of IPv6 auto configuration]]
[[Remove djbdns]]
[[Advanced shell scripting (sed -e, set -x, set -o, pipefail, PIPESTATUS, declare)]]
[[Filesystem quota (similar to the topic removed from LPIC-1)]]
[[Understanding of consistency in backups, e.g. for databases]]
[[Let's Encrypt for certification procurement]]
[[202.2: Reconsider NVMe booting]]
[[207.1: Consider dropping djbdns and consider unbound]]
[[207.1: /var/named/ is distro-specific]]
[[207.2: Remove creation of root.hints]]
[[207.2: Reconsider nslookup]]
[[207.3: Reconsider chroot]]
[[208.2: Remove CA.pl]]
[[208.2: Remove SNI specialties]]
[[208.2: Remove client certificate options]]
[[208.3: Reconsider the relevance of Squid]]
[[209.1: Remove Samba Share-Level security]]
[[209.1: Remove nmblookup]]
[[210.1: Remove arp]]
[[210.4: Aggregate Whitepages, schemas, classes etc.]]
[[212.2: Remove FTP]]
[[212.3: Remove Protocol]]
[[212.4: Remove bugtraq etc.]]
[[Remove paths to commands and configuration files wherever possible]]
