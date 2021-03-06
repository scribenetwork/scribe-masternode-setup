# Scribe
Shell script to install a [Scribe Masternode](http://scribe.network/).  
This will require a VPS, I use [Vultr](https://www.vultr.com/?ref=7310394).  The $5/mo server size will suffice.  
This script will install **Scribe v0.3**.
***

## Installation:
Log into the server using ssh (Putty for windows or terminal for Mac users) and run the following commands:
- Ubuntu 16.04 (64bit):
   ```
   wget -q https://raw.githubusercontent.com/scribenetwork/scribe-masternode-setup/master/ubuntu/16.04/amd64/scribe_install.sh
   bash scribe_install.sh
   ```
***

## Desktop wallet setup

After the MN is up and running, you need to configure the desktop wallet accordingly. Here are the steps for Windows Wallet
1. Open the Scribe Core Wallet.
2. Go to RECEIVE and create a New Address: **MN1**
3. Send **1000** **Scribe** to **MN1**.
4. Wait for 15 confirmations.
5. Go to **Tools -> "Debug console - Console"**
6. Type the following command: **masternode outputs**
7. Go to  ** Tools -> "Open Masternode Configuration File"
8. Add the following entry:
```
Alias Address Privkey TxHash Output_index
```
* Alias: **MN1**
* Address: **VPS_IP:PORT**
* Privkey: **Masternode Private Key**
* TxHash: **First value from Step 6** 
* Output index:  **Second value from Step 6** It can be **0** or **1**
9. Click OK and exit the Wallet.
10. Open Scribe Core Wallet, go to **Masternode Tab**. If you tab is not shown, please enable it from: **Settings - Options - Wallet - Show Masternodes Tab**
11. Click **Update status** to see your node. If it is not shown, close the wallet and start it again.
10. Click **Start All** or **Start Alias**
11. If you are not able to see your **Masternode**, try to close and open your desktop wallet.
***

## Usage:
```
scribe-cli getinfo
scribe-cli masternode status
scribe-cli mnsync status
```
Also, if you want to check/start/stop **Scribe** , run one of the following commands as **root**:
```
systemctl status Scribe #To check the service is running.
systemctl start Scribe #To start Scribe service.
systemctl stop Scribe #To stop Scribe service.
systemctl is-enabled Scribe #To check whetether Scribe service is enabled on boot or not.
```
***

## Updating Scribe
The first line (rm scribe_update.sh) is not required the very first time you update the node and will return an error if you run it.  This is fine, continue with the update script.

- Ubuntu 16.04 (64bit):
   ```
   rm scribe_update.sh*
   wget -q https://raw.githubusercontent.com/scribenetwork/scribe-masternode-setup/master/ubuntu/16.04/amd64/scribe_update.sh
   bash scribe_update.sh
   ```
***

## Sentinel

**Sentinel** is installed in **/root/sentinel** and added to **crontab** file.  
Sentinel log file is **/root/.scribecore/sentinel.log**  
Test the config by running the following commands:
```
cd /sentinel
./venv/bin/py.test ./test
SENTINEL_DEBUG=1 ./venv/bin/python bin/sentinel.py
```
***

