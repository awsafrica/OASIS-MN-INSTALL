# OASIS Masternode Setup Guide

This guide assumes that you will setup so called COLD Masternode, where the server process is running on a remote Linux system (usually a rented VPS), and your funds are kept safely in your local offline wallet.

# 1 - Local wallet (collateral transfer)
First, you need to make a transaction collateral of exactly 285 OASIS coins. It should be kept untouched to receive masternode rewards.

* Start the OASIS wallet on your desktop and wait for it to complete the blockchain synchronisation.
* Open Menu → **Receiving addresses**... and create a new address with label EZIMN1 (or any one you like). Copy this address to the clipboard.
* Send exactly 285 OASIS coins in a single transaction to the account address you generated in the previous step. This may be sent from another wallet, or from funds already held in your current wallet.
* Wait for at least 15 transaction confirmations.
* Go to Help/Tools → **Debug console** and type the following command: masternode outputs
* This command should print a collateral transaction hash and index, usually 0 or 1.
* Keep this info at hand and proceed to the remote VPS setup.

# 2 - Remote VPS (masternode setup)
You have to find a Linux server which runs 24/7/365 and has a real IP address accessible from the outside. While it is possible to run it at home, the best way is to rent a VPS from a VPS provider. There are many providers, but we recommend https://www.ezimn.com/ which provides VPS starting from as low as $2.85 USD/month. To simplify the setup we provide an install script which runs on Ubuntu Linux version 16.04, 17.10 or 18.04 and automates most of the setup for you. You should have a root user access with a password, and log in to the VPS using any ssh client (on Windows it could be putty, kitty or something similar).

Copy and paste the following commands to the root command prompt on Linux:

`wget -N https://raw.githubusercontent.com/awsafrica/OASIS-MN-INSTALL/master/install.sh`

`bash install.sh`

The script will check if it runs on a supported Ubuntu version, update your system, install necessary libraries, install OASISCoin software, configure it as a cold masternode daemon and set the masternode private key. If you don't have one yet, just press Enter, and a new key will be generated for you.
PRIVATE KEYS - Only add your own if you are doing your own install, if you use a thirdparty provider then you should never share your private key.

Then you should have a script output similar to this one:

![mnsetupready](https://raw.githubusercontent.com/awsafrica/brixcoin6.0/master/contrib/masternode/brixmnsetupready.jpg)

The most important thing is the green line with the data you have to put into your local wallet. So let's go back to it to finalise the setup.

# 3 - Local wallet (masternode start)

First you should edit a masternode configuration file which is located in the coin data directory. On Windows it is in the "%APPDATA%/Oasis" directory. But you may simply use Tools → **Open Masternode Configuration** File to edit it.

* Copy the green line starting from ezimn1 from your Linux console and paste it into the end of **masternode.conf** file you just opened.
* Replace your-tx-hash and your-tx-index with the data from masternode outputs command you got earlier.
* Close editor and save the file.
* Close and restart your wallet.
* After restart ensure you have **at least 15 confirmations** of your collateral transaction. If you have less - please wait, or your masternode will not start.
* If you have the Masternodes tab - switch to it. If not, open wallet preferences and enable Masternodes tab from there.
* Click Start All button to start your masternode.

## Now your masternode should be up and running.

You may go to the Linux console and type there:
``oasis-cli masternode status``

If it shows:

``Masternode successfully started``

You should be fine and start receiving awards. The first award may be granted in an 1 to 24 hours depending on the number of masternodes in the network.
