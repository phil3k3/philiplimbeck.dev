---
title:  "Thoughts on account abstraction"
date:   2021-01-15 16:11:35 +0200
featured_image: '/images/demo/erc4337.png'
---

After attending quite a bit of Hackathons and Web3 conferences in this year I believe I got a good grasp
on how products are built in this sphere of software engineering. This article is made to sum-up the impressions
I got so far. I will refer to traditional engineering as Web2, although I am a bit reluctant to separate these
two worlds too much, more on that later.

* Ultra-fast pace

This relates to a few other points in this list. When you consider a typical Software Product to be built in
many months and years, things happen a lot faster in Web3. That is not only because there are many
amazing people building complex products, but also because you don't need to think about infrastructure so much.
For a dAPP, all you need is a set of Smart Contracts (your middleware) and fancy UI to be potentially successful.

* Hard to use for the everyday user on the street

Regardless or because of the fast-pace, many products are still built for crypto-enthusiasts in
mind. Although this follows what Sam Altman once said "Build what a few people love vs a lot of people like", it makes
products difficult to use by design, with UX tightly coupled to wallets and addresses and regular signing of transactions.
Additionally, since smart contracts dictate the data model, the UIs mostly tightly coupled to that as well

* Immature tooling

When you attend a hackathon with years of Web2 experience, the first thing which catches attention is
the lack of sophistication of tooling used. IDEs lack the support for Solidity/Vyper (talking about the EVM).
Although there are attempts to solve this (Tenderly), it doesn't give you full insight especially when Account Abstraction
is used. Basically it's like debugging an issue on a complex set of services without access to tracing or logging and no
good way to reproduce the issue, essentially flying blind.

* Lack of abstraction on low-level concepts

Normally frameworks building on top of low-level concepts should make things easier to implement and
improve the developer experience compared to using the low-level concepts. This is only partly true in Web3.
Oftentimes concepts from theoretical definitions (such as https://www.erc4337.io/) are 1:1 carried over
to an engineer who wants to use account abstraction. The base assumption is that you know all the theory behind
to actually use it. The equivalent would be to know the very internals of a database in order to actually use it.
The same goes for solving bugs, which still require deep understanding of how ERC-4337 works.

(Other example?)

* Too much noise (Quick hacks vs solid business models)

Related to the first point, means that a hackathon project is often seen as a business. It's usually not
a business involves a way to monetize the solution for the benefit of the users. A product trades functionality
for money. This is often missed out, as the products built in Hackathons provide functionality, they are often
not monetizable (aside from ads).

* Very market driven

Software, many domains where Web2 still dominates (banking, insurance, logistics)

* Solutions

Since I don't want to just complain, I want to offer some suggestions on how to improve the situation.
Of course this can't be done overnight, but with a few course corrections a lot less Web3 developers have to suffer.

- offer proper ways to debug EIP-4337 accounts (like Tenderly but for Bundlers)
- offer a proper tooling (we need IDEA for the EVM)
- slow down and introduce proper quality gates
- think about UX, and how to use Blockchain technologies more subtle, while keeping UX patterns known from Web2 (evolution instead of revolution)
