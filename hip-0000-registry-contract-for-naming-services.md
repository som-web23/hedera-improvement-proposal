---
hip: <HIP number (this is determined by the HIP editor)>
title: REGISTRY CONTRACT containing default naming structure format for HTLDs & SLDs ever minted over Hedera network
author: som-web23,somkirann@web23.io
working-group:somkirann@web23.io,rahul@web23.io,del@web23.io
type: Process
category: Service
needs-council-approval: No
status: Draft
created: 2022-07-29 
updated: 2022-07-29
---

## Table of Contents

1.	Abstract
2.	Motivation
3.	Rationale
4.	Specification
5.	Detailed note on the flow
6.	Reference Implementation
7.	Rejected Ideas
8.	Open Issues
9.	References
10.	Copyright/license 


## Abstract

Fostering overall growth of Hedera, minting of HTLDs (Hedera based -Top-Level-Domains) & SLDs (Second-Level-Domains) within Hedera are open. Any entity, person could mint of the HTLDs & SLDs which could eventually create issues like:
a.	Duplication of TLDs; .hbar (for example) by one contract & .hbarby the other contract
b.	Duplication of SLDs; for example, minted SLD user.tld by one contract & user.tld by the other contract
c.	Phishing attempts and inconvenience amongst the community owing to the duplication of names
d.	Challenges for the wallets providers to choose one contract over the other
e.	Complete chaos within the Hedera ecosystem

## Motivation

Hedera public ledger is comparatively new in comparison to other existing L1 chains. Hedera wins over the other chains through higher TPS leading to scalable solutions, negligible cost to execute the transactions to name a few. 
In the beginning, ICANN (The Internet Corporation for Assigned Names and Numbers) responsible for web2 domains had started with thirteen TLDs. Today, we have hundreds of gTLD (generic Top Level Domains) like .biz, .capital etc. At the same time, no two SLD within a TLD match or so to say, duplication of domain names within a TLDs does not exist across the globe although buying of domains is administered by hundreds of domain registrars, resellers etc.
Riding on the exceptional capabilities of Hedera & following the design philosophy of ICANN where no two SLDs are identical, proposed default structured format of TLDs & SLDs in the form of registry contract within Hedera would allow multi-parties to co-exist without leading to the confusion. 
This approach of proposed registry contract containing default structure format of TLDs & SLDs would possibly make Hedera a natural fit for decentralized ICANN allowing inter-chain dialogues too.

## Rationale

Taking the motivation, a further step ahead, it is proposed to allow multiple parties who could be resellers, companies to exist within the ecosystem of Hedera and allow community/users to mint/book domains ending in .hbar or any other TLD without the fear of duplication or phishing attempts.
Proposed Hedera centric registry contract that would also be extended to other inter-operable chains in the future would be able to accommodate multiple parties. Same registry contract would contain the real truth of mappings between Account IDs on the Mainnet & the corresponding human readable user-names. For example, john.hbar tied to 0.0.XXXXXXX

## Specification

Architecture of the proposed registry contract over Hedera would be, as follows:

![image](https://user-images.githubusercontent.com/97507177/181764916-06aaa2b2-bc65-4a95-94a9-fc40811853a4.png)
 
(Image source: https://drive.google.com/file/d/1e3yxtaY8glEiptSXlrNxznxfzTfk1SKr/view) 

## Detailed note on the flow

1. What is Registry Contract Suite?
Registry Contract Suite is a group of smart Contracts developed over Solidity. These smart contracts are intended to register HTLDs (Hedera Top-Level-Domains) and Second-Level-Domains (SLDs) in a hierarchical manner. Domains and HTLDs once registered could be queried and looked up to avoid duplication.
2. How does Registry Contract Suite Works?
Registry Contract Suite is an intelligent group of smart contract that maintains an alphabetical hierarchy to register HTLDs and is smart enough to create and store HTLDs in their respective Alphabetical Registry Component. 
	Once a HTLD is registered by the provider, an entry in respective alphabetical hierarchy smart contract is made. All further domains and subdomains under that hierarchy would be stored in that structure. So that for future, queries for that registered domain names or HTLD/s could be appropriately handled.
3. Who are providers and how could someone become a provider of domains/HTLDs?
Providers for Registry Contracts are the account addresses of Mainnet of entities who have access to register and update HTLD/s and domains. These providers could do a handful of operations and are provisioned to register a domain/HTLD. 
To become a provider, entities need to raise a request to the admin of Registry Contracts, who have the privilege to add addresses as providers for the Registry Smart Contract Suite. This would be done through a form accessible via the website of Web23 at web23.io 
4. Structure of Smart Contracts
The structure of smart contracts are as follows:
1.	AlphaInterface: This solidity file is an interface and it enables functions and abstract logic for the AToZRegistry Solidity Smart Contract. It enables functionalities such as register HTLD, activate TLD, etc.
2.	AlphaRegistry: This solidity file is responsible for doing all the jobs and is exposed for providers. It would internally call different smart contracts from the suite to get the job done. 
3.	UTools: This smart contract empowers the suite with a handful of utility functions like substring and all.
4.	AToZRegistry: This solidity file is responsible for creating a hierarchical alphabetical order of smart contracts
5. Exposed Functionalities and Functions (may not be in the order)
1.	isTLDAvailable method is used to check whether a particular TLD is available or not.
Inputs:- TLDName
Output:- True or False
Scenario :- This method is an external view function and will return Boolean and is used to Check whether a TLD is available or not
2.	isDomainAvailable method is used to check whether a particular Domain under a TLD is available or not.
Inputs:- DomainName, TLDName
Output:- True or False
Scenario :- This method is an external view function and is used to check whether a particular Domain under a TLD is available or not.
3.	registerTLD method is used to register TLD, only providers who are registered would be able to register a TLD
Inputs:- TldOwnerAddress, TLDName, ChainId, Expiry
Output:- True or False
Scenario :- This method is an external view function and is used to register TLD, only providers who are registered would be able to register a TLD
4.	registerDomain method is used to register domain, only providers who are registered would be able to register a domain
Inputs:- DomainOwnerAdress,TldOwnerAddress,TLDName,DomainName,ChainId,Expiry
Output:- True or False
Scenario :- This method is an external view function and is used to register Domain, only providers who are registered would be able to register a domain
5.	activateDomain method is used to activate Domain
Inputs:- DomainName, TLDName
Output:- True or False
Scenario :- This method is an external view function and is used to activate a Domain, only providers who are registered would be able to activate a domain.
6.	deactivateDomain method is used to deactivate a domain
Inputs:- DomainName, TLDName
Output:- True or False
Scenario :- This method is an external view function and is used to deactivate a Domain, only providers who are registered would be able to deactivate a domain.
7.	updateDomainExpiry method is used to update the Domain Expiry 
Inputs:- DomainName, TLDName, expiry
Output:- True or False
Scenario :- This method is an external view function and is used to update the Domain Expiry. The expiry should be a greater than the current date.
8.	deactivateTLD method is used to deactivate TLD
Inputs:- TLDName
Output:- True or False
Scenario :- This method is an external view function and is used to deactivate TLD so that no domain under that TLD could be booked.
9.	activateTLD method is used to activate TLD
Inputs:- TLDName
Output:- True or False
Scenario :- This method is an external view function and is used to activate TLD so that domain under that TLD could be booked.
10.	updateTLDExpiry method is used to update the TLD Expiry
Inputs:- TLDName,Expiry
Output:- True or False
Scenario :- This method is an external view function and is used to update TLD Expiry

11.	addProvider method is used to add Provider to the Registry, so that they could add TLDs and domains to the Registry.
Inputs:- ProviderWalletAddress
Output:- True or False
Scenario :- This method is an external view function and can be only executed by the administrator/Super Admin of the Smart Contract Suite  and is used to add Provider to the Registry , so that they can add TLDs and Domains to the Registry.
12.	getProvider method is used to get Provider by passing their provider ID
Inputs:- ProviderID
Output:- ProviderWalletAddress
Scenario :- Each time a provider is registered , a Provider ID would be allocated by the smart Contract suite and the provider Wallet Address will be mapped/associated with that Provider ID. This method on passing that provider ID, would return the Provider Wallet address of Mainnet.


## Reference Implementation

N/A

## Rejected Ideas

N/A

## Open Issues

N/A

## References

N/A

## Copyright/license

This document is licensed under the Apache License, Version 2.0 – see, https://www.apache.org/licenses/LICENSE-2.0)