# Escrow Journal

In the ever-evolving world of blockchain technology, the implementation of escrow systems has become a cornerstone in ensuring secure and trustless interactions with smart contract systems. This readme details some of the intricacies of creating escrow programs on Solana, contrasting the traditional 'vanilla' approach with the streamline process offered by the Anchor and based Anchor frameworks. 

## What Is An Escrow

An escrow is a digital mechanism where assets or tokens are held by a third party smart contract until predefined conditions are met. An escrow ensures security in transactions between parties who may or may not trust each other. Once pre-determined conditions are fulfilled, an escrow smart contract automatically executes the transfer of assets. Basic escrow contracts are the backbone of DeFi applications, and allow for the creation of a trustless environment for payments, trading, and multi-party agreements. In essence, escrow contracts are vital to almost every web3 application one interacts with. 

![Basic-bitcoin-escrow-layout-1024x614](https://github.com/jhuhnke/escrow-journal-jessicahuhnke-solanaq4/assets/91915469/01782548-d1bc-422e-acff-2d4baad17841)

## Vanilla Escrow 

As detailed in the [Paulx blog post](https://paulx.dev/blog/2021/01/14/programming-on-solana-an-introduction/#intro-motivation), creating an escrow on Solana without using a framework requires a deep understanding of Solana's low-level programming model. 

Say Alice (the payer) wishes to exchange Token X with Bob (the taker) for Token Y. Let's look at the accounts needed for an escrow contract to conduct such a transaction. Alice and Bob will both need a token account for both token X and token Y. This will be true in any escrow on Solana, as an associated token account is simply a program-derived account consisting of the wallet address itself and the token mint. If an associated token account for a given wallet address does not yet exist (in this case, Token Y for Alice and Token X for Bob), it may be created by anybody issuing the transaction. Because Solana programs are stateless, the vanilla escrow also requires the creation of an account to store the escrow state.    

![escrow-sketch-1 6df070a8](https://github.com/jhuhnke/escrow-journal-jessicahuhnke-solanaq4/assets/91915469/35f4abf0-5363-4514-b31e-2a5f35022227)

But this isn't all the accounts required to successfully broker this p2p token trade. Let's look at how Token X gets from the payer to the taker. Alice first transfers her token X to a temporary escrow account. While she is still the owner of this account, the token account authority is assigned to a PDA of the escrow program. Once the escrow program has validated the conditions of the escrow contract, the token X is transferred from the temporary escrow account to Bob's Token X account. 

The same account flow occurs to transfer Bob's token Y to Alice. Bob transfers Token Y to a temporary token account in which the authority is an escrow program PDA. Then Token Y is transferred from this temporary account to Alice's token Y account. 

So why are these temporary accounts necessary? To faciliate the transaction in a manner that requires minimal communication between users. Without these temporary accounts, the from address would have to sign the transaction initiated by the taker as well. This can result in frustration as takers will have to wait on the other party.     

![escrow_token_accounts_2 9291f5c8](https://github.com/jhuhnke/escrow-journal-jessicahuhnke-solanaq4/assets/91915469/c27fab0d-856a-4614-973a-02efabb903e3)



## Anchor Framework 

## Based Anchor Framework 
