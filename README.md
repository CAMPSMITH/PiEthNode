# PiEthNode

My journey to standing up an ethereum node using a Raspberry Pi.

---

## Based on
I used the following guides:
* https://ethereum.org/en/developers/tutorials/run-node-raspberry-pi/
* https://ethereum-on-arm-documentation.readthedocs.io/en/latest/


## Equipment I Used

The following list details the equipment I used:
* Raspberry Pi 4 - 8 Gig RAM
* USB MicroSD Card Reader
* 128 Gig Micro SD Card
* Western Digital 2 TB SSD - WD Green SN350 NVMe 
* Sabrent USB Type C tool free enclosure for M.2 PCIe NVMe SSD
* XAOSUN USB C to USB 3 adapter
* **...** - ...

---

## Day 1
### Get Raspberry Pi 4 Image

* https://ethereumonarm-my.sharepoint.com/:u:/p/dlosada/ES56R_SuvaVFkiMO1Tgnf6kB7lEbBfla5c2c18E3WQRJzA?download=1
Check image integrity
```
shasum -a 256 ethonarm_kiln_22.03.01.img.zip
485cf36128ca60a41b5de82b5fee3ee46b7c479d0fc5dfa5b9341764414c4c57  ethonarm_kiln_22.03.01.img.zip
485cf36128ca60a41b5de82b5fee3ee46b7c479d0fc5dfa5b9341764414c4c57

```

### Image installation process
1. copy image unto micro SD card
2. insert micro SD card into Pi
3. connect network, monitor and keyboard to Pi
4. Turn Pi on.  System automatically installs and initializes.  Takes about 15 minutes to come up.
5. Log into Pi using initial credentials (ethereum:ethereum).  System should force you to reset password.
6. get node ip address
   ```
   ifconfig
   ```
   note yor node's IP address. It most likely is on the `eth0` interface.
6. Check ssh is set up 
    ```
    sudo systemctl status ssh
    ```
    confirm that it is active (running) and listening on port 22.  The rest can be done via SSH.
6. Use ssh-copy-id to set up ssh key based login
    ```
    ssh-copy-id ethereum@<ip of ethereum node>
    ```
    once this is done, you can easily log into your ehtereum node with:
    ```
    ssh ethereum@<ip of ethereum node>
    ```
7. start eth node services
    ```
    sudo systemctl start geth-lh
    sudo systemctl start lh-geth-beacon
    ```  
8. Check logs to ensure the services started
    ```
    # logs for Geth
    sudo journalctl -u geth-lh -f
    #logs for lighthouse
    sudo journalctl -u lh-geth-beacon -f
    ```
This set up is configured to connect your pi to the Kiln testnet.  At this end of the process your pi should be synching with the kiln testnet.  In my case this is expected to take over two days:

from the lh-geth-beacon logs:
```
INFO Syncing                                 est_time: 2 days 5 hrs, speed: 6.69 slots/sec, distance: 1294329 slots
```


---

## Usage

TBD ...

---

## Contributors

*  **Martin Smith** <span>&nbsp;&nbsp;</span> |
<span>&nbsp;&nbsp;</span> *email:* msmith92663@gmail.com <span>&nbsp;&nbsp;</span>|
<span>&nbsp;&nbsp;</span> [<img src="images/LI-In-Bug.png" alt="in" width="20"/>](https://www.linkedin.com/in/smithmartinp/)


---

## License

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)