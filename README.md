# Qtum Lightning Network Specifications (In-Progress)

## Abstract

The Lightning Network is a decentralized system for instant, high-volume micropayments that removes the risk of delegating custody of funds to trusted third parties.

Qtum Lightning is a protocol for making fast payments with QTUM using a network of channels, basically it is the same as [Bitcoin's](https://github.com/lightningnetwork/lightning-rfc).

## How it works

Funds are placed into a two-party, multisignature "channel" Qtum address. This channel is epresented as an entry on the Qtum public ledger. In order to spend funds from the channel, both parties must agree on the new balance. The current balance is stored as the most recent transaction signed by both parties, spending from the channel address. To make a payment, both parties sign a new exit transaction spending from the channel address. All old exit transactions are invalidated by doing so. 

## Specification

### Channels

Qtum Lightning works by establishing channels: two participants create a Lightning payment channel that contains some amount of QTUM (e.g., 0.1 QTUM) that they've locked up on the Qtum network. It is spendable only with both their signatures.

Initially they each hold a QTUM transaction that sends all the QTUM (e.g. 0.1 QTUM) back to one party. They can later sign a new Qtum transaction that splits these funds differently, e.g. 0.09 QTUM to one party, 0.01 QTUM to the other, and invalidate the previous Qtum transaction so it won't be spent.

### Conditional Payments

A Lightning channel only allows payment between two participants, but channels can be connected together to form a network that allows payments between all members of the network. This requires the technology of a conditional payment, which can be added to a channel, e.g. "you get 0.01 QTUM if you reveal the secret within 6 hours". Once the recipient presents the secret, that Qtum transaction is replaced with one lacking the conditional payment and adding the funds to that recipient's output.

### Forwarding

Such a conditional payment can be safely forwarded to another participant with a lower time limit, e.g. "you get 0.01 QTUM if you reveal the secret within 5 hours". This allows channels to be chained into a network without trusting the intermediaries.

### Network Topology

To make a payment, a participant needs to know what channels it can send through. Participants tell each other about channel and node creation, and updates.

### Payment Invoicing

A participant receives invoices that tell her what payments to make.

## Implementions
* [Qtum Eclair](https://github.com/qtumproject/lightning-demo)
* [qtum-lightning](https://github.com/qtumproject/qtum-lightning)

## Reference
* [Lightning Network Summary](https://lightning.network/lightning-network-summary.pdf)
* [Lightning Network Specifications](https://github.com/lightningnetwork/lightning-rfc/)

## [Start here for Table of Contents](00-introduction.md)
