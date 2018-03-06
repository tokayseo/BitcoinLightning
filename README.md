# Bitcoin Lightning
Building Your Bitcoin Lightning Master Node

## Here is a Full Video Walk-through
Coming Soon

## Preperation

1. Get a VPS from a provider like DigitalOcean, Vultr, Linode, etc. 
   - Recommended VPS size at least 1gb RAM 
   - **It must be Ubuntu 16.04 (Xenial)**
2. Make sure you have a transaction of exactly 3000 BLTG in your desktop cold wallet.

## Cold Wallet Setup Part 1

1. Open your wallet on your desktop.

   Click Settings -> Options -> Display
   
   Check "Display coin control features (experts only!)"
   
  
   
   Press Ok (you will need to restart the wallet)
   
   ![Alt text](https://i.imgur.com/cJUOQF8.png "Wallet Settings")

   
   
   
2. Go to the "Help" -> "Debug console" -> "Console"
3. Run the following command: `masternode genkey`
4. You should see a long key that looks like:
```
3HaYBVUCYjEMeeH1Y4sBGLALQZE1Yc1K64xiqgX37tGBDQL8Xg
```
5. This is your `private key`, keep it safe, do not share with anyone.




## VPS Setup

1. Log into your VPS
   - Windows users [follow this guide](https://www.digitalocean.com/community/tutorials/how-to-log-into-your-droplet-with-putty-for-windows-users) to log into your VPS.
2. Copy/paste these commands into the VPS and hit enter: (One Box At A Time)
```
apt-get -y update
```
```
apt-get -y upgrade
```
```
cd /var
touch swap.img
chmod 600 swap.img
dd if=/dev/zero of=/var/swap.img bs=1024k count=2000
mkswap /var/swap.img
swapon /var/swap.img
echo "/var/swap.img none swap sw 0 0" >> /etc/fstab
```
```
cd
```
```
apt-get install -y build-essential libtool autotools-dev pkg-config libssl-dev libboost-all-dev
autoconf automake 
```
apt-get -y install software-properties-common
```
```
apt-add-repository -y ppa:bitcoin/bitcoin
```
```
apt-get -y update
```
```
apt-get -y upgrade
```
```
apt-get -y install \
    wget \
    git \
    unzip \
    libevent-dev \
    libboost-dev \
    libboost-chrono-dev \
    libboost-filesystem-dev \
    libboost-program-options-dev \
    libboost-system-dev \
    libboost-test-dev \
    libboost-thread-dev \
    libminiupnpc-dev \
    build-essential \
    libtool \
    autotools-dev \
    automake \
    pkg-config \
    libssl-dev \
    libevent-dev \
    bsdmainutils \
    libzmq3-dev \
    nano
```
```
apt-get -y update
```
```
apt-get -y upgrade
```
```
apt-get -y install libdb4.8-dev
```
```
apt-get -y install libdb4.8++-dev
```
```
apt-get install libzmq3-dev libminiupnpc-dev libssl-dev libevent-dev
```
```
apt-get install git 
```
```
git clone https://github.com/bitcoin-core/secp256k1
```
```
cd ~/secp256k1
```
```
./autogen.sh
```
```
./configure
```
```
make
```
```
./tests
```
```
make install
```
```
apt-get install libgmp-dev
```
```
apt-get install openssl 
```
```
apt-get install software-properties-common && add-apt-repository ppa:bitcoin/bitcoin
```
```
apt-get -y update
```
```
apt-get install libdb4.8-dev libdb4.8++-dev
```
```
```
cd
```
```
git clone https://github.com/Bitcoinlightning/Bitcoin-Lightning.git
```
```
cd ~/Bitcoin-Lightning/src
```
```
make -f makefile.unix     (THIS STEP CAN TAKE A WHILE, GRAB A BEER.)
```
```
strip Bitcoin_Lightningd 
```
```
cp Bitcoin_Lightningd /usr/bin/
```
```
Bitcoin_Lightningd
```
```
cd
```
```
nano ~/.Bitcoin_Lightning/Bitcoin_Lightning.conf
```
```
Replace:
externalip=VPS_IP_ADDRESS
masternodeprivkey=WALLET_GENKEY
With your info!
```
```
rpcuser=putanythingyoulike
rpcpassword=putanythinkyoulike
rpcport=17126
server=1
listen=1
daemon=1
masternodeaddr=your-server-ip:17127 Example 104.238.164.50:17127
masternode=1
masternodeprivkey=your masternode private key
(ex: 69SteYY8bLzWL9jZYLKwU3wWpj4xt5oFzsbSMeoZbutJapKp6FW) 

```
CTRL X to save it. Y for yes, then ENTER.
```
Bitcoin_Lightningd
```

3.Use `watch Bitcoin_Lightningd getinfo` to check and wait til it's synced 



## Cold Wallet Setup Part 2 
1. Let's go back to windows Bitcoin Lightning wallet. 
2. Go to Receive > New Address MN01 > Press OK
3. Let's copy address
4. Send Exactly 3000BLT. NOTE: Go to your transactions wait for at least 15 confirmations
5. Getting TxHash and TxIndex
6. Now Go to Help > Debug Window > Console > Type masternode outputs You should see
something like this but different values 
7. Copy this information and save it and exit out from console
8. Now go back to your windows wallet go to Masternodes > Create 
9. Fill out like this. 
https://i.imgur.com/A6rhoHE.png
10. Press OK
11. Now Press Update 
12. After that Press Start All 
13. Your masternode is completed 

Cheers !!
