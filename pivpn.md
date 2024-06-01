# Setting Up DDNS on No-IP and Installing WireGuard VPN Using PiVPN on Port 1337

In this tutorial, we'll walk through setting up Dynamic DNS (DDNS) on No-IP and installing WireGuard VPN using PiVPN on a Raspberry Pi. This guide assumes you have basic knowledge of Linux commands and network configurations.

## Prerequisites
- A Raspberry Pi with Raspbian installed
- A No-IP account
- Internet access
- A public IP address

## Step 1: Setting Up DDNS on No-IP

Dynamic DNS (DDNS) allows you to map a dynamic IP address to a static hostname. This is useful if your ISP changes your IP address frequently.

### 1.1 Create a No-IP Account
1. Go to [No-IP's website](https://www.noip.com/) and sign up for a free account.
2. Confirm your email address.

### 1.2 Create a Hostname
1. Log in to your No-IP account.
2. Navigate to `Dynamic DNS` > `Add Hostname`.
3. Enter a hostname (e.g., `myhome.no-ip.org`).
4. Select a domain.
5. Click `Save Hostname`.

### 1.3 Install the No-IP DUC (Dynamic Update Client)
1. Open a terminal on your Raspberry Pi.
2. Download the No-IP DUC:

   ```bash

    cd /usr/local/src
    sudo wget https://www.noip.com/client/linux/noip-duc-linux.tar.gz
    sudo tar xf noip-duc-linux.tar.gz
    cd noip-2.1.9-1
    sudo make
    sudo make install
    
    ```

4. Configure the No-IP DUC:
    ```bash
    
    sudo /usr/local/bin/noip2 -C

    ```
5. Enter your No-IP account credentials when prompted.
6. To start the No-IP DUC client:
    ```bash

    sudo /usr/local/bin/noip2

    ```
    
7. To ensure it runs on startup, add the following to `/etc/rc.local`:
    ```bash

    sudo nano /etc/rc.local

    ```

   Add before the `exit 0` line:
    ```bash
    /usr/local/bin/noip2
    ```

## Step 2: Installing WireGuard VPN Using PiVPN

WireGuard is a modern, fast, and secure VPN protocol. PiVPN makes the installation of WireGuard easy.

### 2.1 Update Your System
1. Update and upgrade your system:
    ```sh
    sudo apt update
    sudo apt upgrade -y
    ```

### 2.2 Install PiVPN
1. Install PiVPN:
    ```sh
    curl -L https://install.pivpn.io | bash
    ```
2. Follow the on-screen prompts:
    - Select `WireGuard`.
    - For the local user, select the default user (e.g., `pi`).
    - When prompted for the port, enter `1337`.
    - Confirm and proceed with the installation.

### 2.3 Configure Your Router
1. Log in to your router's web interface.
2. Navigate to the port forwarding section.
3. Add a new rule to forward UDP port `1337` to the internal IP address of your Raspberry Pi.

### 2.4 Generate WireGuard Client Configuration
1. On your Raspberry Pi, generate a new client profile:
    ```sh
    pivpn add
    ```
2. Follow the prompts to create a client profile (e.g., `myclient`).

### 2.5 Retrieve the Configuration File
1. The configuration file will be saved in `/home/pi/configs/` (or the home directory of the selected user).
2. Transfer the configuration file to your client device (e.g., via SCP, email, or USB drive):
    ```sh
    scp pi@your_pi_ip:/home/pi/configs/myclient.conf /local/path/
    ```

### 2.6 Install WireGuard on Your Client Device
1. Install the WireGuard app on your client device (available for Windows, macOS, Linux, iOS, and Android).
2. Import the configuration file `myclient.conf` into the WireGuard app.

### 2.7 Connect to Your VPN
1. Open the WireGuard app on your client device.
2. Select the imported configuration and connect.

## Conclusion

You have successfully set up Dynamic DNS with No-IP and installed WireGuard VPN using PiVPN on port 1337. Your Raspberry Pi is now ready to provide secure VPN access with a consistent hostname.

Feel free to leave comments if you encounter any issues or have questions!
