---
title: 'Ethereum Validator'
subtitle: 'Running an validator with Rocketpool'
date: 2018-06-30 00:00:00
description: My approach of running an Ethereum validator with Rocketpool
featured_image: '/images/demo/rocketpool.png'
---

## Rocketpool ETH Validator

Rocket Pool is a decentralized protocol designed to facilitate Ethereum staking, particularly catering to users and node operators in the Ethereum blockchain ecosystem. 
It addresses the challenges associated with the high entry barrier for Ethereum staking, especially the requirement of holding 32 ETH to become a full validator on the Ethereum 2.0 network.

Since October 5th, 2023 I am running one of these validators to get familiar with maintaining a validator without providing the full 32 ETH.

To make sure I can easily recover from a full node loss, I have created an ansible playbook. 

These are my learnings and recommendations: 

* Don't run it on cloud instances (GCP/AWS) as they will significantly cut into your profit
* Don't run it locally, it gives you the piece of mind of not having to worry about backups, Internet connection and power supply
* Don't use a public IP, use tailscale to create a VPN to your instance
* Use Grafana + Alerts to get alerted when something fails
* Use a service like pingdom to get alerted when the whole instance becomes unavailable (impeding Grafana Alerts)
* Automate the creation of your box as much as possible to be able to resume where you left of and not losing many attestations
* Use beaconchain metrics, they also provide a Mobile App for checking out the metrics on the go

### Tools

<span class="tag-style-lang">Bash</span>
<span class="tag-style-infra">Ansible</span>

### Relevant links
- [Tailscale](https://tailscale.com/)
- [Rocket Pool](https://rocketpool.net/)
- [Beaconcha.in](https://beaconcha.in/)
- [Rocket Pool Support on GitHub](https://github.com/phil3k3/rocketpool-support)




