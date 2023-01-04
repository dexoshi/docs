---
description: https://dexoshi.github.io/docs/
---

# Dexoshi

## Overview

Dexoshi is a Twitter trading card game on the blockchain. There are a total of 20,000 unique cards and amount of individual cards can be infinite. But not all cards are equal!

## Cards

Each card has certain properties

Name: Ivarick the Teensy Toad

Card ID: #9900

Image:

![9900](https://user-images.githubusercontent.com/19412160/210462871-110a0df1-611b-4bf9-b3b7-6dae03b22524.jpg)

Cards can be minted, burned, merged and transferred.

## Twitter Commands

### Get Twitter User's Info

Tweet

```
@dexoshi info <@TWITTER_HANDLE>
```

Example

```
@dexoshi info @elonmusk
```

### Gift a Card You Own to User

Tweet

```
@dexoshi gift <@TWITTER_HANDLE> <TOKEN_ID>
```

Example

```
@dexoshi gift @elonmusk 9900
```

### Merge Cards to Create a New Card

Player owns Card ID: #2 and #3

Merging will burn cards #2 and #3 to create card #6

Math: 2 \* 3 = 6

Tweet

```
@dexoshi merge <TOKEN_ID_1> <TOKEN_ID_2>
```

Example

```
@dexoshi burn 2 3
```

### Transfer To Address

Transfer to a 0x address

Tweet

```
@dexoshi transfer <0xADDRESS> <TOKEN_ID> <AMOUNT>
```

Example

```
@dexoshi transfer 0xdD4c825203f97984e7867F11eeCc813A036089D1 9900 1
```

### Burn

Tweet

```
@dexoshi burn <TOKEN_ID>
```

Example

```
@dexoshi burn 9900
```

