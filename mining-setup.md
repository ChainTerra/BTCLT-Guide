---
# Page settings
layout: default
keywords:
comments: false

# Hero section
title: Mining Setup
description: Learning about how to set up mining and how to connect to what is needed.

# Author box
author:
    title: About Author
    title_url: 'https://www.minds.com/gamer456148'
    external_url: true
    description: Andrew has built technologies for numerous startups. He currently does research in Computational Genomics, Distributed Systems, and Quantum Computing. He is a Copt, and likes to play a variety of sports or build things in his free time.
    
# Micro navigation
micro_nav: true

# Page navigation
page_nav:
    prev:
        content: Previous page
        url: 'cloutpool/'
    next:
        content: Next page
        url: 'information/'
        
---

Right now this is experimental, but here is the guide as it currently stands *(as of time last updated)*:

**For the core node:** \
`git clone https://github.com/bitclout/core` \
`git clone https://github.com/bitclout/backend` \
`cd backend` \
Either run: `docker build -t ubuntu-test:latest .` \
Or run `docker build -t backend ..` \
`cd ../` \
`cd core` \
`sudo nano run_remote_miner.sh` \
Edit `miner_public_key` value to your public key \
Run `go build` in the `core` directory \
Then also run: `docker build -t ubuntu-test:latest .` \
Theoretically, you are supposed to be able to run `./run_remote_miner.sh` to start mining. \
However, the [cmd](https://github.com/bitclout/core/cmd/) module needs to be live. Once it is, the above instructions likely should work.

**For running a mining pool:** \
`git clone https://github.com/ChainTerra/CloutPool.git` \
Make sure to run the [bitclout/core](https://github.com/bitclout/core) daemon (Dockerfile and node) first locally. \
Run `go build .` \
Copy `go-stratum-pool` and rename `config.clout.json` to `config.json` \
Change the `rewardRecipients` address in line 18 of the config to your address. \
Run `./go-stratup-pool` and it should detect the `config.json` file and node automatically. \
You can host this in a VPS and share mining rewards w/ your "workers".

**For running w/ Node.js** \
`git clone https://github.com/zone117x/node-stratum-pool.git` \
`git clone https://github.com/ChainTerra/NSP_Configs.git` \
Make sure to run the [bitclout/core](https://github.com/bitclout/core) daemon (Dockerfile and node) first locally. \
Move to `NSP_Configs` files to `node-stratum-pool` \
Replace the addresses in the `pool.js` file. \
Add the configs as modules + `pool.start();` \
Run `npm run`

**For Cuda:** See software [here](https://github.com/ChainTerra/CP_Cuda) \
**Windows**: `sgminer-x64 -k keccak -o stratum+tcp://localhost:3032 -u BITCLOUTADDRESS.WorkerName -p x` \
`ccminer -a keccak -o stratum+tcp://localhost:3032 -u BITCLOUTADDRESS.WorkerName -p x` \
**Unix**: `./sgminer -k keccak -o stratum+tcp://localhost:3032 -u BITCLOUTADDRESS.WorkerName -p x` \
`-dpool stratum+tcp://localhost:3032 -dwal BITCLOUTADDRESS.WorkerName -dpsw x -dcoin keccak -allpools 1` \
**Regarding Claymore:** `-dpool stratum+tcp://localhost:3032 -dwal BITCLOUTADDRESS.WorkerName -dpsw x -dcoin keccak -allpools 1` \
Obivously replace `BITCLOUTADDRESS` w/ your address \
**In regards to Hive OS:** See farm instructions [here](https://github.com/ChainTerra/CP_WR_Confs)
