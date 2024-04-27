---
title: WPA-PSK Hacking
permalink: /wpa_psk_hacking/
layout: default
nav_order: 5
---

# **WPA-PSK HACKING**

When you enable Wi-Fi in public places, you'll encounter numerous networks that likely utilize **WPA-PSK (Wi-Fi Protected Access Pre-Shared Key) encryption**, which is commonly used in wireless networks to secure data transmission.

While it offers a level of security, there are **vulnerabilities** to consider. This guide will explore one of the most common methods of hacking **WPA-PSK** networks.

{: .warning-title }
Although these networks are susceptible to hacking, it is crucial to emphasize that this guide is **strictly for educational purposes**. Engaging in these activities on networks without proper authorization is **illegal**. This is for **educational purposes only**. Having addressed this disclaimer, let's explore the underlying mechanisms, the practical execution, and measures to safeguard yourself against such vulnerabilities.

## **Introduction**

When you connect to a network from a wireless device, a **handshake** is sent from the device to the **router**. This **handshake** contains the **encrypted password**.

While it's not possible to reverse the **encrypted password**, you can use a technique called a **word list attack**. A word list is a huge text file containing **thousands of passwords**. By comparing the encrypted **handshake** password with the passwords in the word list, you can determine the real password.

## **Requirements**

- `Linux` distro distribution;
- PC with a network card that supports `monitor mode`;
- Install the package `Aircrack-ng` with the command `sudo apt install aircrack-ng`;

## **Procedure**

### **Determine the Network Interface**

<div class="code-example" markdown="1">
Identify the wireless network interfaces, which usually start with (e.g. `wlp3s0`).
<br>This information will be needed later.
</div>
```bash
ip a
```

{: .important-title }
The "ip a" command in Linux displays network interface information, including **IP addresses**, **MAC addresses**, and **related configurations**. It is used for troubleshooting and network configuration purposes.

### **Enable Monitor Mode**

<div class="code-example" markdown="1">
Use the `airmon-ng` tool to switch your network card to monitor mode.
<br>It will break your internet connection temporarily.
</div>
```bash
airmon-ng start <wireless interface>
```

### **Verify Monitor Mode**

<div class="code-example" markdown="1">
Now, the wireless interface should be displayed as `<interface>mon` (e.g., `wlp3s0mon`).
<br>Run the command and It should appear `Mode: Monitor`.
</div>
```bash
iwconfig
```

{: .important-title }
If the wireless interface doesn't appear, it means your network card **doesn't support monitor mode**, and you'll need the external network card mentioned earlier.

### **Scan for Networks**

<div class="code-example" markdown="1">
Use `airodump-ng` to view the networks around you.
<br>This command will display a list of nearby networks along with their `BSSIDs` **(Network MAC Addresses)** and `channels`.
</div>
```bash
airodump-ng <wireless interface>mon
```

### **Target Network**

<div class="code-example" markdown="1">
Identify and copy/save the `BSSID` and `channel` of the network you wish to attack.
</div>

### **Capture the Handshake**

<div class="code-example" markdown="1">
This command will show all the devices currently connected to that network and the amount of `packets` being sent to each device.
<br>For example, watching a video will increase the number of packets sent to the device by a lot.
<br>Type this command in a new terminal window:
</div>
```bash
airodump-ng -d(--bssid) <BSSID> -w(--write) <filename> -c(--channel) <channel>  <wireless interface>mon
```

- `<BSSID>` - target network's BSSID;
- `<channel>` - target network's channel;
- `<filename>` - the desired name for the captured handshake file;
- `<wireless interface>mon` - the name of your wireless interface in monitor mode;

### **Deauthentication Attack**

<div class="code-example" markdown="1">
Now we need to to send `de-authentication packets` to the victim's device, forcing it to disconnect and reconnect to the network, so we can capture the `handshake`.
<br>Leave the previous terminal open (running) and use this command in another terminal:
</div>
```bash
aireplay-ng -0 10 -a <BSSID> -c <client ESSID> <wireless interface>mon
```

- `-0 10` - number of de-authentication packets to send;
- `-a <BSSID>` - target network's BSSID;
- `-c <client ESSID>` - ESSID (name) of the device you want to de-authenticate;
- `<wireless interface>mon` - the name of your wireless interface in monitor mode;

### **Capture the Handshake**

<div class="code-example" markdown="1">
Observe the terminal running `airodump-ng` capture the `handshake` and wait for the device to reconnect.
<br>Once the handshake is captured, you can see a message saying `WPA handshake: <BSSID>`.
<br>You can stop `airodump-ng` by pressing `Ctrl+C`.
<br>The captured handshake will be saved in the specified filename.
</div>

### **Word List Attack**
<div class="code-example" markdown="1">
Kali Linux comes with pre-installed word lists located in the directory `/usr/share/wordlists`.
<br>If you are not on Kali, you can download a word list from [here](https://www.kali.org/tools/wordlists).
<br>Now let's attempt to match the captured handshake with passwords from the word list.
</div>
```bash
aircrack-ng -w <wordlist> <filename>
```

- `<wordlist>` - path to the desired word list file (e.g. **/usr/share/wordlists/rockyou.txt**);
- `<filename>` - name of the captured **handshake** file;

### **Cracked!**
<div class="code-example" markdown="1">
Congratulations! If the password is found in the word list, it will be displayed.
<br>After performing these steps, your internet connection may still be interrupted.
<br>To fix this, you can either restart your computer or execute the command:
</div>
```bash
airmon-ng stop <monitor interface>
systemctl restart network*
```

## **Protecting Yourself**
While you cannot prevent the authentication process, you can protect against word list attacks by choosing a long and random password that is unlikely to be found in any word list, like **passphrases**. Additionally, you can enable **MAC address filtering** and **WPS (Wi-Fi Protected Setup)** to enhance security.

## **Conclusion**
We explored the process of WPA-PSK hacking. It is essential to respect **privacy** and **legality** when using these techniques. We learned about capturing **handshakes**, performing **de-authentication attacks**, and cracking passwords using **word lists**. Remember to always use this knowledge responsibly and protect yourself.