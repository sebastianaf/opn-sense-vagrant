
# OPNsense Configuration with Vagrant

This repository contains the files necessary to create and configure a virtual machine with OPNsense using Vagrant. The virtual machine is configured with two network interfaces (WAN and LAN) in bridge mode and with DHCP enabled by default. This procedure allows you to update the OPNsense ISO without having to download an unofficial box, as OPNsense does not provide an official box.

## Steps to Create and Configure the Virtual Machine

### 1. Create the Vagrant Box

1. Download the OPNsense ISO from the [official site](https://opnsense.org/download/).
2. Create a new virtual machine in VirtualBox and install OPNsense from the ISO.
3. Configure the LAN interface with a static IP address for initial access.
4. Enable SSH access and note the credentials.
5. Power off the virtual machine once OPNsense is configured.
6. Package the virtual machine into a Vagrant box:

   ```sh
   vagrant package --base <name-of-your-vm> --output opnsense.box
   ```

### 2. Upload the Vagrant Box to an Accessible Location

1. Upload the `opnsense.box` file to an accessible server or cloud storage.
2. Note the download URL of the `opnsense.box` file.

### 3. Clone the Repository and Configure the Vagrant Project

1. Clone this repository:

   ```sh
   git clone https://github.com/sebastianaf/opn-sense-vagrant.git
   cd opn-sense-vagrant
   ```

2. Create a `.env` file in the same directory by copying the contents of `.env.example`:

   ```env
   ADAPTER_NAME=YourAdapterNameHere  # Change this to the exact name of your adapter in Windows or Linux
   BOX_URL=https://path/to/your/opnsense.box
   ```

### 4. Start the Virtual Machine

1. Start the virtual machine with the following command:

   ```sh
   vagrant up
   ```

### 5. Access the Web Interface

1. Track the IP assigned to the LAN interface.
2. Open a web browser and access the OPNsense web interface using the tracked IP address:

   ```http
   http://<IP_LAN>
   ```

## Additional Notes

- **WAN Interface**: Configured to receive the incoming connection.
- **LAN Interface**: Configured to provide the outgoing connection.
- Both interfaces are configured in DHCP mode by default.

By following these steps, you can create and configure a virtual machine with OPNsense using Vagrant and access its web interface for administration.
