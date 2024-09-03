# GNS3 Setup Guide for Windows Using VirtualBox

This guide will walk you through the steps to set up GNS3 on a Windows machine using VirtualBox, including adding a Kali Linux VM to your VirtualBox environment.

## Prerequisites

Before you begin, make sure you have the following software installed:

- [GNS3](https://gns3.com/software/download)
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- [Kali Linux VM Image](https://www.kali.org/get-kali/#kali-virtual-machines)

## Step 1: Install GNS3

1. Download the latest version of GNS3 from the [official website](https://gns3.com/software/download).
2. Run the installer and follow the on-screen instructions.
3. Choose the "GNS3 all-in-one" option to install the GNS3 GUI and GNS3 VM.
4. Once the installation is complete, launch GNS3.

## Step 2: Install and Set Up VirtualBox

1. Download the latest version of VirtualBox from the [official website](https://www.virtualbox.org/wiki/Downloads).
2. Run the VirtualBox installer and follow the installation prompts.
3. After the installation is complete, launch VirtualBox.

## Step 3: Configure GNS3 to Use VirtualBox

1. Open GNS3 and go to `Edit` > `Preferences`.
2. In the Preferences window, navigate to `Virtualization` > `VirtualBox`.
3. Check the box labeled "Enable VirtualBox support."
4. Click `Apply` and then `OK` to save the settings.

## Step 4: Import the GNS3 VM into VirtualBox

1. In VirtualBox, go to `File` > `Import Appliance`.
2. Browse to the location where the GNS3 VM .ova file was downloaded during the GNS3 installation.
3. Select the .ova file and click `Next`.
4. Follow the prompts to import the GNS3 VM into VirtualBox.
5. Once the import is complete, you should see the GNS3 VM listed in VirtualBox.

## Step 5: Configure the GNS3 VM

1. Go back to GNS3 and open `Edit` > `Preferences` > `GNS3 VM`.
2. Select "Enable the GNS3 VM" and choose VirtualBox as the VM engine.
3. Ensure that the "VM Name" matches the name of the GNS3 VM in VirtualBox.
4. Click `Apply` and then `OK`.

## Step 6: Add Kali Linux VM to VirtualBox

1. Download the Kali Linux VirtualBox image from the [official Kali Linux website](https://www.kali.org/get-kali/#kali-virtual-machines).
2. In VirtualBox, go to `File` > `Import Appliance`.
3. Select the Kali Linux .ova file you downloaded and follow the prompts to import it.
4. After the import is complete, you should see the Kali Linux VM in the VirtualBox VM list.

## Step 7: Configure Network Settings for Kali Linux VM

1. In VirtualBox, right-click on the Kali Linux VM and select `Settings`.
2. Go to the `Network` tab and ensure that Adapter 1 is set to "Bridged Adapter" or "Host-Only Adapter" (depending on your network requirements).
3. Click `OK` to save the changes.

## Step 8: Start and Test the Setup

1. Start the GNS3 VM from VirtualBox.
2. Open GNS3 and drag the GNS3 VM and Kali Linux VM into the workspace.
3. Connect the devices using virtual network interfaces as needed.
4. Start the simulation and test connectivity between the GNS3 VM and Kali Linux VM.

## Conclusion

Your GNS3 environment is now set up and configured on Windows using VirtualBox, and you have successfully added a Kali Linux VM. You can now start building and testing your network scenarios!
