# Implement a Private Blockchain

Start the application server: node app.js


## Operational Detail

#### Set Up Bitcoin Core Development Environment
1. Create a bitcoin.conf file in the Bitcoin Core application directory
2. Write `prune=550` to reduce amount of storage used, avoiding storing a full copy of the blockchain (550 is the minimum prune allowed by Bitcoin Core)
 - Reduce Bitcoin Storage Article: https://bitcoin.org/en/full-node#reduce-storage
3. Download and Install your Bitcoin wallet
 - Latest Bitcoin Core: https://bitcoin.org/en/download
 - Where data is stored by default: https://en.bitcoin.it/wiki/Data_directory
 - Bitcoin Core Data Directory: https://en.bitcoin.it/wiki/Data_directory 
4. In bitcoin.conf, put `testnet=1` to switch to testnet, or `regnet=1` to switch to regnet. For this we want the regnet
5. Open wallet in Testnet mode, create receiving wallet
6. Get Testnet coins from the Bitcoin TestNet Sandbox Faucet http://bitcoinfaucet.uo1.net/
7. 


#### Bitcoin SDLC
Mainnet: The live network, where coins have real value, and peers exist
 - blockchain approx 200GB+ in size
 - block creation time is 10 min
 - public key prefix: 1
Testnet: A live netowrk, but coins do not have real value, but peers exist (production mirror environment)
 - blockchain approx 14GB in size
 - block creation time is 10 min
 - public key prefix: m or n
 - block difficulty: half of mainnet
 - Bitcoin Testnet Wiki: https://en.bitcoinwiki.org/wiki/Testnet
Regnet: An application regression testing network, where coins have no value, and no peers exist. Blocks can be made at will so dApps can be tested quickly
 - Developer Test Applications: https://bitcoin.org/en/developer-examples#testing-applications


#### Useful Links
Testnet Wiki: https://en.bitcoin.it/wiki/Testnet
How to activate Bitcoin Core Testnet: https://www.youtube.com/watch?v=CxDSrYuzmyQ
How to use Bitcoin Core Testnet: https://www.youtube.com/watch?v=MX_DHGJxoOc
Testnet Bitcoin: https://www.youtube.com/watch?v=WgNhwExy_cM
Testnet Faucets: https://www.youtube.com/watch?v=gIZCQUatkes
Bitcoin.conf file generation from UI: https://jlopp.github.io/bitcoin-core-config-generator/
Bitcoin.conf Overview: https://www.youtube.com/watch?v=W54aRszkEOI&t=32s
BlockCypher - Bitcoin Testnet Explorer: https://live.blockcypher.com/btc-testnet/


STEP 1: GET BLOCK BY HEIGHT
curl --location --request GET 'http://localhost:8000/block/0'

STEP 2: REQUEST OWNERSHIP

curl --location --request POST 'http://localhost:8000/requestValidation' \
--header 'Content-Type: application/json' \
--data-raw '{
    "address" : "tb1qfwdwn9gk2qv0n29rxt63afdx4agxq40xdwye9n"
}'

STEP 3: SUBMIT STAR WITH SIGNED MESSAGE

curl --location --request POST 'http://localhost:8000/submitstar' \
--header 'Content-Type: application/json' \
--data-raw '{
    "address" : "tb1qfwdwn9gk2qv0n29rxt63afdx4agxq40xdwye9n",
    "signature" : "IAdbcvtdAzlNT3fkd01yvrLypFZgB9XVkwVs2HBhQqA/Kn5TLFq/zcwnElJ3TjSCZvb7lYP2b6GUyVEIKZHbP+s=",
    "message" : "tb1qfwdwn9gk2qv0n29rxt63afdx4agxq40xdwye9n:1617938746:starRegistry",
    "star" : {
        "dec" : "68 52 56.9",
        "ra" : "16h 29m 1.0s",
        "story" : "Testing submitStar 1"
    }
}'
