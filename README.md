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
Then start the node 
```
./target/release/node-template --dev
```
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
![polka2]()
![polka3]()










