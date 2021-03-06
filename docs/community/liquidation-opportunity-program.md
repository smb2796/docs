---
title: Liquidation Opportunity Program
sidebar_label: Liquidation Opportunity Program
---

The Liquidation Opportunity Program is designed to incentivize community members
to run liquidation bots. Intentionally under-collateralized positions will be
created to reward community members for keeping the UMA system secure and
appropriately collateralized.

## When is the next opportunity?

On Friday, August 14th at 11:30am Pacific Time (i.e. San Francisco time), Risk Labs will intentionally create an under-collateralized
position, creating an on-chain profit opportunity of approximately \$1,000 for
any liquidator bot to take.

## What do I need to liquidate a position?

You'll need to make sure you have an account loaded with enough `yUSD` to
liquidate the position, and also enough `ETH` to pay for the necessary gas costs
associated with the liquidation transaction.

## How do I run a bot?

The in-depth tutorial [here](tutorials/bots.md) will walk you through the
process of running a bot through various methods. However, the most expedient
way to run a bot is from the Docker image. This process is detailed in the
Docker [section](tutorials/bots.md#running-the-bots-locally-with-docker) of that
tutorial.

For your convenience, however, the following is a quick summary of the important
points.

### Minimal quick start guide

:::caution

This short guide only teaches you how to run a bot. To take advantage of the
liquidation opportunity, you will have to tweak your polling interval and
[liquidation sensitivity](tutorials/bots.md#specifying-liquidation-sensitivity-parameters)
amongst other variables.

:::

First, create a file to set the appropriate configuration for your liquidation
bot. Please edit the following example with your own values. You can reference
the [tutorial](tutorials/bots.md) for appropriate values.

```shell title="example.env"
EMP_ADDRESS=0xb56C5f1fB93b1Fbd7c473926c87B6B9c4d0e21d5
PRIVATE_KEY=0xf7cbade2b9eec8fc83aa70e4b43f480d0ca78b7060737ead2669d095f2035322
COMMAND=yarn truffle exec ./packages/liquidator/index.js --network mainnet_privatekey
PRICE_FEED_CONFIG={"apiKey":"CRYPTO-WATCH-API-KEY"}
```

Once you have a properly configured `.env` file, use the following commands to
pull the Docker image and run a container with your specified configuration.

```shell
# Pull the latest docker container image
docker pull umaprotocol/protocol:latest

# Start the liquidator bot Docker container
docker run --name liquidator-bot -d --env-file ./example.env umaprotocol/protocol:latest
# *your container hash should print here*

# List logs from running bot:
docker logs <your container hash>
```

When you are familiar with using the Docker image, you can deploy the Docker
image on any cloud service provider of your choice, or alternatively you could
run it locally on your machine.
