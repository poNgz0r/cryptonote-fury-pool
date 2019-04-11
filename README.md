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
- Replace **YOUR_POOL_URL** with the url of your pool (example: **fury.piratepools.nl**).
- Replace **YOUR_POOL_WALLET** with a fury wallet you want to use for your pool
- Replace **YOUR_ADMIN_PASSWORD** with a password your can remember. You will be using that to reach the back-end of your pool (example **fury.piratepools.nl/admin.html**)

```javascript
{
    "poolHost": "YOUR_POOL_URL",
    "coin": "FuryCoin",
    "symbol": "FURY",
    "coinUnits": 100000000,
    "coinDecimalPlaces": 4,
    "coinDifficultyTarget": 60,
    "daemonType": "default",
    "cnAlgorithm": "cryptonight_superfast",
    "cnVariant": 0,
    "cnBlobType": 0,
    "logging": {
        "files": {
            "level": "info",
            "directory": "logs",
            "flushInterval": 5
        },
        "console": {
            "level": "info",
            "colors": true
        }
    },

    "poolServer": {
        "enabled": true,
        "clusterForks": "auto",
        "poolAddress": "YOUR_POOL_WALLET",
        "blockRefreshInterval": 350,
        "minerTimeout": 900,
        "sslCert": "/etc/letsencrypt/live/YOUR_POOL_URL/cert.pem",
        "sslKey": "/etc/letsencrypt/live/YOUR_POOL_URL/privkey.pem",
        "sslCA": "/etc/letsencrypt/live/YOUR_POOL_URL/chain.pem",
        "ports": [  
			{
                "port": 6111,
                "difficulty": 4000,
                "desc": "Low end hardware",
                "hashrate": "< 1000H/s"
            },		
            {
                "port": 6112,
                "difficulty": 40000,
                "desc": "Medium end hardware",
                "hashrate": "~ 1000H/s"
            },
            {
                "port": 6113,
                "difficulty": 80000,
                "desc": "High end hardware",
                "hashrate": "~ 2000H/s"
            },
            {
                "port": 6114,
                "difficulty": 200000,
                "desc": "Low end rigs",
                "hashrate": "~ 5000H/s"
            },
            {
                "port": 6115,
                "difficulty": 400000,
                "desc": "High end rigs",
                "hashrate": "~ 10000H/s"
            }
        ],
        "varDiff": {
            "minDiff": 4000,
            "maxDiff": 1000000,
            "targetTime": 60,
            "retargetTime": 30,
            "variancePercent": 30,
            "maxJump": 100
        },
        "paymentId": {
            "enabled": true,
            "addressSeparator": "."
        },
        "fixedDiff": {
            "enabled": true,
            "addressSeparator": "+"
        },
        "shareTrust": {
            "enabled": false,
            "min": 10,
            "stepDown": 3,
            "threshold": 10,
            "penalty": 30
        },
        "banning": {
            "enabled": true,
            "time": 30,
            "invalidPercent": 50,
            "checkThreshold": 30
        },
        "slushMining": {
            "enabled": false,
            "weight": 300,
            "blockTime": 60,
            "lastBlockCheckRate": 1
         }
    },

    "payments": {
        "enabled": true,
        "interval": 900,
        "maxAddresses": 10,
        "mixin": 3,
        "priority": 0,
        "transferFee": 1000000,
        "dynamicTransferFee": true,
        "minerPayFee" : true,
        "minPayment": 2500000000,
        "maxPayment": 100000000000,
        "maxTransactionAmount": 750000000000,
        "denomination": 100000000
    },

    "blockUnlocker": {
        "enabled": true,
        "interval": 30,
        "depth": 10,
        "poolFee": 0.2,
        "devDonation": 0.0
    },

    "api": {
        "enabled": true,
        "hashrateWindow": 600,
        "updateInterval": 5,
        "port": 8128,
        "bindIp":"0.0.0.0",
        "blocks": 30,
        "payments": 30,
        "password": "YOUR_ADMIN_PASSWORD",
        "ssl": true,
        "sslPort": 2888,
        "sslCert": "/etc/letsencrypt/live/YOUR_POOL_URL/cert.pem",
        "sslKey": "/etc/letsencrypt/live/YOUR_POOL_URL/privkey.pem",
        "sslCA": "/etc/letsencrypt/live/YOUR_POOL_URL/chain.pem",
        "trustProxyIP": false
    },

    "daemon": {
        "host": "127.0.0.1",
        "port": 18081
    },

    "wallet": {
        "host": "127.0.0.1",
        "port": 18400
    },

    "redis": {
        "host": "127.0.0.1",
        "port": 6379,
        "auth": null,
        "db": 0,
        "cleanupInterval": 15
    },
 
	"email": {
        "enabled": false
    },
	
    "telegram":{
        "enabled":false
    },
	
    "monitoring": {
        "daemon": {
            "checkInterval": 900,
            "rpcMethod": "getblockcount"
        },
        "wallet": {
            "checkInterval": 900,
            "rpcMethod": "getbalance"
        }
    },

    "prices": {
        "source": "tradeogre",
        "currency": "USD"
    },
    
	"charts": {
        "pool": {
            "hashrate": {
                "enabled": true,
                "updateInterval": 60,
                "stepInterval": 1800,
                "maximumPeriod": 86400
            },
            "miners": {
                "enabled": true,
                "updateInterval": 60,
                "stepInterval": 1800,
                "maximumPeriod": 86400
            },
            "workers": {
                "enabled": true,
                "updateInterval": 60,
                "stepInterval": 1800,
                "maximumPeriod": 86400
            },
            "difficulty": {
                "enabled": true,
                "updateInterval": 1800,
                "stepInterval": 10800,
                "maximumPeriod": 604800
            },
            "price": {
                "enabled": true,
                "updateInterval": 1800,
                "stepInterval": 10800,
                "maximumPeriod": 604800
            },
            "profit": {
                "enabled": true,
                "updateInterval": 1800,
                "stepInterval": 10800,
                "maximumPeriod": 604800
            }
        },
        "user": {
            "hashrate": {
                "enabled": true,
                "updateInterval": 180,
                "stepInterval": 1800,
                "maximumPeriod": 86400
            },
            "worker_hashrate": {
                "enabled": true,
                "updateInterval": 60,
                "stepInterval": 60,
                "maximumPeriod": 86400
            },
            "payments": {
                "enabled": true
            }
        },
        "blocks": {
            "enabled": true,
            "days": 30
        }
    }    
}

```

#### 3) Host the front-end
Simply host the contents of the `website_example` directory on file server capable of serving simple static files. Edit the variables in the `website_example/config.js`.

Replace **YOUR_POOL_URL** with the url of your pool (example: **fury.piratepools.nl**)

```javascript
var api = "https://YOUR_POOL_URL:2888";

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
