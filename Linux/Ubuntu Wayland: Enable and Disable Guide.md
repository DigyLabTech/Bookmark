https://linuxconfig.org/how-to-enable-disable-wayland-on-ubuntu-22-04-desktop

Skip to content
LinuxConfig
Home
Linux Commands
Tools
Forum
Resources
About Us
Ubuntu Wayland: Enable and Disable Guide
28 November 2025 by Korbin Brown
Wayland is a communication protocol that specifies the communication between a display server and its clients. On Ubuntu, users can choose to enable or disable Wayland according to their needs. By default, Ubuntu’s desktop environment runs on Wayland, but it is also possible to switch to the Xorg display server. This tutorial will demonstrate how to enable and disable Wayland on the Ubuntu desktop.

Reasons for using Xorg instead of Wayland are if you are encountering graphical errors or performance issues while using Wayland. Wayland does not always play nicely with every kind of software. Xorg is the safe fall back choice whenever you are having problems with Wayland. Since both are included on Ubuntu and installed by default, it is relatively easy to switch back and forth between them.

Table of Contents
→ How to Enable/Disable Wayland
→ Conclusion
→ Frequently Asked Questions
In this tutorial you will learn:
How to enable Wayland
How to disable Wayland
How to verify which display server is active
Ubuntu desktop terminal showing Wayland and X11 display server configuration with GDM3 settings file
Configure Wayland or X11 display server by editing GDM3 configuration file on Ubuntu system
Software Requirements and Linux Command Line Conventions
Category	Requirements, Conventions or Software Version Used
System	Ubuntu 18.04, 20.04, 22.04, 24.04 Desktop
Software	GNOME desktop environment, Wayland
Other	Privileged access to your Linux system as root or via the sudo command.
Conventions	# – requires given linux commands to be executed with root privileges either directly as a root user or by use of sudo command
$ – requires given linux commands to be executed as a regular non-privileged user
TL;DR
Enable or disable Wayland on Ubuntu by editing /etc/gdm3/custom.conf and setting WaylandEnable=true or WaylandEnable=false.
Quick Steps to Enable/Disable Wayland on Ubuntu
Step	Command/Action
1. Edit GDM3 configuration	sudo nano /etc/gdm3/custom.conf
2. Set Wayland option	WaylandEnable=true or WaylandEnable=false
3. Restart display manager	sudo systemctl restart gdm3 OR sudo reboot
4. Verify active display server	echo $XDG_SESSION_TYPE
How to enable/disable wayland on Ubuntu Desktop step by step instructions
DID YOU KNOW?
Users may want to enable or disable Wayland due to application compatibility. Some applications still lack support for Wayland, so Ubuntu gives users the option to enable X display server to resolve these types of issues.
Edit the GDM3 configuration file: The default display manager for the GNOME desktop environment is GDM3. Therefore, we will edit the /etc/gdm3/custom.conf file to either disable or enable Wayland. Open a command line terminal and use nano or your favorite text editor to open this file with root permissions.
$ sudo nano /etc/gdm3/custom.conf
Configure Wayland settings: Within this file, look for the line that says #WaylandEnable=false. You can uncomment this line and either set it to true or false, depending on whether you want Wayland enabled or not.Enable Wayland:
WaylandEnable=true
Or disable Wayland:

WaylandEnable=false
X11 STABILITY NOTE
In my testing, some Ubuntu 24.04 systems experience intermittent black screen issues when using X11. Wayland is the recommended default display server for stability and performance on newer Ubuntu versions. Avoid using X11 if possible, as the situation may worsen with future Ubuntu releases..

Terminal window displaying GDM3 custom.conf file with WaylandEnable=false configuration setting on Ubuntu
GDM3 custom.conf file opened in nano editor showing WaylandEnable=false setting to force X11 display server
Restart the display manager: After you have made the desired changes, save this file and exit it. You will need to restart GDM3 or reboot your Ubuntu desktop for the changes to take effect.
$ sudo systemctl restart gdm3
Verify the active display server: Confirm which display server you are currently using with the following command:
$ echo $XDG_SESSION_TYPE
This will output either wayland or x11, confirming which display server is active. You can run this command before making changes to check your current setup, and again after restarting GDM3 to verify the switch was successful.

Terminal showing echo $XDG_SESSION_TYPE command output displaying x11 on Ubuntu desktop
Terminal output showing x11 as the active display server after checking XDG_SESSION_TYPE variable
Select display server at login: To login to Ubuntu Desktop using Wayland, click on the gear button and select Ubuntu option before you login. If you have disabled the Wayland display server, you will only see the Xorg option appear, or the gear button doesn’t show up at all.
UBUNTU WAYLAND VS X11
Ubuntu supports two display server protocols: Xorg and Wayland. Xorg is the older, traditional server known for broad compatibility but is less secure and efficient compared to modern standards. Wayland, introduced as the default in Ubuntu 17.10, simplifies this model by handling rendering through clients, enhancing performance, reducing latency, and improving security by isolating applications. However, Wayland can face compatibility issues with older software, necessitating occasional fallbacks to Xorg. This transition highlights Ubuntu’s move towards a more secure and robust user experience while maintaining support for a wide range of applications.
Login to Ubuntu using Wayland display server
Login to Ubuntu using Wayland display server
Conclusion
In this tutorial, we saw how to enable or disable the Wayland communication protocol in Ubuntu Desktop Linux. Having more than one option is a good thing for Linux users, as they all have their pros and cons and one may work better with a certain configuration than another. By offering both Xorg and Wayland, Ubuntu ensures that users can choose the most suitable environment based on their specific hardware and software needs. This flexibility not only enhances user satisfaction but also broadens Ubuntu’s appeal as a versatile and adaptable operating system. Whether prioritizing performance and security with Wayland or ensuring maximum compatibility with Xorg, users can tailor their setup to provide the optimal desktop experience.

Frequently Asked Questions
How do I check if I’m currently using Wayland or X11 on Ubuntu? You can verify your active display server by running the command echo $XDG_SESSION_TYPE in the terminal. This will return either wayland or x11, indicating which display server is currently in use. This command works on all recent Ubuntu versions including 24.04.
Do I need to reboot Ubuntu after enabling or disabling Wayland? No, a full system reboot is not required. After editing the /etc/gdm3/custom.conf file, you only need to restart the GDM3 display manager with sudo systemctl restart gdm3. This will log you out and apply the changes immediately. However, rebooting your system will also work if you prefer that option.
Why would I want to disable Wayland on Ubuntu? There are several reasons to disable Wayland and use Xorg instead. Some applications, particularly older software or certain screen recording tools, may not work properly with Wayland. You may also experience compatibility issues with specific graphics drivers, remote desktop applications, or screen sharing software. If you encounter graphical glitches, performance problems, or application crashes on Wayland, switching to Xorg is the recommended troubleshooting step.
What is the difference between Wayland and Xorg on Ubuntu? Wayland is the newer display server protocol that offers improved security, better performance, and reduced input latency compared to Xorg. Wayland isolates applications from each other, preventing them from capturing screen content without permission. However, Xorg has broader application compatibility since it has been around much longer. Ubuntu defaults to Wayland on systems with compatible hardware, but includes Xorg as a fallback option for maximum compatibility.
Related Posts:
Wayland Display Server Guide on Ubuntu 26.04
Choosing the right Linux File System Layout using a…
Ultimate Web Server Benchmark: Apache, NGINX,…
How to Install X11 on Ubuntu 26.04
PROUHD: RAID for the end-user.
Ubuntu Torrent: Best Clients Compared
CategoriesUbuntu
Tagsdesktop, ubuntu
How to install Gnome Shell Extensions on Ubuntu 22.04 Jammy Jellyfish Linux Desktop
How to install and manage fonts on Linux
Featured Linux Job
LinuxCareers - All Linux jobs. One job board.
Posted by a recruiting partner on LinuxCareers (job board)

Senior Linux Systems Administrator
Verified Recruiting Partner

📍 London, United Kingdom · New York, United States
🏢 Full-time  |  Compensation not disclosed

Hands-on, high-ownership Linux systems administration role for an investment firm, covering troubleshooting and root-cause analysis, scripting and automation, and physical hardware work. All infrastructure is on-premises, with no cloud. Frequent international travel required.

View Job Details
NEWSLETTER
Master Linux with our comprehensive tutorials and guides. Get step-by-step Linux tutorials covering commands, administration, and best practices delivered to your inbox.

Subscribe Now
LINUX CAREERS
Find Linux jobs and advance your career in system administration, DevOps, and open-source technologies. Browse opportunities that value Linux tutorial expertise.

Browse Jobs
TAGS
bash centos commands database debian desktop docker fedora gaming Hardware kernel networking nvidia programming rhel security server ubuntu virtualization
LATEST UPDATES
Linux Mint 23: Release Date and New Features
Ubuntu Download: All Ubuntu Versions and Flavors
Ubuntu 22.04 Download
Ubuntu 26.04 Download: All Flavors
Ubuntu 24.04 download – All Official Flavors
Ubuntu 26.04: Release Date and New Features in Resolute Raccoon
How to Install Nvidia Drivers on Ubuntu 26.04
How to Install the LAMP Stack on Ubuntu 26.04
Rayhunter Tutorial: Convert a Verizon Orbic Speed RC400L into a Stingray Detector
How to Change Default Desktop Environment on Ubuntu 26.04
How to Set Up NFS Server and Client on Ubuntu 26.04
How to Install and Configure PHP on Ubuntu 26.04
How to Install and Configure PostgreSQL on Ubuntu 26.04
How to Configure nftables Firewall on Ubuntu 26.04
How to Set Up Samba File Sharing on Ubuntu 26.04
How to Configure Dracut Initramfs on Ubuntu 26.04
How to Install Brave Browser on Ubuntu 26.04
How to Install Visual Studio Code on Ubuntu 26.04
How to Install and Secure MySQL on Ubuntu 26.04
How to Install Desktop Environment on Ubuntu 26.04
LATEST TUTORIALS
How to Install Desktop on Ubuntu Server 26.04
How to Flash Server BIOS Using a Bootable DOS USB on Linux
Linux Mint 23: Release Date and New Features
How to Change SSH Port on Ubuntu 26.04
How to Fix SSH Connection Refused on Ubuntu 26.04
How to Install Node.js on Ubuntu 26.04
Wayland Display Server Guide on Ubuntu 26.04
How to Install Xfce on Ubuntu 26.04
How to Install X11 on Ubuntu 26.04
How to Install KDE Plasma on Ubuntu 26.04
How to Use Sudo Command on Ubuntu 26.04
ZFS File System Guide on Ubuntu 26.04
How to Enable Firewall In Terminal on Ubuntu 26.04
How to Install ZFS on Ubuntu 26.04
How to Set Up NTP Server on Ubuntu 26.04
UFW Firewall Configuration Guide on Ubuntu 26.04
Install UFW: How to Set Up a Basic Firewall on Linux
whois-app-tool
How to Set Up SSH Server on Ubuntu 26.04 (Hardened Production Ready)
How to Disable Firewall on Ubuntu 26.04
How to Change Hostname on Ubuntu 26.04
How to Configure Static IP with Netplan on Ubuntu 26.04 Server
© 2026 - LinuxConfig.org
