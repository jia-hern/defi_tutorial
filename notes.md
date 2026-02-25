https://codewave.com/insights/blockchain-dapp-development-guide/

https://coinsbench.com/how-i-built-a-dapp-token-farm-4b3b3209ec53

https://www.youtube.com/watch?v=CgXQC4dbGUE

timestmap 6.01 for installing

install chocolately
https://chocolatey.org/install

Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

install node:
12.18.3 LTS

choco install --force --version 1.1.12 nvm.install
nvm install 12.18.3
nvm use 12.18.3

install ganache

truffle framework
npm i --g truffle@5.1.39

npm install -g solc@0.5.16

install meta mask dependency on chrome extension

truffle-config.js is the config used to connect to the ganache blockchain
need to match the same port 7545

added the contracts_directory and contracts_build_directory

/migration/2_deploy_contacts.js -> used to put new contracts in the blockchain

to compile the truffle:
after this is done:
src/abis -> got new json files

# 1

truffle compile

got issues with truffle compile
version: "0.5.16", // Fetch exact version

//
https://relay.trufflesuite.com/solc/bin/list.json
cannot access this from my home network

C:\Users\Jia Ho\AppData\Roaming\npm\node_modules

# to put the truffle migrations on the blockchain

truffle migrate

# 2

truffle migrate --reset

# to interact with the smart console

# 3

truffle console
// next line works because of how we defined tokenFarm in mgirations/2_deploy_contracts.js
tokenFarm = await TokenFarm.deployed() --> gives undefined but its working, see next line
tokenFarm.address --> prints the value

name = await tokenFarm.name() --> gives undefined
name --> prints name

truffle console

mDai = await DaiToken.deployed() --> gives undefined

accounts = await web3.eth.getAccounts() --> gives undefined

accounts[1] --> prints the value e.g. 0x33 //can chec 0x33 in ganache

balance = await mDai.balanceOf(accounts[1]) --> gives undefined
balance --> prints a json
balance.toString() --> prints the value e.g. 100 with more zeroes because of 18 dp

formattedBalance = web3.utils.fromWei(balance) --> gives undefined
balance --> prints the value e.g. 100 because of convert wei to ether

e.g.
web3.utils.toWei('1.5','Ether') -> 15000000000000000

create /test for tests because cannot change the code in the smart contract

chai is the assertion library used for testing

# 4 to run the test in /test/TokenFarm.test.js

truffle test

msg is a global variable in solidity
msg.sender is the person who initiated that.

mapping is used to store key value pairs in an object variable

address[] is an array of addresses
hasStaked to keep track of who has staked how much

need to arrove then can stakeToken
e.g.
// Stake Mock DAI Tokens
await daiToken.approve(tokenFarm.address, tokens("100"), {
from: investor,
});
await tokenFarm.stakeTokens(tokens("100"), { from: investor });

1.23.50
allowing app to issue tokens to people

issueTokens in TokenFarm.sol

// is a for loop
for (uint i=0; i<stakers.length; i++) {
}

/\*
address recipient = stakers[i];
uint balance = stakingBalance[recipient];
if(balance > 0) {
dappToken.transfer(recipient, balance);
}

\*/

above code issue same amount of dap token

modified for 50:30:20

\*
if(balance > 0) {
uint reward1 = balance _ 50 / 100;
uint reward2 = balance _ 30 / 100;
uint reward3 = balance \_ 20 / 100;
dappToken.transfer(recipient, reward1 + reward2 + reward3);
}
\*\

require(condition, "string")
if condition is true then the rest of the code runs

scripts/issue-token.js
can run this script to issue the tokens

# run the script

truffle exec scripts/issue-token.js

web3.js used to make react app web3

loadWeb3 method in App.js used to connect the app to the block chain
loadBlockchainData is used to fetch the accounts data

2.25.31 the token interest demo
