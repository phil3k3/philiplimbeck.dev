---
layout: single
title:  "How to run an Ethereum Validator with Rocketpool"
date:   2021-01-15 16:11:35 +0200
---

* Introduction

For those who don't know how Ethereum Proof-of-Stake works, a short primer. Unlike Bitcoin, where Proof-of-Work was utilized
as proofing algorithm (finding hashes of a specific difficulty), in Ethereum and many other blockchain networks, this is replaced
by Proof-of-Stake. Basically, you get attestation rights by putting a lot of money on the table and risking it to be taken away from
you should you act maliciously or carelessly.

At time of writing, 32 ETH (around 50k US Dollars) are required to run a validator. As this excludes a lot of people
from participation, Liquid Staking Protocols emerged such as Lido or Rocketpool. The idea is to model the dynamics of staking
by introducing another asset which will accrue in value as more staking rewards are issued to the validators.

Rocketpool also allows running a validator with less than 32 ETH (namely 8 and 16 ETH) which is more easily to finance.
These so-called minipools are formed by bundling your own stake together with the remaining 24 or 16 ETH as well as putting
in another asset as collateral in form of their utility token called RPL.

To have some edge in thmatloce steps of what must be setup for your Rocketpool.


