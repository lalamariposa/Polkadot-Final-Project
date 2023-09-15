# Polkadot-Final-Project

## 1. Building a blockchain
First I cloned the template for substrate node
```
git clone https://github.com/substrate-developer-hub/substrate-node-template
```
Then I changed my directory to be in the project 
```
cd substrate-node-template
```
Created a new branch 
```
git switch -c my-new-branch
```
To start the node, we first need to build and compile this project
```
cargo build --release
```
Then I started the node 
```
./target/release/node-template --dev
```





