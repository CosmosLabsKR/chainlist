

# Mintscan Chain Information
Chain metadata used by Mintscan Explorer, managed by [Cosmos](https://github.com/cosmos)

- [Validator's moniker image](https://github.com/CosmosLabsKR/chainlist/tree/main#how-to-display-validator-moniker-keybase-identity)
- [Add Asset's Info](https://github.com/CosmosLabsKR/chainlist/tree/main#how-to-add-your-asset-info)
- [Add Cw20 Info](https://github.com/CosmosLabsKR/chainlist/tree/main#how-to-add-your-cw20-token-info)
- [Add Erc20 Info](https://github.com/CosmosLabsKR/chainlist/tree/main#how-to-add-your-erc20-token-info)
- [Add IBC Eureka Info](https://github.com/CosmosLabsKR/chainlist/tree/main#how-to-add-your-ibc-eureka-asset-info)
- [Add gRPC/EVM Endpoint](https://github.com/CosmosLabsKR/chainlist/tree/main#how-to-add-endpoint)
- [dApp link and description on Wallet](https://github.com/CosmosLabsKR/chainlist/tree/main/wallet/eco_list.json)


## Productions using with

- [Mintscan Explorer](https://mintscan.io)
- [Extension Wallet](https://bit.ly/3VhVJIF)
- [Android Wallet](https://bit.ly/2BWex9D)
- [iOS Wallet](https://apple.co/2IAM3Xm)




## Chain Image Set
<img src="https://raw.githubusercontent.com/CosmosLabsKR/chainlist/main/mintscan/resource/guide_chains.png" width="368" height="266"> <img src="https://raw.githubusercontent.com/CosmosLabsKR/chainlist/main/mintscan/resource/guide_tokens.png" width="249" height="266">


- Chains and Assets image with 3D
- Available in all sizes and formats. 



<details open>
  <summary><h2 style='display: inline; font-size: 24px'>How to display validator moniker (Keybase Identity)</h2></summary>

 - From March 2025, Display moniker information based on the on-chain validator description (Keybase Identity). 
 - The existing moniker folder will be deleted soon.

</details>

---

<details>
  <summary><h2 style='display: inline; font-size: 24px'>How to add your asset info</h2></summary>

‼️ Please be noted that assets of Testnets and unverified networks may not be merged to master.
1. Fork this repo to your own github account
2. Clone fork and create new branch

   ```shell
   git clone git@github.com:YOUR_ACCOUNT/chainlist.git
   cd chainlist
   git branch <branch_name>
   git checkout <branch_name>
   ```

3. Add the info of your asset in the chain `assets_2.json` file that your asset needs to be displayed
    >If there is no chain in the list, create a folder for the chain  
    Then add `assets_2.json` file to the folder, add asset info to that file  
    Changes will be updated within 24 hours after merged to master


   - ***Common info to fill***
     - `type`
       - `native` refers that the asset is a native asset issued on a chain.
       - `ibc` refers that the asset was ibc transferred.
       - `bridge` refers that the asset is a bridge asset.
     - `denom`
       - Asset's denom
     - `name`
       - Asset's name
     - `symbol`
       - The displayed name of the asset in the list.
     - `description`
       - A brief summary of the asset
     - `decimals`
       - Asset's decimals.
     - `image` (optional)
       - Image route of the asset.
       - Add image in `${targetchain}/asset` folder.
         - Make sure to upload a `png` file.
     - `color` (optional)
     - `coinGeckoId`
       - Asset gecko site's API ID 
         - ex. https://www.coingecko.com/en/coins/cosmos-hub 
            - API ID: *cosmos*
       - Empty string if none

    - ***If the type is <ins>ibc</ins>, provide the info below:***
      - `ibc_info`
        - `path`
          - If the asset was transferred via ibc, bridge or other path, provide full details of where it was transferred from.
        - `client`
          - `channel`
          - `port`
            - Add the asset's channel and port
        - `counterparty`
          - `channel`
          - `port`
            - Add counter party's channel and port
          - `chain`
          - `denom`
            - Assets's denom before ibc transfer
     - ***If the type is <ins>bridge</ins>, provide the info below:***
       - `bridge_info`
         - `path` (optional)
           - If the asset was transferred via ibc, bridge or other path, provide full details of where it was transferred from.
         - `counterparty`
           - `chain`
           - `contract` (optional)
             - If the asset was transferred via contract, provide the contract address.
         - `enable` (optional)
           - `true` if ibc transmission is possible



   ### Asset info json example
   `chain/${chain}/assets_2.json`

    - Native Asset

      ```json
      // example OSMOSIS
      [
        {
            "type": "native",
            "denom": "uosmo",
            "name": "Osmosis",
            "symbol": "OSMO",
            "description": "The native token of Osmosis",
            "decimals": 6,
            "image": "https://raw.githubusercontent.com/CosmosLabsKR/chainlist/master/chain/osmosis/asset/osmo.png",
            "color": "#760dbb",
            "coinGeckoId": "osmosis"
        },
        {
            "type": "native",
            "denom": "uion",
            "name": "Ion DAO",
            "symbol": "ION",
            "description": "ION is the second native token of Osmosis.",
            "decimals": 6,
            "image": "https://raw.githubusercontent.com/cosmos/chain-registry/master/osmosis/images/ion.svg",
            "color": "#4453c7",
            "coinGeckoId": "ion"
        }
      ]
      ```

    - IBC Asset

      ```json
      [
        // example COSMOS
        {
            "type": "ibc",
            "denom": "ibc/14F9BC3E44B8A9C1BE1FB08980FAB87034C9905EF17CF2F5008FC085218811CC",
            "name" : "Osmosis",
            "symbol": "OSMO",
            "description": "Osmosis Staking Coin",
            "decimals": 6,
            "image": "https://raw.githubusercontent.com/CosmosLabsKR/chainlist/master/chain/osmosis/asset/osmo.png",
            "coinGeckoId": "osmosis",
            "ibc_info" : {
                "path": "osmosis>cosmos",
                "client" : {
                    "channel": "channel-141",
                    "port": "transfer"
                },
                "counterparty": {
                    "channel": "channel-0",
                    "port": "transfer",
                    "chain": "osmosis",
                    "denom": "uosmo"
                }
            }
        }
        // example IRIS
        {
            "type": "ibc",
            "denom": "ibc/E244B968EE0D1EC047E7516F6ABECE7B68E9FD93B4BD8D08D13642247416BB17",
            "name" : "Wrapped Ethereum (Ethereum to Gravity-Bridge)",
            "symbol": "WETH.grv",
            "description": "Gravity Bridge WETH",
            "decimals": 18,
            "image": "https://raw.githubusercontent.com/CosmosLabsKR/chainlist/master/chain/ethereum/asset/weth.png",
            "coinGeckoId": "weth",
            "ibc_info" : {
                "path": "ethereum>gravity-bridge>iris",
                "client" : {
                    "channel": "channel-29",
                    "port": "transfer"
                },
                "counterparty": {
                    "channel": "channel-47",
                    "port": "transfer",
                    "chain": "gravity-bridge",
                    "denom": "gravity0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2"
                }
            }
        }
      ]
      ```

    - Bridge Asset

      ```json
      [
        // example GRAVITY-BRIDGE
        {
            "type": "bridge",
            "denom": "gravity0x2260FAC5E5542a773Aa44fBCfeDf7C193bc2C599",
            "name" : "Wrapped Bitcoin (Ethereum to Gravity-Bridge)",
            "symbol": "WBTC.grv",
            "description": "Gravity Bridge WBTC",
            "decimals": 8,
            "image": "https://raw.githubusercontent.com/CosmosLabsKR/chainlist/master/chain/ethereum/asset/wbtc.png",
            "coinGeckoId": "wrapped-bitcoin",
            "color": "#f39444",
            "bridge_info" : {
                "path": "ethereum>gravity-bridge",
                "counterparty": {
                    "chain": "ethereum",
                    "contract": "0x2260fac5e5542a773aa44fbcfedf7c193bc2c599"
                }
            }
        }
        // example IRIS
        {
            "type": "bridge",
            "denom": "htltbcbusd",
            "name" : "BUSD - Deprecated",
            "symbol": "BUSD",
            "description": "BUSD on IRIS - Deprecated",
            "decimals": 8,
            "image": "https://raw.githubusercontent.com/CosmosLabsKR/chainlist/master/chain/bnb-beacon-chain/asset/busd.png",
            "coinGeckoId": "binance-usd",
            "bridge_info" : {
                "path": "bnb-beacon-chain>iris",
                "enable": false
            }
        }
      ]
      ```


4. Commit and push to your fork

   ```shell
   git add -A
   git commit -m “Add <YOUR ASSET NAME>”
   git push origin <branch_name>
   ```

5. From your repository, make pull request (PR)
</details>

---

<details>
  <summary><h2 style='display: inline; font-size: 24px'>How to add your CW20 token info</h2></summary>

  [Juno Cw20](https://github.com/CosmosLabsKR/chainlist/blob/main/chain/juno/cw20_2.json) list supporting
1. Fork this repo to your own github account
2. Clone fork and create new branch

   ```shell
   git clone git@github.com:YOUR_ACCOUNT/chainlist.git
   cd chainlist
   git branch <branch_name>
   git checkout <branch_name>
   ```

3. Add the info of your token in the chain `cw20_2.json` file that your token needs to be displayed  
   >If there is no chain in the list, create a folder for the chain  
   Then add `cw20_2.json` file to the folder, add token info to that file   
   Changes will be updated within 24 hours after merged to master
      - `type`
        - cw20 
      - `contract`
        - Token's contract_address
      - `name`
        - Token's name
      - `symbol`
        - Name of token's symbol
      - `description`
        - A brief summary of the token
      - `decimals`
        - Decimal of the token
      - `image`
        - Image route of the token
        - `/${targetChain}/asset` add image in the folder
        - Make sure to upload a `png` file
      - `coinGeckoId`
        - Coin gecko site's API ID 
          - ex. https://www.coingecko.com/en/coins/cosmos-hub
            - API ID: *cosmos*
        - Empty string if none
      - `color` (optional)
      - `wallet_preload` (optional)
        - default value is `false`


   ### Cw20 info json example
   `chain/${targetChain}/cw20_2.json`

     - Cw20 Token

        ```json
        // example JUNO
        [
          {
              "type": "cw20",
              "contract": "juno1pqht3pkhr5fpyre2tw3ltrzc0kvxknnsgt04thym9l7n2rmxgw0sgefues",
              "name" : "DAO",
              "symbol": "DAO",
              "description": "DAO DAO",
              "decimals": 6,
              "image": "https://raw.githubusercontent.com/CosmosLabsKR/chainlist/master/chain/juno/asset/dao.png",
              "coinGeckoId": ""
          },
          {
              "type": "cw20",
              "contract": "juno168ctmpyppk90d34p3jjy658zf5a5l3w8wk35wht6ccqj4mr0yv8s4j5awr",
              "name" : "Neta",
              "symbol": "NETA",
              "description": "The native token cw20 for Neta on Juno Chain",
              "decimals": 6,
              "image": "https://raw.githubusercontent.com/CosmosLabsKR/chainlist/master/chain/juno/asset/neta.png",
              "coinGeckoId": "neta",
              "color": "#f87b7b",
              "wallet_preload": true
          }
        ]
        ```
4. Commit and push to your fork

    ```shell
      git add -A
      git commit -m “Add <YOUR TOKEN NAME>”
      git push origin <branch_name>
    ```

5. From your repository, make pull request (PR)
</details>

---

<details>
  <summary><h2 style='display: inline; font-size: 24px'>How to add your ERC20 token info</h2></summary>

  [Ethereum Erc20](https://github.com/CosmosLabsKR/chainlist/blob/main/chain/ethereum/erc20_2.json) list supporting

1. Fork this repo to your own github account
2. Clone fork and create new branch

   ```shell
   git clone git@github.com:YOUR_ACCOUNT/chainlist.git
   cd chainlist
   git branch <branch_name>
   git checkout <branch_name>
   ```

3. Add the info of your token in the chain that your token needs to be displayed  
   >If there is no chain in the list, create a folder for the chain  
   Then add `erc20_2.json` file to the folder, add token info to that file   
   Changes will be updated within 24 hours after merged to master
   - `type`
     - erc20
   - `contract`
     - Token's contract_address
   - `name`
     - Token's name
   - `symbol`
     - Name of token's symbol
   - `description`
     - A brief summary of the token
   - `decimals`
     - Decimal of the token
   - `image`
     - Image route of the token
     - `/${targetChain}/asset` add image in the folder
     - Make sure to upload a `png`file
   - `coinGeckoId` (optional)
     - Coin gecko site's API ID
       - ex. https://www.coingecko.com/en/coins/cosmos-hub
         - API ID: *cosmos*
     - Empty string if none
   - `color` (optional)
   - `wallet_preload` (optional)
     - default value is `false`


   ### Erc20 info json example
   `chain/${targetChain}/erc20_2.json`

    - ERC20 Token

      ```json
      // example Ethereum
      [
        {
            "type": "erc20",
            "contract": "0xdAC17F958D2ee523a2206206994597C13D831ec7",
            "name" : "Tether",
            "symbol": "USDT",
            "description": "Tether",
            "decimals": 6,
            "image": "https://raw.githubusercontent.com/CosmosLabsKR/chainlist/master/chain/ethereum/asset/usdt.png",
            "coinGeckoId": "tether",
            "wallet_preload": true
        },
        {
            "type": "erc20",
            "contract": "0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2",
            "name" : "WETH",
            "symbol": "WETH",
            "description": "WETH",
            "decimals": 18,
            "image": "https://raw.githubusercontent.com/CosmosLabsKR/chainlist/master/chain/ethereum/asset/weth.png",
            "coinGeckoId": "weth"
        }
      ]
      ```

4. Commit and push to your fork

   ```shell
   git add -A
   git commit -m “Add <YOUR TOKEN NAME>”
   git push origin <branch_name>
   ```

5. From your repository, make pull request (PR)
</details>

---

<details>
  <summary><h2 style='display: inline; font-size: 24px'>How to add your IBC Eureka asset info</h2></summary>

1. Fork this repo to your own github account
2. Clone fork and create new branch

   ```shell
   git clone git@github.com:YOUR_ACCOUNT/chainlist.git
   cd chainlist
   git branch <branch_name>
   git checkout <branch_name>
   ```

3. Add the info of your asset in the chain `assets_2.json` file that your asset needs to be displayed
   >If there is no chain in the list, create a folder for the chain  
   Changes will be updated within 24 hours after merged to master
   - `type`
     - `ibc`
   - `denom`
     - IBC denom on the target chain
   - `name`
     - Asset's name
   - `symbol`
     - Name of Asset's symbol
   - `description`
     - A brief summary of the asset
   - `decimals`
     - Asset's decimals
   - `image`
     - Image route of the token
     - `/${targetChain}/asset` add image in the folder
     - Make sure to upload a `png`file
   - `coinGeckoId`
     - Coin gecko site's API ID
       - ex. https://www.coingecko.com/en/coins/{API-ID}
     - Empty string if none
   - `ibc_info`
     - `path`
       - Transfer path (e.g. `ethereum>cosmos`)
     - `counterparty`
       - `ICS20ContractAddress`
         - ICS20 contract address on Ethereum
       - `channel`
         - Channel ID on the target chain
       - `port`
         - Asset's port (e.g. `transfer`)
       - `chain`
         - Source chain (e.g. `ethereum`)
       - `denom`
         - ERC20 contract address of the token on Ethereum

   ### IBC Eureka info json example
   `chain/${chain}/assets_2.json`

   - Eureka Asset

     ```json
     [
      // example USDT on Cosmos Hub
      {
          "type": "ibc",
          "denom": "ibc/E7E51FFF94A8B55BE84CEB0345E5CAF0A5DAEB374C6806CE908098B8996C7782",
          "name": "Tether",
          "symbol": "USDT",
          "description": "Tether via Eureka",
          "decimals": 6,
          "image": "https://raw.githubusercontent.com/CosmosLabsKR/chainlist/master/chain/ethereum/asset/usdt.png",
          "coinGeckoId": "tether",
          "ibc_info": {
              "path": "ethereum>cosmos",
              "counterparty": {
                  "ICS20ContractAddress": "0xa348cfe719b63151f228e3c30eb424ba5a983012",
                  "channel": "cosmoshub-0",
                  "port": "transfer",
                  "chain": "ethereum",
                  "denom": "0xdAC17F958D2ee523a2206206994597C13D831ec7"
              }
          }
      },
     
      // example SEDA on Cosmos Hub
      {
          "type": "ibc",
          "denom": "ibc/D0BD765CF2EC6B97264795351BD75685A7B806F857D7D84633F5AC5E4A9812ED",
          "name": "SEDA",
          "symbol": "SEDA",
          "description": "SEDA on the Cosmos Hub",
          "decimals": 18,
          "image": "https://raw.githubusercontent.com/CosmosLabsKR/chainlist/master/chain/ethereum/asset/seda.png",
          "coinGeckoId": "seda-2",
          "ibc_info": {
              "path": "ethereum>cosmos",
              "counterparty": {
                  "ICS20ContractAddress": "0xa348cfe719b63151f228e3c30eb424ba5a983012",
                  "channel": "cosmoshub-0",
                  "port": "transfer",
                  "chain": "ethereum",
                  "denom": "0x14862c03A0cACcC1aB328B062E64e31B2a1afcd7"
              }
          }
      }
    ]
    ```

4. Commit and push to your fork

   ```shell
   git add -A
   git commit -m "Add <YOUR TOKEN NAME>"
   git push origin <branch_name>
   ```

5. From your repository, make pull request (PR)
</details>

---

<details>
  <summary><h2 style='display: inline; font-size: 24px'>How to add endpoint</h2></summary>

To add endpoints managed by chainlist,
You must add an endpoint to `https://github.com/CosmosLabsKR/chainlist/blob/main/chain/{chain}/param_2.json`

```
{
   ...,
    "grpc_endpoint" : [
        {
            "provider": "Stakin",
            "url": "cosmoshub.grpc.stakin-nodes.com:443"
        },
        {
            "provider": "Citizen Web3",
            "url": "grpc.cosmoshub-4.citizenweb3.com:443"
        }
    ],
    "evm_rpc_endpoint" : [
        {
            "provider": "Drpc",
            "url": "https://eth.drpc.org"
        },
        {
            "provider": "Publicnode",
            "url": "https://ethereum-rpc.publicnode.com"
        }
    ],
   ...
}
```

Before requesting addition, please check whether the endpoint is operating properly using the method below.

- Check gRPC Endpoint

```sh
GRPC_URL=<GRPC_ENDPOINT_URL>

# check has grpc endpoints
grpcurl $GRPC_URL list
# check has grpc nodeinfo
grpcurl $GRPC_URL cosmos.base.tendermint.v1beta1.Service.GetNodeInfo

# check has grpc plaintext(non-TLS) endpoints
grpcurl -plaintext $GRPC_URL list
# check has grpc plaintext(non-TLS) nodeinfo
grpcurl -plaintext $GRPC_URL cosmos.base.tendermint.v1beta1.Service.GetNodeInfo
```

- Check EVM Endpoint

```sh
EVM_URL=<EVM_ENDPOINT_URL>

curl --location '$EVM_URL' \
--header 'Content-Type: application/json' \
--data '{
    "jsonrpc": "2.0",
    "method": "eth_getBlockByNumber",
    "params": [
        "latest",
        false
    ],
    "id": 1
}'
```

</details>

---

## Contact and Community
- [Official Website](https://cosmos.network/)

## License
Copyright © CosmoslabsKR, Inc. All rights reserved.
Licensed under the [MIT](LICENSE).
