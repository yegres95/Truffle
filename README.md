## Setting up Mist


### Dependencies

* `Node.js` v7.x (use the prefered installation method for your OS)
* `Meteor` javascript app framework
* `Yarn` package manager
* `Electron` v1.4.15 cross platform desktop app framework
* `Gulp` build and automation system

```
$ curl https://install.meteor.com/ | sh
$ curl -o- -L https://yarnpkg.com/install.sh | bash
$ yarn global add electron@1.4.15
$ yarn global add gulp
```

### Mist setup

Now you're ready to initialize Mist for development:

```
$ cd ~/Desktop
$ mkdir mist_test
# cd mist_test
$ git clone https://github.com/ethereum/mist.git
$ cd mist
$ yarn
$ cd interface && meteor --no-release-check
```
While meteor is running open another terminal window and go back to the folder you created `/Desktop/mist_test/mist`

Now lets run electron for the first time:

```
$ cd ~/Desktop/mist_test/mist
$ yarn dev:electron
```
![Alt text](https://scontent-iad3-1.xx.fbcdn.net/v/t1.0-9/21686188_1989133898010328_7137568609932587406_n.jpg?oh=42af6e65337729d4b88469533c99eec4&oe=5A55EC48)

* Launch the application in test network
* Wait for past blocks to download
* Write down your ethereum address (we need this later)
* `0x6a6401AEb4a3beb93820904E761b0d86364bb39E` 
* This is my test ethereum wallet, every time you see this wallet in my code you should replace this with your wallet

### Were done with mist!

If you want to read more about mist [you can do so here.](https://github.com/ethereum/mist "Ethereum's github") For now close both terminals. The one running meteor and the one running mist/electron.
* Make sure to close both terminals

# Truffle setup

Lets install truffle and get testrpc

* `$ npm install -g truffle`
* `$ npm install -g ethereumjs-testrpc`

Now we can go ahead and start a truffle app

* `$ cd ~/Desktop`
* `$ mkdir truftest`
* `$ cd truftest`
* `$ truffle unbox react`

So we can start the servers

* `$ testrpc`

in another terminal go into your truffle folder
* `$ cd ~/Desktop/truftest`
* `$ truffle compile`
* `$ truffle migrate`
* `$ npm start`

Now we can play with the solidity and react on the site.

# Connecting to Rinkeby 

Make sure to close the terminal 

First, start geth with Rinkeby and make sure that the correct APIs for Truffle are enabled.
```
geth --rinkeby --rpc --rpcapi db,eth,net,web3,personal --unlock="0x6a6401AEb4a3beb93820904E761b0d86364bb39E" --rpccorsdomain http://localhost:3000
```
Please dont forget to replace my wallet with the wallet you got from mist/electron.

This will ask you for the password you gave mist/electron.

Next, we need to add Rinkeby to our truffle config file. If we open `truffle.js` in our contract code we’ll see something like:

```
module.exports = {
  rpc: {
    host: 'localhost',
    port: '8545'
 },
  networks: {
    development: {
      host: "localhost",
      port: 8545,
      network_id: "*" // Match any network id
    },
    rinkeby: {
      host: "localhost", // Connect to geth on the specified
      port: 8545,
      from: "0x6a6401AEb4a3beb93820904E761b0d86364bb39E", // default address to use for any transaction Truffle makes during migrations
      network_id: 4,
      gas: 4612388 // Gas limit used for deploys
    }
  },
};
```
