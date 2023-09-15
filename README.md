# Polkadot-Final-Project

## 1. Building a blockchain
Clone the template for substrate node
```
git clone https://github.com/substrate-developer-hub/substrate-node-template
```
Change my directory to be in the project 
```
cd substrate-node-template
```
Created a new branch 
```
git switch -c my-new-branch
```
![polka1](https://user-images.githubusercontent.com/119344636/268200111-380e3b9e-b6e0-4fc3-b48a-e6b4e6382186.png)
To start the node, we first need to build and compile this project
```
cargo build --release
```
![polka4](https://user-images.githubusercontent.com/119344636/268207982-fa3930c3-0988-45be-8511-45d85c6e0420.png)
Then start the node 
```
./target/release/node-template --dev
```
![polka5](https://github.com/lalamariposa/Polkadot-Final-Project/assets/119344636/fa3930c3-0988-45be-8511-45d85c6e0420)
Open a new terminal and check if you have node and yarn installed
```
node --version
yarn --version
```
Clone the frontend template for substrate node 
```
git clone https://github.com/substrate-developer-hub/substrate-front-end-template
```
Change directory 
```
cd substrate-front-end-template
```
Start the project and the frontend 
```
yarn install
yarn start 
```
![polka2](https://user-images.githubusercontent.com/119344636/268204691-b987e1bf-e406-47aa-83cb-37010709029f.png)
![polka3](https://user-images.githubusercontent.com/119344636/268204711-60071994-db19-4cff-bcda-6bcf561f9dc2.png)
![polka6](https://github.com/lalamariposa/Polkadot-Final-Project/assets/119344636/61d0c42b-bcaa-40e3-89ee-6383783df70f)

## 2. Simulating a substrate network
Start a new terminal, change directory into the project and purge old chain data
```
./target/release/node-template purge-chain --base-path /tmp/alice --chain local
```
Then press 'y' for yes 

Start the local blockchain node using the “alice” account
```
./target/release/node-template 

--base-path /tmp/alice 

--chain local 

--alice 

--port 30333 

--rpc-port 9933 

--node-key 0000000000000000000000000000000000000000000000000000000000000001 

--telemetry-url "wss://telemetry.polkadot.io/submit/ 0" 

--validator
```
Didn't include `--ws-port 9945` 

Open up a new terminal to start and interact with the second node and purge old chain data
```
./target/release/node-template purge-chain --base-path /tmp/bob --chain local -y
```
Start the new node but using “bob” account
```
./target/release/node-template 

--base-path /tmp/bob 

--chain local 

--bob 

--port 30334 

--rpc-port 9934 

--telemetry-url "wss://telemetry.polkadot.io/submit/ 0" 

--validator 

--bootnodes /ip4/127.0.0.1/tcp/30333/p2p/12D3KooWEyoppNCUx8Yx66oV9fJnriXwCcXwDDUA2kj6vnc6iDEp
```
Didn't include `--ws-port 9946`

![polka7](https://user-images.githubusercontent.com/119344636/268216689-825397f7-b959-455c-a0a0-88c788bc5f6f.png)














