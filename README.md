# dbix-proxy-solo

Dubaicoin-DBIX mining proxy with web-interface 127.0.0.1:7070.

**Proxy feature list:**

* Rigs availability monitoring
* Keep track of accepts, rejects, blocks stats
* Easy detection of sick rigs
* Daemon failover list

![Demo](https://raw.githubusercontent.com/sanja18/dbix-proxy-solo/master/proxy.png)

### Building on Linux

Dependencies:

  * go >= 1.4
  * gdbix

Export GOPATH:

    export GOPATH=$HOME/go

Install required packages:

    go get github.com/ethereum/ethash
    go get github.com/ethereum/go-ethereum/common
    go get github.com/goji/httpauth
    go get github.com/gorilla/mux
    go get github.com/yvasiyarov/gorelic

Compile:

    go build -o dbix-proxy main.go

### Building on Windows

Follow [this wiki paragraph](https://github.com/ethereum/go-ethereum/wiki/Installation-instructions-for-Windows#building-from-source) in order to prepare your environment.
Install required packages (look at Linux install guide above). Then compile:

    go build -o dbix-proxy.exe main.go

### Building on Mac OS X

If you didn't install [Brew](http://brew.sh/), do it. Then install Golang:

    brew install go

And follow Linux installation instructions because they are the same for OS X.

### Configuration

Configuration is self-describing, just copy *config.example.json* to *config.json* and specify endpoint URL and upstream URLs.

#### Example upstream section

```javascript
"upstream": [
  {
    "pool": true,
    "name": "Dubaicoin.org",
    "url": "http://pool1.arabianchain.org:7777/miner/0xb85150eb365e7df0941f0cf08235f987ba91506a/proxy",
    "timeout": "10s"
  },
  {
    "name": "backup-gdbix",
    "url": "http://127.0.0.1:7565",
    "timeout": "10s"
  }
],
```

In this example we specified [Dubaicoin.org](https://pool.dubaicoin.org) mining pool as main mining target and a local geth node as backup for solo.

With <code>"submitHashrate": true|false</code> proxy will forward <code>eth_submitHashrate</code> requests to upstream.

#### Running

    ./dbix-proxy config.json

#### Mining

    ethminer -F http://x.x.x.x:7555/miner/5/gpu-rig -G
    ethminer -F http://x.x.x.x:7555/miner/0.1/cpu-rig -C


### TODO

**Currently it's solo-only solution.**

* Report block numbers
* Report luck per rig
* Maybe add more stats
* Maybe add charts


### License

The MIT License (MIT).
