cryptonote-fury-pool
======================

#### 1. Requirements for Ubuntu 16.04
* Install dependencies:
```
sudo apt-get install libgtest-dev && cd /usr/src/gtest && sudo cmake . && sudo make && sudo mv libg* /usr/lib/
sudo apt update && sudo apt install build-essential cmake pkg-config libboost-all-dev libssl-dev libzmq3-dev libunbound-dev libsodium-dev libunwind8-dev liblzma-dev libreadline6-dev libldns-dev libexpat1-dev doxygen graphviz libpcsclite-dev libpgm-dev
sudo apt-get install libcurl3-dev
```

* Install node: 
 ```
  curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash
  sudo apt-get install -y nodejs
```

* Install redis (follow all steps to install Redis as daemon):
```
https://redis.io/topics/quickstart
 ```

* Clone this repository
```
git clone git@github.com:poNgz0r/cryptonote-fury-pool.git fury-pool
cd fury-pool
npm update
```

#### 2) Adjust config.json
Replace **YOUR_POOL_URL** with the url of your pool (example: fury.piratepools.nl)

Replace **YOUR_POOL_WALLET** with a fury wallet you want to use for your pool

Replace **YOUR_ADMIN_PASSWORD** with a password your can remember. You will be using that to reach the back-end of your pool (example fury.piratepools.nl/admin.html)


#### 3) Host the front-end
Simply host the contents of the `website_example` directory on file server capable of serving simple static files.

Edit the variables in the `website_example/config.js`:

Variable explanations:

```javascript
var api = "https://**YOUR_POOL_URL**:2888";

var email = null;
var telegram = null;
var discord = "https://discord.gg/ZfrPMby";

var marketCurrencies = ["{symbol}-BTC", "{symbol}-USD", "{symbol}-EUR", "{symbol}-CAD"];

var blockchainExplorer = "https://fury-block-explorer.piratepools.nl/block/{id}";
var transactionExplorer = "https://fury-block-explorer.piratepools.nl/tx/{id}";

var themeCss = "themes/stellite.css";
var defaultLang = 'en';
```

#### 4) Start pool
In the fury-pool folder type:
```
node init.js
```
