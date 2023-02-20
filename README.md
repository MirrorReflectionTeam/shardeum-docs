<!--
parent:
  order: false
-->

<div align="center">
  <h1> Shardeum</h1>
</div>

![image](https://github.com/MirrorReflectionTeam/shardeum-docs/blob/master/Shardeum.png)

## What is Shardeum?

Shardeum is an EVM-based, linearly scalable smart contract platform that provides low gas fees forever while maintaining true decentralization and solid security through dynamic state sharding.

## Hardware Requirements

Installation on server **[Hetzner - CPX31:](https://hetzner.cloud/?ref=AwVksaI2T3Nz) 4 CPU, 8 GB RAM, 160 GB SSD.**

## Manual Setup

Update packages and Install tools

```
sudo apt update && sudo apt upgrade -y
sudo apt install curl build-essential pkg-config libssl-dev git wget jq make gcc tmux chrony -y
```

Install Docker and docker-compose

```
. <(wget -qO- https://raw.githubusercontent.com/SecorD0/utils/main/installers/docker.sh)
```

Install apparmor

```
sudo apt install apparmor-profiles
```

Setup permissions for docker-compose

```
sudo chmod +x /usr/bin/docker-compose
```

## Download and install validator

Download and run script

```
curl -O https://gitlab.com/shardeum/validator/dashboard/-/raw/main/installer.sh && chmod +x installer.sh && ./installer.sh
```

The terminal will ask questions about your setup settings.

Give permission to collect validator data for bug reporting:

**By running this installer, you agree to allow the Shardeum team to collect this data. (y/n)?:** Enter **y**

Enter y to setup the web based dashboard:

**Do you want to run the web based Dashboard? (y/n): y**

Set a password for dashboard access:

**Set the password to access the Dashboard:**

Add a custom session port for the web based dashboard or hit enter for port 8080:

**Enter the port (1025-65536) to access the web based Dashboard (default 8080):**

Set the first p2p port (default 9001):

**This allows p2p communication between nodes. Enter the first port (1025-65536) for p2p communication (default 9001):**

Set the second p2p port (default 10001):

**Enter the second port (1025-65536) for p2p communication (default 10001):**

Add a custom path or install to root:
**What base directory should the node use (defaults to ~/.shardeum):** Enter

Wait for the installation process to complete.

Install and Open ports in firewall

```
sudo apt install ufw
sudo ufw allow 22
sudo ufw allow 9001
sudo ufw allow 10001
sudo ufw enable
sudo ufw reload
```

**If you used custom ports instead of 9001 and 10001, enter your ports**

## Open validator CLI

Go to the hidden Shardeum directory:

```
cd && cd .shardeum
```

Start the CLI by running the following shell script:

```
./shell.sh
```

Checking node status

```
operator-cli gui status
```

The output should look something like this:

![image](https://github.com/MirrorReflectionTeam/shardeum-docs/blob/master/gui%20status.jpg)

## Start validator

Go to your web browser and go to: **https://<server_ip>:8080/** "server ip" - Hetzner or another server you rent

You will be asked for your password set during setup.

The login will fail even if you put no password during the setup process. To set a new password inside the validator CLI:

```
operator-cli gui set password <type_new_password__here>
```

You should see the “Overview” page for the Shardeum Validator Dashboard in your web browser:

![image](https://github.com/MirrorReflectionTeam/shardeum-docs/blob/master/overview.jpg)

Go to the “Maintenance” page, then click the “Start Node” button in the top left white box

Go to terminal and start node:

```
operator-cli start
```
Then go to web browser and refresh the page.

The node is running correctly if the “Start Node” button now says “Stop Node”.

Connect Wallet to Betanet [Sphinx](https://docs.shardeum.org/Network/Endpoints#connect-wallet)

Get SHM from Betanet [Faucet](https://docs.shardeum.org/Faucet/Claim#shardeum-faucet-website)

## Stake SHM to validator

After you start the validator, go to the “Settings” page. You will be asked to connect your wallet

After you connect your wallet, you should click "Add Stake"

Fill minimum 10 SHM tokens and click the “Stake” button.

Your wallet will ask you to sign the transaction stake your SHM.

Once the transaction is signed and complete, you have staked your SHM tokens successfully.

## Uninstall Node

```
cd ~/.shardeum
./cleanup.sh
cd ~/
rm -rf .shardeum
rm installer.sh
```

## Useful Commands

To exit the shell, use the command

```
exit
```

Stop node

```
operator-cli stop
```

Check node

```
operator-cli gui status
```
