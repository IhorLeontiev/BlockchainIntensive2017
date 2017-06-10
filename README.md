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
curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash –
sudo apt-get update -y && sudo apt-get upgrade -y
4. Install the NodeJs
sudo apt-get install -y build-essential python nodejs
5. Upgrade npm before install tools
sudo npm install -g npm 
sudo npm install -g ethereumjs-testrpc truffle
if you have acces error, try to use unsafe parameters - sudo npm install --unsafe-perm --verbose -g ethereumjs-testrpc
6. Intall geth
sudo apt-get install software-properties-common
sudo add-apt-repository -y ppa:ethereum/ethereum
sudo apt-get update
sudo apt-get install ethereum

# Linux installation
The same as for Windows subsytem 

#Test Guide

1. How to use truffle console
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
2. For BASIC Truffle project
truffle init
Truffle console:
//How to get accounts
web3.eth.accounts

//How to get reference to deployed contract
var metaCoin;
MetaCoin.deployed().then(function(deployed) {metaCoin = deployed;});

//How to get balance of account 0
metaCoin.getBalance.call(web3.eth.accounts[0])

//How to send coins
var account0 = web3.eth.accounts[0];
var account1 = web3.eth.accounts[1];
metaCoin.sendCoin(account1, 1000, {from: account0});
metaCoin.getBalance.call(account0);


