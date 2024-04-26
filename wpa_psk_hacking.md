---
title: WPA-PSK Hacking Guide
layout: default
nav_order: 5
---

# Wi-Fi Network Hacking Guide (Educational)

When you enable Wi-Fi in public places, you'll encounter numerous networks that likely utilize WPA-PSK encryption. Although these networks are susceptible to hacking, it is crucial to emphasize that this guide is strictly for educational purposes. Engaging in these activities on networks without proper authorization is illegal. Having addressed this disclaimer, let's explore the underlying mechanisms, the practical execution, and measures to safeguard yourself against such vulnerabilities.

## Introduction

When you connect to a network from a wireless device, a `handshake` is sent from the device to the router. This handshake contains the encrypted password.

While it's not possible to reverse the encrypted password, you can use a technique called a word list attack. A word list is a huge text file containing thousands of passwords. By comparing the encrypted handshake password with the passwords in the word list, you can determine the real password.

## Requirements
For this guide, to perform Wi-Fi network hacking, you'll need:
- Computer running `Linux` distribution;
- Computer with a network card that supports `monitor mode`;
- Install the package `Aircrack-ng` with the command `sudo apt install aircrack-ng`;

## Procedure
### 1 - Determine the Network Interface
Identify the wireless network interfaces, which usually start with w (e.g., wlp3s0).
<br>This information will be needed later.
<br>Open a terminal and type:

```
ip a
```

> _The "ip a" command in Linux displays network interface information, including IP addresses, MAC addresses, and related configurations. It is used for troubleshooting and network configuration purposes._

### 2 - Enable Monitor Mode
Use the airmon-ng tool to switch your network card to monitor mode.
<br>It will break your internet connection temporarily.
<br>Enter the command:

```
airmon-ng start <wireless interface>
```

### 3 - Verify Monitor Mode
Now, the wireless interface should be displayed as `<interface>mon` (e.g., wlp3s0mon).
<br>If not, it means your network card doesn't support monitor mode, and you'll need the external network card mentioned earlier.
<br>Run the command in a terminal to check if the network card's mode has changed to monitor.

```
iwconfig
```
It should appear `Mode: Monitor`.

### 4 - Scan for Networks
Use airodump-ng to view the networks around you.
<br>This command will display a list of nearby networks along with their BSSIDs (network MAC addresses) and channels.
<br>Enter the command:

```
airodump-ng <wireless interface>mon
```

### 5 - Target Network
Identify the BSSID and channel of the network you wish to attack.

### 6 - Capture the Handshake
This command will show all the devices currently connected to that network.
<br>If you watch a video in one of this devices, the amount of packets (frames) being set to a device increses a lot. 
<br>In a new terminal window, enter the command:

```
airodump-ng -d(--bssid) <BSSID> -w(--write) <filename> -c(--channel) <channel>  <wireless interface>mon
```
- `<BSSID>` - target network's BSSID;
- `<channel>` - target network's channel;
- `<filename>` - desired name for the captured handshake file;
- `<wireless interface>mon` - name of your wireless interface in monitor mode;

### 7 - Deauthentication Attack
Now we need to to send deauthentication packets to the victim's device, forcing it to disconnect and reconnect to the network so we can capture the handshake.
<br>Leave the previous terminal open and running.
<br>Use this command in another terminal:

```
aireplay-ng -0 10 -a <BSSID> -c <client ESSID> <wireless interface>mon
```
- `-0 10` - deauthentication and we gonna send 10 packets;
- `-a <BSSID>` - target network's BSSID;
- `-c <client ESSID>` - ESSID (name) of the device you want to deauthenticate (e.g., the victim's device);
- `<wireless interface>mon` - name of your wireless interface in monitor mode;

### 8 - Capture the Handshake
Observe the terminal running `airodump-ng` (step 6) and wait for a device to reconnect.
<br>Once the handshake is captured, you can see a message saying `WPA handshake: <BSSID>`.
<br>You can stop `airodump-ng` by pressing `Ctrl+C`.
<br>The captured handshake will be saved in the specified filename.

### 9 - Word List Attack
Kali Linux comes with pre-installed word lists located in the directory `/usr/share/wordlists`.
<br>If you are not on Kali, you can download a word list from here.
<br>Now let's attempt to match the captured handshake with passwords from the word list.
<br>Use the command:

```
aircrack-ng -w <wordlist> <filename>
```

- `<wordlist>` - path to the desired word list file (e.g., /usr/share/wordlists/rockyou.txt);
- `<filename>` - name of the captured handshake file;

### 10 - Cracked!
Note: After performing these steps, your internet connection may still be interrupted. To fix this, you can either restart your computer or execute the command airmon-ng stop <monitor interface> followed by systemctl restart network* to restart the network services.

## Protecting Yourself
While you cannot prevent the authentication process, you can protect against word list attacks by choosing a long and random password that is unlikely to be found in any word list.

## Conclusion
In this guide, we explored the process of Wi-Fi network hacking for educational purposes only. It is essential to respect privacy and legality when using these techniques. We discussed capturing handshakes, performing de-authentication attacks, and cracking passwords using word lists. Remember to always use this knowledge responsibly and protect yourself by setting strong passwords for your Wi-Fi networks.

If you found this guide helpful, feel free to leave a star, and thank you for reading!
