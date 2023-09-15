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

## 3. Adding trusted nodes to a network

### Generate account and keys

Start two new terminals and change the user for one of the terminals with `su secondUser` then enter the password 

Generate a random secret phase and keys by running the following command

```
./target/release/node-template key generate --scheme Sr25519 --password-interactive
```
Generated Aura key for the first user

![polka8](https://github.com/lalamariposa/Polkadot-Final-Project/assets/119344636/ab52c2f1-4b2f-4de1-8e71-77ffefcc4079)

Generated Aura key for the second user 

![polka9](https://github.com/lalamariposa/Polkadot-Final-Project/assets/119344636/33bb8ab5-09e0-49b7-8b78-eb096e42503c)

Use the seed phrase to derive keys using the Ed25519 signature scheme

```
./target/release/node-template key inspect --password-interactive --scheme Ed25519 "seed phrase" 
```
Generated Grandpa key for the first user

![polka10](https://github.com/lalamariposa/Polkadot-Final-Project/assets/119344636/4b875084-136e-40a7-8b1c-2b870636af2b)

Generated Grandpa key for the second user

![polka11](https://github.com/lalamariposa/Polkadot-Final-Project/assets/119344636/8ea4cab3-5101-4e1f-bbe3-f3ee60c245f0)

### Create a custom chain specification 

Instead of writing a completely new chain specification, you can modify the predefined local chain specification

Export the local chain specification to a file named customSpec.json with the following command

```
./target/release/node-template build-spec --disable-default-bootnode --chain local > customSpec.json
```
Make some changes to the customSpec.json file, open it up in a text editor

Modify the name field

![polka12](https://github.com/lalamariposa/Polkadot-Final-Project/assets/119344636/dda2f009-6554-4dd5-80b8-5aa9441be804)

Modify the aura field

Modify the grandpa field

![polka13](https://github.com/lalamariposa/Polkadot-Final-Project/assets/119344636/a6ba6677-5f72-41d3-9d13-937594c896e2)

Convert the customSpec.json chain specification to the raw format with the file name customSpecRaw.json
```
./target/release/node-template build-spec --chain=customSpec.json --raw --disable-default-bootnode > customSpecRaw.json
```

To start the first node 
```
./target/release/node-template 

  --base-path /tmp/node01 

  --chain ./customSpecRaw.json 

  --port 30333 

  --rpc-port 9933 

  --telemetry-url "wss://telemetry.polkadot.io/submit/ 0" 

  --validator 

  --rpc-methods Unsafe 

  --name MyNode01 

  --password-interactive
```

Didn't include `--ws-port 9945 `

### Adding keys to keystore

For each node:

- Add the aura authority keys to enable block production.
- Add the grandpa authority keys to enable block finalization.

For the first node: 

```
./target/release/node-template key insert --base-path /tmp/node01 \

  --chain customSpecRaw.json \

  --scheme Sr25519 \

  --suri <your-secret-seed> \

  --password-interactive \

  --key-type aura
```
```
./target/release/node-template key insert \

  --base-path /tmp/node01 \

  --chain customSpecRaw.json \

  --scheme Ed25519 \

  --suri <your-secret-key> \

  --password-interactive \

  --key-type gran
```

Verify that the keys are in the keystore for node01

```
ls /tmp/node01/chains/local_testnet/keystore
```

![polka14](https://github.com/lalamariposa/Polkadot-Final-Project/assets/119344636/2e22b7a9-ed54-41ba-9256-498d464e1535)

For the second node: 

```
./target/release/node-template key insert --base-path /tmp/node02 \

  --chain customSpecRaw.json \

  --scheme Sr25519 \

  --suri <second-participant-secret-seed> \

  --password-interactive \

  --key-type aura
```
```
./target/release/node-template key insert --base-path /tmp/node02 \

  --chain customSpecRaw.json \

  --scheme Ed25519 --suri <second-participant-secret-seed> \

  --password-interactive \

  --key-type gran
```

Verify that the keys are in the keystore for node02

```
ls /tmp/node02/chains/local_testnet/keystore
```

![polka15](https://github.com/lalamariposa/Polkadot-Final-Project/assets/119344636/27f536f8-4217-4898-a3d7-f90bfdc42add)

Start the first node

```
./target/release/node-template \

  --base-path /tmp/node01 \

  --chain ./customSpecRaw.json \

  --port 30333 \

  --rpc-port 9945 \

  --telemetry-url "wss://telemetry.polkadot.io/submit/ 0" \

  --validator \

  --rpc-methods Unsafe \

  --name MyNode01 \

  --password-interactive
```

Start the second node 

```
./target/release/node-template \

  --base-path /tmp/node02 \

  --chain ./customSpecRaw.json \

  --port 30334 \

  --rpc-port 9946 \

  --telemetry-url 'wss://telemetry.polkadot.io/submit/ 0' \

  --validator \

  --rpc-methods Unsafe \

  --name MyNode02 \

  --bootnodes /ip4/127.0.0.1/tcp/30333/p2p/12D3KooWLmrYDLoNTyTYtRdDyZLWDe1paxzxTw5RgjmHLfzW96SX \

  --password-interactive
```

![polka16](https://github.com/lalamariposa/Polkadot-Final-Project/assets/119344636/13698dc8-f926-427a-ba3a-0308e4253c73)



![polka17]()
![polka18]()
![polka19]()










