# Pool Templates for Hive 2.0

This is a list of pools that are available in Hive for creating Flight Sheet.
If you found mistake or the configuration changed please make push request.
If you want your pool to be listed here then create yourpool.json and push it, we will review it and add.


## Variables
`%WAL%` - wallet address

`%COIN%` - wallet coin

`%URL%` - pool URL <address:port>

`%URL_HOST%` - pool address

`%URL_PORT%` - pool port

`%WORKER_NAME%` - worker name (from rig name)

`%EMAIL%` - e-mail for some pool (ex. nanopool)

## Miners
Available miners:
- claymore - Claymore's DUAL ETH GPU AMD&NVidia miner
- claymore-x - Claymore's Cryptonote AMD GPU miner
- claymore-z - Claymore's AMD GPU ZCash miner
- ewbf - ewbf for equihash and new for equihash algo variants miner
- ccminer - ccminer & forks (ccminer forks available: alexis, allium, bcd, dace-cryptonight, djm34, enemy, klaust, klaust-yescrypt, nanashi, nevermore, nevermore-x16s, phi-anxmod, rvn, suprminer, sp-mod, tpruvot, vertminer, xevan, zp)
- ethminer - ethminer (forks available - ethash, progpow, ubiqhash, zilminer)
- sgminer - sgminer forks (avermore, djm34, fancyix, gatelessgate, gm, gm-nicehash, kl, phi)
- dstm - legacy 0.3.4b and new zhash
- bminer - ethash/tensority/equihash variants/Grin PoW miner 
- lolminer - equihash variants OpenCL miner
- xmr-stak - XMR-Stak (AMD,NVidia,CPU cryptonight variants algo with forks arto, alloy, b2n, mox, marketcash)
- xmrig - XMRig (CPU cryptonight variants miner with forks xmrigcc, hycon)
- xmrig-amd - XMRig (AMD cryptonight variants miner with forks xmrigcc, hycon)
- xmrig-nvidia - XMRig (NVidia cryptonight variants miner  with forks fruityminer, hycon)
- cast-xmr - cryptonight variants (AMD)
- cryptodredge - multi algo CUDA miner (NVidia)
- teamredminer - lyra2z/lyra2v3/phi2/cryptonight-r/v7/v8/half/double/rwz/trtl OpenCL miner (AMD)
- phoenixminer - ethash miner (AMD/NVidia)
- t-rex - multi algo CUDA miner (NVidia)
- cpuminer-opt - cpuminer-opt (CPU miner)
- wildrig-multi - multi-algo OpenCL miner (AMD)
- finminer - ethash, randomhash miner (AMD/NVidia/CPU)
- nanominer - next generation of finminer (AMD/NVidia/CPU)
- rhminer - randomhash CPU miner
- gminer - equihash variants CUDA miner
- beamcl - open source BEAM OpenCL miner
- beamcuda - open source BEAM CUDA miner
- grinminer - Cuckaroo29 and Cuckatoo31 miner (AMD/NVidia)
- gringoldminer - Cuckaroo29 miner (AMD/NVidia)
- grinpro - improved version of grinminer (AMD/NVidia)
- nbminer - ETH, BTM, Cuckoo miner (NVidia)
- hspminerae - CUDA AE miner (NVidia)
- kbminer - AE/Cuckaroo29/Cuckatoo31 miner (AMD/NVidia)
- zjazz-cuda - CUDA bitcash/cuckoo/x22i miner (NVidia)
- custom - Custom miner package



## Pool template example
```javascript
[
    { // pool header section - not necessary
        "pool": {
            "name": "Hiveon",             // pool name
            "url": "https://hiveon.net",  // pool URL
            "fee": 0,                     // pool fee in persent
            "type": "PPS+"                // pool reward system
        }
    },
    {
        "coin": "ETH",  // coin name
        "servers": [    // pool addresses array
            {   // geo element
                "geo": "Europe", // geo location, maybe null if unknown or in some cases you can indicate port difficulty
                "urls": [
                    "eu1-eth.hiveon.net:4444",  // pool server URL  and port
                    "eu1-eth.hiveon.net:14444"  // another server instance
                ]
            }
        ],
        "miners": { // miner's settings section
            "claymore": { //miner's name
                "epools_tpl": "POOL: %URL%, WALLET: %WAL%.%WORKER_NAME%, PSW: x" //miner's settings
            },
            "ethminer": {
                "cuda": 1,
                "opencl": 1,
                "pass": "x",
                "port": "%URL_PORT%",
                "server": "stratum1+tcp://%URL_HOST%",
                "template": "%WAL%.%WORKER_NAME%"
            },
            "sgminer-gm": {
                "url": "stratum+tcp://%URL%",
                "algo": "ethash",
                "pass": "x",
                "template": "%WAL%.%WORKER_NAME%",
                "user_config": "\"worksize\": \"192\"\n\"gpu-threads\": \"1\"\n\"xintensity\": \"1024\""
            }
        }
    }
]
```

WARNING!
Comments in this example only for helping purposes!

## SSL ports
If your pool contains SSL ports on the same domains then you can add special section "ssl_urls" in geo element
```json
{
    "geo": "Low-End",
        "urls": [
            "pool.wowne.ro:3333"
        ],
        "ssl_urls": [
            "pool.wowne.ro:3334"
        ]
}
```


# Miners definitions for Hive 2.0

Each file in `miners` directory contains definitions for corresponding miner.

Below is a description of available options.
All fields are optional and may contain `null` value.

Field name | Type | Default | Description
--- | ---| --- | ---
full_name | `string` |  | Display name.
for_amd | `boolean` | `false` | Is suitable for AMD GPUs.
for_nvidia | `boolean` | `false` | Is suitable for Nvidia GPUs.
for_cpu | `boolean` | `false` | Is suitable for CPUs.
for_asic | `boolean` | `false` | Is suitable for ASICs.
default_algo | `string` |  | Algorithm to use if not reported by miner.<br>This is useful for single-algo miners.
default_fork | `string` |  | Fork to use if not configured in flight sheet.
algos | `string[]` or `object` |  | Supported algorithms list.<br>This can be either a simple array of strings or an object where keys are algos and values are display names.
dalgos | `string[]` or `object` |  | Supported algorithms list for dual mining.<br>This can be either a simple array of strings or an object where keys are algos and values are display names.
forks | `string[]` or `object` |  | Available forks list.<br>This can be either a simple array of strings or an object where keys are forks and values are display names.
algomap | `object` |  | Algorithms matching.<br>Keys are miner's algos and values are Hive's algos.


# Changelog for Hive 2.0

Located in file `changelog.md`.

Each section of the file represents one release and consist of heading, optionally followed by body.

##### Heading
Starts with at least one # sign and contain definition string in such format:

[ `LINUX` | `ASIC` | `Windows` ] [ `IMAGE RELEASE` ] `Version` `Date YYYY-MM-DD`

Examples:
```markdown
##### 0.6-30@190416 2019-04-16
##### 0.5-77 2018-10-01
##### LINUX 0.5-46 2018-04-20
##### LINUX IMAGE RELEASE 0.5-76 2018-09-24
##### ASIC 0.1-09 2018-09-26
##### Windows 0.1-01 2018-06-20
```

##### Body
Contains any text, mardown syntax is supported.

All lines until next heading are considered as body, empty leading and trailing lines are skipped.

Example:
```markdown
*   Description line
*   Description line
```
