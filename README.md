# BlockchainIntensive2017
Hi all this repository for support Microsoft Blockchain Intense 2017

# Nedeed instruments
Truffle framework
http://truffleframework.com/
https://truffle-box.github.io/
TestRPC https://github.com/ethereumjs/testrpc
Geth - https://github.com/ethereum/go-ethereum/wiki/Installation-Instructions-for-Ubuntu

# How to set-up Dev Environment
# Windows Subsytem for Linux intallation:
1. Turn-om Windows subsystem for Linux in "Turn Windows Features on or off"
More info - https://msdn.microsoft.com/en-us/commandline/wsl/install_guide
2. Start Ubuntu Bash from searching bar
3. Takes a clean Ubuntu image, up to being dev ready.
install npm from official repo, as apt-get has a very old version of npm:

    `curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash -`

    `sudo apt-get update -y && sudo apt-get upgrade -y`
4. Install the NodeJs

    `sudo apt-get install -y build-essential python nodejs`

5. Upgrade npm before install tools

    `sudo npm install -g npm` 
    
    `sudo npm install -g ethereumjs-testrpc truffle`

    *if you have access error, try to use* 

    `unsafe parameters - sudo npm install --unsafe-perm --verbose -g ethereumjs-testrpc`

6. Intall geth

    `sudo apt-get install software-properties-common`

    `sudo add-apt-repository -y ppa:ethereum/ethereum`

    `sudo apt-get update`
    
    `sudo apt-get install ethereum`

# Linux installation
The same as for Windows subsytem 

# Mac installation

1. Install Homebrew
   
   `More installation information and options at http://docs.brew.sh/Installation.html.`

2. Check that you have latest version of Xcode

3. Install NodeJs
    
    `brew install node`
    
    To make sure you have Node and NPM installed, run two simple commands to see what version of each is installed
    
    `node -v`
    `npm -v`
    
    How to Update Node and NPM
    
    `brew update`
    `brew upgrade node  `

4. Intall geth

    `brew tap ethereum/ethereum`
    `brew install ethereum`
    
    You can install the develop branch by running --devel
    
    `brew install ethereum --devel`


# Test Guide

1. How to use truffle console
```
Truffle v3.2.5 - a development framework for Ethereum
Usage: truffle <command> [options]
Commands:
  init      Initialize new Ethereum project with example contracts and tests
  compile   Compile contract source files
  migrate   Run migrations to deploy contracts
  deploy    (alias for migrate)
  build     Execute build pipeline (if configuration present)
  test      Run Mocha and Solidity tests
  console   Run a console with contract abstractions and commands available
  create    Helper to create new contracts, migrations and tests
  install   Install a package from the Ethereum Package Registry
  publish   Publish a package to the Ethereum Package Registry
  networks  Show addresses for deployed contracts on each network
  watch     Watch filesystem for changes and rebuild the project automatically
  serve     Serve the build directory on localhost and watch for changes
  exec      Execute a JS module within this Truffle environment
  version   Show version number and exit

See more at http://truffleframework.com/docs
```
2. For BASIC Truffle project
```
truffle init
truffle console
```
-How to get accounts
```
web3.eth.accounts
```

2.1. How to get reference to deployed contract
```
var metaCoin;
MetaCoin.deployed().then(function(deployed) {metaCoin = deployed;});
```

2.2. How to get balance of account 0
```
metaCoin.getBalance.call(web3.eth.accounts[0])
```

2.3. How to send coins
```var account0 = web3.eth.accounts[0];
var account1 = web3.eth.accounts[1];
metaCoin.sendCoin(account1, 1000, {from: account0});
metaCoin.getBalance.call(account0);
```

# How to deploy Smart Contract to Ethereum BaaS on Azure by using truffle

1. Go to folder with truffle project
2. Add parameters of Deployed Azure template to truffle.js:
```
    module.exports = {
  networks: {
  azure :{
      host: "", //Adress of your Azure RPC endpoints (Deployments - Output)
      port: 8545, //Port of RPC - basically rest the same
      network_id: "" //Network id which you have choose when created the network 
    },
    development: {
      host: "localhost",
      port: 8545,
      network_id: "*" // Match any network id
    }
  }
};
```
3. Safe file
4. Try to migrate your Smart contact by using ```truffle migrate --network azure```
```
You will get the following error:
Running migration: 1_initial_migration.js
  Deploying Migrations...
Error encountered, bailing. Network state unknown. Review successful transactions manually.
Error: account is locked 
For resolve this problemm you need to unlock the account
```
5. Connect to your TX node (Deployments - Output - SSH to first Tx node)
6. Run ```geth attach``` command
7. Run ```personal.unlockAccount(eth.coinbase)``` command to unlock the account
8. Migrate your smart contract ```truffle migrate --network azure```
9. To connect to truffle console type ```truffle console --network azure```
