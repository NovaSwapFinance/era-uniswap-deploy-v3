# deploy uniswap V3 on zkLink
  
## Prerequisites

Ensure the following prerequisites are met:

- Node.js
- npm (Node Package Manager)
  
## Installation

1. git clone https://github.com/uniswap-zksync/era-uniswap-deploy-v3.git
2. Modify the package.json file as follows:
```bash
Change @uniswap/v3-periphery to: https://github.com/NovaSwapFinance/era-uniswap-v3-periphery.git#v1.1.1-zksync-era
Change v3-periphery-1_3_0 to: https://github.com/NovaSwapFinance/era-uniswap-v3-periphery.git#v1.3.0-zksync-era
Change @uniswap/v3-staker to: https://github.com/AGXDEX/era-uniswap-v3-staker.git#main
```
3. Run `yarn`
Run `yarn start --confirmations 2 --json-rpc $NETWORK --native-currency-label ETH --owner-address $OWNER_ADDRESS --private-key $WALLET_PRIVATE_KEY --weth9-address $WETH_ADDRESS`
4. Log the deployment process
5. Create a new folder and clone the following repositories:
```bash
git clone https://github.com/uniswap-zksync/era-uniswap-v3-core.git
git clone https://github.com/NovaSwapFinance/era-uniswap-v3-periphery.git
git clone https://github.com/uniswap-zksync/era-uniswap-swap-router-contracts.git
git clone https://github.com/uniswap-zksync/era-openzeppelin-contracts.git
```
6. Prepare a .env file with the following content:
```bash
NETWORK=https://rpc.zklink.io
WALLET_PRIVATE_KEY=
OWNER_ADDRESS=
WETH_ADDRESS=
UNISWAPV3_FACTORY=
UNISWAP_INTERFACE_MULTICALL=
TICKLENS=
NFTDESCRIPTOR=
NONFUNGIBLE_TOKENPOSITION_DESCRIPTOR=
TRANSPARENT_UPGRADEABLE_PROXY=
NONFUNGIBLE_POSITION_MANAGER=
V3MIGRATOR=
UNISWAPV3_STAKER=
QUOTERV2=
SWAPROUTER02=
PROXYADMIN=
DESCRIPTORPROXY=
```
7. Add the following configuration to the hardhat.config.ts file for each of the four projects, changing the defaultNetwork to zkLinkNovaMainnet
```bash
zkLinkNovaMainnet: {
      url: 'https://rpc.zklink.io',
      ethNetwork: 'mainnet',
      zksync: true,
      verifyURL: 'https://explorer.zklink.io/contract_verification',
},
```
8. Run `yarn` in each project to download the  
dependency packages
Verify each contract based on the deployment logs and the directory structure using the following command for each contract:
```bash
npx hardhat verify --network zkLinkNovaMainnet <contract address> <parameters>
```
9. Deploy the factory contract
10. Deploy the permit contract:
```bash
git clone https://github.com/uniswap-zksync/era-permit2.git
```
11. Run `forge install and yarn`
12. Modify the deploy.ts file by changing CREATE2_FACTORY_ADDRESS to the factory contract address
13. Run `yarn deploy --json-rpc https://rpc.zklink.io --private-key <PRIVATE_KEY>`
14. Deploy the remaining two contracts:
```bash
git clone https://github.com/uniswap-zksync/era-universal-router.git
```
15. Run `forge install and yarn`
16. Add nova parameters under script/deployParameters/, following the format in zksync_era_testnet.json
Update permit2 to the newly deployed permit contract、weth9、v3Factory to the newly deployed factory contract, and leave others as 0x000
17. poolInitCodeHash without changes
18. Add the following configuration to hardhat.config.ts, changing defaultNetwork to zkLinkNovaMainnet:
```bash
zkLinkNovaMainnet: {
      url: 'https://rpc.zklink.io',
      ethNetwork: 'mainnet',
      zksync: true,
      verifyURL: 'https://explorer.zklink.io/contract_verification',
},
```
19. Run `yarn hardhat --network zkLinkNovaMainnet deploy --private-key <PRIVATE_KEY> --params <pathToJSON> and --verify`
