# About
A NFT contract that uses ERC-721 and Base64 from openzeppelin and that can switch it's mood. 
It is a SVG NFT that is hosted 100% on-chain.
Stay stuned for my work in the future. Thanks!

<br/>
<p align="center">
<img src="./img/happy.svg" width="225" alt="NFT Happy">
<img src="./img/sad.svg" width="225" alt="NFT Frown">
</p>
<br/>

# Getting started

## Requirements
- [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
  - You'll know you did it right if you can run `git --version` and you see a response like `git version x.x.x`
- [foundry](https://getfoundry.sh/)
  - You'll know you did it right if you can run `forge --version` and you see a response like `forge x.x.x`

## Quickstart
```
git clone https://github.com/robivagner/foundry-mood-nft
cd foundry-mood-nft
```

# Usage

## Deploy

Quick deploy
```
forge script script/DeployMoodNft.s.sol 
```

Deploy on anvil chain (2 terminal windows needed)
First terminal:
```
anvil
```

Second terminal:
```
forge script script/DeployMoodNft.s.sol:DeployMoodNft --rpc-url http://127.0.0.1:8545
```

Now if you'd like to call the mint function for example and see the nft in your metamask wallet you can use the cast command to call functions for example:
```
cast send <DEPLOYED_CONTRACT_ADDRESS> "mintNft()" --private-key <PRIVATE_KEY> --rpc-url http://127.0.0.1:8545
```
After you have used this command you can go to your metamask wallet and import the nft with the contract address and the nft index (should be 0 if u only used the command once since it's the first nft minted).

If you'd like to call the flipMood function and see the nft flip mood in your wallet use this command:
```
cast send <DEPLOYED_CONTRACT_ADDRESS> "flipMood(uint256)" 0 --private-key <PRIVATE_KEY> --rpc-url http://127.0.0.1:8545
```
Now you will have to go to your wallet again delete the previous nft and import it again to refresh it.

## Testing

If you want to do unit testing
```
forge test
```

If you want to do forked testing on the sepolia chain for example(the $SEPOLIA_RPC_URL is a enviromental variable check the deployment paragraph to see how it's done)

```
forge test --fork-url $SEPOLIA_RPC_URL
```

### Test coverage

To see the test coverage percentage

```
forge coverage
```

# Deployment to a testnet or mainnet

1. Setup environment variables

You'll want to set your `SEPOLIA_RPC_URL` and `PRIVATE_KEY` as environment variables. You can add them to a `.env` file, like this

```
SEPOLIA_RPC_URL=EXAMPLE_URL
PRIVATE_KEY=EXAMPLE_PRIVATE_KEY
ETHERSCAN_API_KEY=EXAMPLE_ETHERSCAN_API_KEY
```

Then you can type:

```
source .env
```

to use them in the command line after you saved the .env file.


!!PLEASE do NOT put your actual private key in the .env file it is NOT good practice. 
!!EITHER put the private key of a wallet you won't have actual money in OR use this command to store your private key interactively in a encrypted form:
```
cast wallet import <NAME_OF_ENCRYPTED_PRIVATE_KEY_WALLET> --interactive
```

2. Get testnet ETH

Head over to [faucets.chain.link](https://faucets.chain.link/) and get some testnet ETH. You should see the ETH show up in your metamask.

3. Deploy

```
forge script script/DeployMoodNft.s.sol:DeployMoodNft --rpc-url $(SEPOLIA_RPC_URL) --account <NAME_OF_ENCRYPTED_PRIVATE_KEY_WALLET> --broadcast --verify --etherscan-api-key $(ETHERSCAN_API_KEY)
```

To get the etherscan api key go to their [site](https://etherscan.io/), sign in, hover over your name and go to api keys. 
Then u can click add, give it a name, copy the API key token and put it in an enviromental variable in the .env file like shown above.

## Scripts

After deploying to a testnet(for example sepolia), you can run the scripts.

Using cast deployed locally example:

```
cast send <DEPLOYED_CONTRACT_ADDRESS> "minfNft()" --account <NAME_OF_ENCRYPTED_PRIVATE_KEY_WALLET> --rpc-url $SEPOLIA_RPC_URL
```

## Estimate gas

You can estimate how much gas things cost by running:

```
forge snapshot
```

And you'll see an output file called `.gas-snapshot`

# Thank you!

Another fun and simple project to create and add to my arsenal.