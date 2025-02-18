# How to set up Pi-hole on Debian based systems for network-wide ad blocking

[Pi-hole](https://pi-hole.net/) is a powerful network-wide ad blocker that works by acting as a DNS sinkhole, blocking unwanted content such as advertisements and trackers across all devices in your network. It's designed for low-power devices like the Raspberry Pi but can be installed on most Linux machines. This guide will walk you through installing and configuring Pi-hole on a Debian 12 system.

**Prerequisites**

-A machine running Debian 12

-A static IP address for your machine.

-Internet access.

-Root privileges (sudo).

**Step 1: Make sure your system is up to date:**

Before starting, it is best practice to update your system. Open a terminal and run the following commands:

```
sudo apt update
sudo apt dist-upgrade
sudo shutdown now -r
```

This will update all your installed packages and reboot the system if necessary.

**Step 2: Install Pi-hole**

Pi-hole can be installed easily via a one-line installation script. Run the following command to start the installation:

```
curl -sSL https://install.pi-hole.net | bash
```
The script will automatically download and install Pi-hole. During the installation, you'll be prompted with various configuration options:

  1. Static IP Address: Ensure that your machine has a static IP address. Pi-hole will display your current IP during installation, and you need this to configure Pi-hole’s web interface and DNS settings.
  2. DNS Provider: If you are not using a custom DNS server like Unbound, choose one of the default DNS providers for Pi-hole to use.
  3. Password for Admin Console: Note the admin password displayed at the end of the installation. You'll use this to access Pi-hole’s web interface.

**Step 3: Configure Router’s DNS Settings**

To ensure Pi-hole is used network-wide, you need to configure your router to point to Pi-hole’s IP address for DNS resolution.

  1. Log into your router’s web interface. This is usually done by navigating to http://192.168.0.1 or http://192.168.1.1 in a browser (check your router's manual if these don't work).
  2. Find the DHCP Settings section (often under Advanced Settings).
  3. Change the Primary DNS setting to the static IP address of your Debian machine running Pi-hole.

This ensures that all devices on your network will use Pi-hole for DNS resolution, allowing Pi-hole to block ads and trackers across your network.

**Step 4: Access the Pi-hole Web Interface**

After installation, you can access Pi-hole's web interface by navigating to:

```
http://[PiHole_IP]/admin
```
Log in using the password displayed during installation. From here, you can manage Pi-hole settings, view statistics, and add blocklists.

**Step 5: Adding Blocklists to Pi-hole**

Pi-hole uses blocklists to filter out unwanted content like ads, trackers, and malicious domains. Below are several recommended blocklists to improve Pi-hole’s ad-blocking capabilities.

   1. Log into the Pi-hole Admin Interface: Go to http://[YourPiIP]/admin and log in.

   2. Navigate to Group Management > Adlists: In the Pi-hole admin interface, go to Group Management and then Adlists.

   3. Add the Following Blocklists
   
Copy the URLs below, one by one, and paste them into the Address field, then click Add for each list.

Recommended Blocklists:

   AdGuard DNS Blocklist: This extensive blocklist targets ads and trackers, maintained by AdGuard. It blocks a wide variety of domains, providing effective ad-blocking across websites and applications
   https://v.firebog.net/hosts/AdguardDNS.txt

   StevenBlack's KADhosts List: This list is part of the unified hosts project by StevenBlack. It focuses on blocking domains related to advertising and trackers.
   https://raw.githubusercontent.com/StevenBlack/hosts/master/data/KADhosts/hosts

   StevenBlack's Spam Blocklist: Designed to block known spam and phishing domains, this list protects you from malicious websites and email-related threats.
   https://raw.githubusercontent.com/StevenBlack/hosts/master/data/add.Spam/hosts

   4. Update Gravity: After adding the blocklists, go to Tools > Gravity and click on Update. This will refresh Pi-hole’s database with the new blocklist entries, and it may take a few minutes to complete.

**Step 6: Troubleshooting**

If you encounter issues with blocked websites or apps, you can:

   Check Pi-hole Logs: The Pi-hole logs can show which domains are being blocked. You can access them via the Pi-hole admin interface or by running:

```
tail -f /var/log/pihole.log
```
   Whitelist Domains: If a legitimate site is being blocked, search for the blocked domain in Pi-hole’s admin interface and whitelist it.

**Conclusion**

By following these steps, you've successfully set up Pi-hole on Debian 12 to block ads and trackers across your network. With Pi-hole installed and blocklists in place, your devices should enjoy a smoother, ad-free browsing experience. Remember to periodically update your blocklists and review the Pi-hole logs to maintain the best blocking performance.

Feel free to further enhance your Pi-hole setup by integrating it with additional security features like DNS-over-HTTPS (DoH) or configuring it with a local DNS resolver like Unbound for a more private and secure DNS setup.
