# Using Remote Desktop Connection to Use a Lab Computer while Remote

This tutorial is designed to let a user either SSH (command line interface) or XRDP (full desktop interface) into a computer that is running Ubuntu 24.04 or higher. This would allow you to remote in and use attached systems or access local data from a remote location.

The computer you use does not have to be Ubuntu or any flavor of Linux - the only parts specific to 

> [!WARNING]
> Remote connections always represent a security risk and you must follow proper protocols to ensure you do not leave your host or controller system open to network attacks. ALWAYS use strong passwords (32+ characters) or use an SSH Key to reduce your risk and limit network access using a firewall. Preferably, you should be connecting via a secure VPN or only on the Local Area Network (LAN).

## Subsection 1: Configure your Ubuntu Computer to Accept Remote Connections

### 1.1: Firewall
Avoid leaving your Ubuntu computer vulnerable by turning on your firewall and selectively activating specific ports that can only communicate over specific networks and protocols. To turn on your firewall, use:
```py
sudo ufw enable
```

This will activate your firewall and block ALL ports from accepting requests. Selectively allow the following ports to remote connect:
```py
sudo ufw allow from any to any port 3389 proto tcp      # Allows all requests to 3389; default port for SSH and XRDP.
sudo ufw allow from any to any port 3390 proto tcp      # (Optional) Allows all requests to 3390; backup default port for SSH and XRDP.
```

### 1.2: Local NAT Settings (Optional, LAN Connections Only)

If you want to access a computer over Ethernet LAN without an internet connection, you may have to tweak some settings in your ethernet.

As Ubuntu 24 and 25 gives you an easy interface, go to "Settings" followed by "Network" and locate your ethernet connection. Select the settings cog and navigate to the "IPV4" tab. Select "Shared to Other Computers" and select "Apply"; if this worked, you should see a network speed associated with the ethernet port.

With these rules in place, you can proceed to installing or running your remote connection.

### 1.3 Get your IP Address.

You can do this multiple ways, but all of them are easy.

1) Go to "settings" and either "Wifi" or "Network" and select the cog next to the connection you're interested in. Under "Details", you will see the IPV4 address you will use to connect.
2) Via commandline, type
   > ```py
   > ip a
   > ```
   and locate the IP of the connection you will use.
3) Using Net-Tools (more Advanced options). Via command line, type
   > ```py
   > sudo apt install net-tools
   > ```
   After install, run the following command:
   > ```py
   > ifconfig
   > ```
   and locate the IP of the connection you will use. You can also configure the connection using Net-Tools if you need something more specific.

## Subsection 2: Connecting to your Ubuntu Computer

Remoting in to modern versions of Ubuntu 24.04 and 25 is surprisingly easy, and you can even perform these via the user interface.

To quickly activate these options, navigate to "Settings" followed by "System"; you will see multiple potential options. You can enable SSH, Remote Desktop, or both. Generally, I'd reccomend sticking with "Remote Desktop Connection" as it gives you the most options.

When you select "Remote Desktop Connection", you will be faced with two options: "Desktop Sharing" and "Remote Login". Select which one you want to use and configure a unique username and password for the connection; this will not be your user username and password and will actually ONLY be for remote connection. Once connected, you will still have to log in with your local user credentials.

> [!NOTE]
> Desktop Sharing shares an active user's desktop and requires that you be signed in. Think of it like AnyDesk but built into Ubuntu.
> Remote Login lets any remote user who is not currently logged in to enter and access the desktop like they are currently there, but does not allow someone physically next to the computer to see that you are logged in.

### 2.1: XRDP - A Full Remote Desktop

This is the most complex way to connect to a remote computer and it will give you full access to the user interface.

### 2.2: SSH - Command Line Connection

This is the most minimal way to connect to a remote computer. This is useful for tansferring files or performing minimal tasks not requiring interactions with a user interface. Generally, you want to use XRDP if you want to perform work on the host computer.

## Subsection 3: Connect via a VPN or Enter your Local Network

### Linux Users


### Mac Users


### Windows Users
