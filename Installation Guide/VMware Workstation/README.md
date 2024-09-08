# GNS3 Setup Guide for Windows Using VMware

This guide will walk you through the steps to set up GNS3 on a Windows machine using VMware Workstation Player, including integrating the GNS3 VM and adding a Kali Linux VM to enhance your network simulations.

## Prerequisites

Before you begin, make sure you have the following software installed:

- [VMware Workstation Player](https://www.vmware.com/products/workstation-player.html)
- [GNS3 All-in-One](https://gns3.com/software/download)
- [GNS3 VM OVA File](https://gns3.com/software/download)
- [Kali Linux VM Image](https://www.kali.org/get-kali/#kali-virtual-machines)

---

## Step 1: Install VMware Workstation Player

1. **Download VMware Workstation Player** from the official [VMware website](https://www.vmware.com/products/workstation-player.html).
2. **Run the installer** and follow the installation wizard:
   - Accept the license agreement.
   - Choose your preferred installation path.
3. **Complete the installation** by clicking **Finish** once the process is done.

---

## Step 2: Install GNS3 All-in-One

1. **Download the GNS3 All-in-One installer** from the [GNS3 website](https://gns3.com/software/download).
2. **Run the installer** and follow the on-screen instructions.
3. When prompted, select **Yes** to install the **GNS3 VM** as part of the installation.
4. **Complete the installation** process by following the wizard steps.

---

## Step 3: Import GNS3 VM into VMware Workstation

1. **Open VMware Workstation Player** on your system.
2. **Import the GNS3 VM OVA file**:
   - Click **File > Open** and select the GNS3 VM OVA file you downloaded.
   - Follow the import wizard to add the VM to VMware.
3. **Power on the GNS3 VM**:
   - Right-click on the GNS3 VM in VMware and select **Power On**.

---

## Step 4: Configure GNS3 to Use VMware Workstation Player

1. **Launch GNS3** on your Windows machine.
2. Go to **Edit > Preferences**.
3. In the left-hand menu, click on **GNS3 VM**:
   - Check the box to **Enable the GNS3 VM**.
   - Select **VMware Workstation** as the VM type.
4. **Test the connection**:
   - Click **Apply** and **OK** to save the settings.
   - Start a simple topology in GNS3 to ensure the GNS3 VM is connected properly.

---

## Step 5: Add Devices and Configure Network Topology

1. **Add device images**:
   - Download required device images (e.g., Cisco IOS, IOU) and add them in **Edit > Preferences > Dynamips/IOU Devices**.
2. **Build your network topology**:
   - Drag and drop devices into the GNS3 workspace.
   - Connect devices by drawing links between them.
   - Start the devices and configure their network settings using the console.

---

## Step 6: Adding Kali Linux VM into VMware Workstation

1. **Download the Kali Linux VM** from the official [Kali website](https://www.kali.org/get-kali/#kali-virtual-machines).
2. Open **VMware Workstation Player** and click **File > Open**.
3. Select the Kali Linux OVA file and import it as a new virtual machine.
4. **Power on the Kali VM** after importing.
5. After the VM starts, you can proceed with assigning the necessary network adapters for the lab environment.

---

## Step 7: Connecting Kali Linux VM with GNS3

1. Open **VMware Workstation** and go to **Virtual Network Editor**.
2. Click **Add Network** and create a new network, e.g., **vmnet2** or **vmnet5**.
3. Set the network type to **Host-Only** and disable **DHCP** (since it won't be needed in a lab environment).
4. Assign an addressing space that fits your needs, ensuring that your VM and connected devices are on the same network. For example:
   - Subnet IP: `172.16.5.0`
   - Subnet mask: `255.255.255.0`
5. Click **Apply**, and a virtual adapter will be created.

### Verifying the New Adapter

6. Open the command line and type `ipconfig` to list all network interfaces.
7. The new adapter should appear with an IP of `172.16.5.1` and the assigned subnet mask.

#### Changing the IP Address (Optional):

If you want to use `.1` as the gateway in your lab.

8. Open **Network Connections**, double-click the new network adapter, and open **Properties**.
9. Select **TCP/IPv4 Protocol**, and manually change the IP address (e.g., `172.16.3.254`), leaving the subnet mask as `255.255.255.0`. 10. Click **OK** to save the changes.

---

## Step 8: Assign Kali Linux to Custom Network

1. Go back to **VMware Workstation** and select the Kali Linux VM.
2. Right-click and select **Settings**.
3. Under **Network Adapter**, choose **Custom** and select the new adapter you created (e.g., **vmnet2**).
4. Power on the Kali VM.

---

## Step 9: Configure Kali Linux IP Address

1. Open **Network Manager** on Kali and manually assign an IP address:
   - IP: `172.16.3.2`
   - Subnet mask: `255.255.255.0`
   - Leave the default gateway blank.
2. Save the configuration.

---

## Step 10: Verify Connectivity with GNS3

1. Create a new project in GNS3.
2. Add the Kali VM and a router to the workspace.
3. Configure the router interface to connect with the VM using the same network:
   - IP: `172.16.3.1`
   - Subnet mask: `255.255.255.0`
4. **Ping** between the router and the Kali VM to check connectivity.

---

### Additional Steps to Overcome Common Issues

Setting up Kali Linux in VMware for GNS3 isn’t always straightforward compared to VirtualBox. The errors in GNS3 can be frustrating to solve, but following these steps should save you time (which I spent searching through YouTube and forums):

1. Open **VMware Workstation** and navigate to **Virtual Network Editor**.
2. **Add a new network** (e.g., `vmnet2`, `vmnet5`).
3. Ensure **Host-Only** is selected for the network, and **disable DHCP**.
4. Choose a subnet IP (e.g., `172.16.5.0`) with a subnet mask of `255.255.255.0`.
5. After applying the settings, verify the new network interface by typing `ipconfig` in the command line.
6. Change the IP address manually if needed.
7. Follow the earlier steps to assign the network adapter to the Kali VM and configure the IP address in **Network Manager**.

For additional help, check this [YouTube video](https://youtu.be/IB41t0g_Tb8).
