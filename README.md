<a href="https://tagion.org"><img alt="tagion logo" src="https://github.com/tagion/resources/raw/master/branding/logomark.svg?sanitize=true" alt="tagion.org" height="60"></a>

# Tagion AlphaOne Release

> The Tagion network decentralizes trading and transferring between compatible cryptocurrencies and is operated by a democratic governance mechanism: the users of the network essentially own and control the network as it is open and technically accessible for everyone.
> 
> The network itself consists of a **gossip protocol,** which is used for data synchronization, the **hashgraph algorithm**, which provides consensus and ordering transactions, and the **sharding** **opportunity,** that lets transactions run in parallel and enhances the speed of the system.


**AlphaOne** is Tagion's initial test network. It consists of a stable public network in which users can send payment requests and receive Tagions in order to test and enhance the system. Tagion **AlphaOne** is live for users, but it is a closed testnet; for access, please contact: [Roxana Nasoi](mailto:rn@i25s.com).

With **AlphaOne** and **Tagion Wallet CLI**, users can create wallets, request Tagions from the automated faucet, create and send payment requests, and transfer Tagions between wallets.

## Table of contents
- [Tagion AlphaOne Release](#tagion-alphaone-release)
  - [Table of contents](#table-of-contents)
- [Tagion AlphaOne Manual](#tagion-alphaone-manual)
  - [Preconditions](#preconditions)
    - [**Option 1**. Use the binary on Linux](#option-1-use-the-binary-on-linux)
      - [Install the `tagionwallet`](#install-the-tagionwallet)
    - [**Option 2**. Use Docker Image](#option-2-use-docker-image)
  - [AlphaOne Node IP Addresses](#alphaone-node-ip-addresses)
  - [About Tagion Wallet CLI](#about-tagion-wallet-cli)
    - [What is payment request](#what-is-payment-request)
  - [How to create the wallet](#how-to-create-the-wallet)
  - [Request Tagions](#request-tagions)
  - [Transfer Tagions between wallets](#transfer-tagions-between-wallets)
  - [Conclusion](#conclusion)
  - [Maintainers](#maintainers)
  - [Questions](#questions)
  - [Issues](#issues)


# Tagion AlphaOne Manual

This manual is intended for Tagion **AlphaOne** network users who will send and receive Tagions over the network in order to build up both user experience and a stronger network. The manual focuses on the following:

- Creating the environment in which the Tagion Wallet CLI can be used;
- Accessing Tagion AlphaOne network via the Wallet CLI;
- Creating and using the Tagion Wallet CLI to send and receive Tagions within the AlphaOne network.


## Preconditions

> **Important!**
>
> **Tagion Wallet CLI** runs only on **Linux**. If you don't have Linux, you can use our **[Docker image](#option-2-use-docker-image)** instead.
>
> *Going forward, this manual assumes you are running `tagionwallet` from Linux.*

### **Option 1**. Use the binary on Linux

#### Install the `tagionwallet`

1. [Download the wallet binary](https://github.com/tagion/alpha_one/releases/download/tagionwallet-v1.0/tagionwallet)
2. Install it to `/usr/bin`

```bash
chmod +x ./tagionwallet # Adds execution rights
cp ./tagionwallet /usr/bin # Move to other binaries
tagionwallet --help # Will output help
```

### **Option 2**. Use Docker Image

> If you **don't have Docker**, follow the [Getting Started With Docker](https://www.docker.com/get-started) guide first.

Run the following command to run the `tagion/tagionwallet` Docker image:

```bash
docker run -it tagion/tagionwallet bash
tagionwallet --help # Will output help
```

By default, all files that will be generated by the wallet in the container, will stay in the container. If you want to persist files, you need to mount a directory when running the container:

First, create directory you want to mount (you can use any directory you want):
```bash
# On Windows:
mkdir C:\tagionwallets

# On macOS or Linux
mkdir ~/tagionwallets
```

Then run the Docker container, mounting that directory:

```bash
# On Windows:
docker run -it -v C:\tagionwallets:/files tagion/tagionwallet bash

# On macOS or Linux
docker run -it -v ~/tagionwallets:/files tagion/tagionwallet bash
```

Now the `/files` directory in the container will match `C:\tagionwallets` or `~/tagionwallets` on your host machine. 



## AlphaOne Node IP Addresses

When sending `--pay` or `--update` requests via the **Tagion Wallet CLI**, you must specify the `-u` flag (**node IP to send the request to**). 

```bash
# Example that updates the local bills:
tagionwallet --update --amount -u 3.250.150.166
```

Here is a list of the first nodes, you can use any of them:

```
3.250.150.166
34.241.136.45
34.242.210.219
34.242.120.199
63.32.90.80
3.249.14.175
54.74.68.133
34.245.73.196
3.250.143.172
34.251.132.77
```

## About Tagion Wallet CLI

When using `tagionwallet`, it will generate and work with files in the directory you call it from. You can have as many wallets as you want, just by using `tagionwallet` from different directories. 

Files that are generated include:

- `tagionwallet.hibon` - configuration and seed of the specific wallet;
- `bills.hibon` - public keys of the tagion bills;
- `invoice.hibon` - **payment request** that needs to be paid by the other wallet;

Most important commands (don't use before [creating the wallet](#how-to-create-the-wallet)):

```bash
# Enter Visual UI for creating 
# wallet or generating invoices:
tagionwallet -g 

# Update the local bills.hibon:
tagionwallet --update -u 3.249.14.175

# Print amount based on your local bills.hibon:
tagionwallet --amount

# Shortcut for updating and printing:
tagionwallet --update --amount -u 3.249.14.175

# Fulfil a payment request
tagionwallet --pay ./invoice.hibon -x 1111 -u 3.249.14.175 --send
```

### What is payment request

Tagion does not have an accounting system, like most blockchains do. Instead, we store the bills in the database. The wallet software manages the keys for those bills. You can 'spend' the bills using the Tagion compatible wallet, in our case - Wallet CLI.

To send Tagions from one wallet to another, the sender must know the public key of the receiver's bill. Currently, we use a primitive system of **payment requests** (previously called *invoices*) for this. The receiver must generate the payment request, that will be fulfilled by the sender.

## How to create the wallet

You can create as many wallets as you want, having one directory for each one. For this guide, let's create two wallets, so you can send Tagions from one to the other.

``` bash
# Create two directories for each wallet
mkdir w1 w2
```

Now from each directory, enter the Visual UI and create the wallets:

```bash
cd w1
tagionwallet -g # Enter the Visual UI
# Press 'c' to enter the creation menu
# Use arrows and 'Enter' to navigate through recovery questions
# Answer at least 3 questions
# Press 'c' again to confirm
# Enter a 4-digit Pincode (will be used later)
# Press 'Enter', and hooray, you are done
# Quit the Visual UI by pressing `q` until you are out

cd ../w2
# Repeat the process
```

Now you should have `tagionwallet.hibon` file in each directory. These files are your wallets.

## Request Tagions

You need some Tagions to pay from one wallet to another. Luckily, we have an **automated faucet** that will send test Tagions to your wallet.

First, you need to generate a **payment request**:

```bash
./tagionwallet -g # Enter Visual UI
# Enter Pincode
# Press 'a' to enter account
# Press 'i' to enter invoice mode
# Type the invoice label, press enter
# and fill the sum of Tagions to generate (less then 1000)
# Quit the Visual UI by pressing `q` until you are out

ls # List all files in the Wallet directory
# ./invoice.hibon should appear
```

Then, send the `invoice.hibon` to our API:

```bash
curl -F paymentRequest=@invoice.hibon api.monitor.tagion.org/faucet/print
```

If there were no problem, you will see a message, saying "Print request was sent to the network". Wait for 5-15 seconds and check the balance:

```bash
tagionwallet --update --amount -u 3.249.14.175
```

You should see that your balance has changed.

## Transfer Tagions between wallets

Now you have Tagions in one of your wallets, you can send them to another wallet. In this guide we will show you how to send to your second wallet, that you have created previously.

```bash
# Go to your empty wallet's directory
cd ../w2

# Generate a payment request, as you did in the previous step
tagionwallet -g # Enter GUI to generate payment request (invoice)

# Go to your wallet with Tagions
cd ../w1
tagionwallet --pay ../w2/invoice.hibon -x [your pin-code] -u 3.249.14.175 --send

# Check balance in 10 seconds
tagionwallet --update --amount -u 3.249.14.175

# Once the balance is updated, you can make sure it is also
# updated in the second wallet:
cd ../w2
tagionwallet --update --amount -u 3.249.14.175
```

Congratulations! You just made your first transaction on **Tagion AlphaOne** Network.

## Conclusion

In this manual you used the Tagion Wallet CLI and public AlphaOne network to send and receive testnet Tagions. Behind the scenes, nodes used **gossip protocol** to transmit transactions, the **hashgraph algorithm** to reach consensus and order transactions, and the **DART** database to store and sync the data. The basic protocols are live and running smoothly.

---

## Maintainers

- [@cbleser](https://github.com/cbleser)
- [@alexSushko](https://github.com/alexSushko)
- [@vladpazych](https://github.com/vladpazych) (Documentation)
- [@James-at-Tagion](https://github.com/James-at-Tagion) (Documentation)

## Questions

For questions and support please use the [official forum](https://forum.tagion.org/c/development/6) or [Telegram chat](https://t.me/tagionChat). The issue list of this repo is exclusively for bug reports and feature requests.

## Issues

Please use GitHub to [report a bug](https://github.com/tagion/alpha_one/issues/new?assignees=cbleser%2C+alexSushko&labels=bug&template=bug_report.md&title=) or [request a feature](https://github.com/tagion/alpha_one/issues/new?assignees=alexSushko%2C+cbleser&labels=enhancement&template=feature_request.md&title=).
