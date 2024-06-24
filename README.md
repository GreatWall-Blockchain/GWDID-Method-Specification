# GWDID-Method-Specification

## Abstract

[Great Wall Decentralized Identity (GWDID)](https://open.gwm.cn/Web3)  provides infrastructure for cross-system and cross-organization trusted digital identity and data exchange services. GWDID is based on the blockchain and provides a distributed mechanism for generating, holding and verifying identity identifiers DIDs (Decentralized Identifiers) and VCs (Verifiable Credentials) that carry identity data, enabling you to encrypt security, protect Data privacy and machine-verifiable third-party representation of various types of real-world identities and credentials on the Internet.

## Status of this document

This is a draft document and will be updated based on W3C.

## Introduction

[Great Wall Blockchain (Great Wall Chain) ](https://open.gwm.cn/Web3), It is a blockchain infrastructure used by Great Wall Motors to build technology, data, value, and industrial connectivity, aiming to lead the application and innovation of blockchain technology in the manufacturing industry, assist in the transformation and upgrading of traditional industries, and promote the deep integration of the real economy and the digital economy.

Great Wall Decentralized Identity (GWDID) is a set of digital identity basic services built on the [Great Wall Blockchain Service Platform (GWBaaS) ](https://open.gwm.cn/Web3) platform, which is full-featured and easy to use. GWDID provides a mechanism for the distributed generation and verification of globally unique identifiers (Decentralized Identifiers, DIDs) to identify various entities (people, institutions, objects, etc.). At the same time, various types of credentials (Verifiable Credentials, VCs) in the real society are expressed on the network by means of encryption security, privacy protection, and machine verification by a third party, so as to provide cross-organization and cross-regional trust between entities. Provides infrastructure for digital identities, digital credentials and data exchange.

<br />

### Features
#### - Distributed ID Registration

The distributed and multi-centralized ID registration mechanism based on blockchain gets rid of the dependence on the single-center ID registration in the traditional mode. It gives entities (people, institutions, things, etc.) the ability to independently control identity control, and provides basic functions such as entity identity creation, update, and verification.

#### - Distributed issuance/validation

Issuers of various identities/credentials issue data-bearing certificates to entities, and verifiers can verify the entity's identity control right on the blockchain, and further verify the authenticity, integrity, and authority of its identity/credential data.

#### - Trusted flow of data

Distributed interconnection between independent business systems is achieved through blockchain technology, and a trusted data flow channel is easily built to support the cross-system, cross-organization, and cross-region trusted flow of entity identity ID, entity credentials/identity data.

#### - Data Privacy Protection

The real identity and digital credentials of the entity are stored under the blockchain, and the entity can choose the storage location and manage or host it independently. Enabling entities to minimize or selectively disclose information to other entities.

#### - Portability and Interoperability

GWDID data can be ported to other platforms that follow the same specifications, and currently supports mainstream blockchain platforms such as Chainmaker, FISCO-BCOS, and Fabric. At the same time, GWDID provides standardized interfaces to support cross-chain and cross-platform interoperability.

<br />

### Current Application scenario
#### - Part trace
GWDID provides reliable digital capabilities for vehicle component traceability scenarios.

<br /><br />

## Great Wall Distributed Identity DID Method

The DID identifier of Great Wall Distributed Identity is defined as:  `gwm`. 
The DID method format of the `did:gwm` identification system is composed as the following format.

```bash
# gwdid
"did:gwm:" + gwm-router-id + ":" + gwm-identifier

# gwdid-router-id
less than 10 characters composed of lowercase letters and numbers

# gwdid-identifier
the prefix of gwm-identifier is 0x, followed by 40 characters composed of lowercase letters and numbers.
```
Example did of GWDID is 
`did:gwm:c767:0x1e7115081c178459be8d3844dd129b2234edc6be`

<br/>

## DID Document
Example did document of `did:gwm:c767:0x1e7115081c178459be8d3844dd129b2234edc6be` is

```json
{
  "@context": "https://w3id.org/did/v1",
  "id": "did:gwm:c767:0x1e7115081c178459be8d3844dd129b2234edc6be",
  "created": 1642992401,
  "updated": null,
  "verificationMethod": [
    {
      "id": "did:gwm:c767:0x1e7115081c178459be8d3844dd129b2234edc6be#keys-0",
      "type": "Secp256k1",
      "controller": "did:gwm:c767:0x1e7115081c178459be8d3844dd129b2234edc6be",
      "publicKey": "9140759724994454628181963565667341739731028461151630822625149865018431527829307192022895075113804689383949423804960687290646469426121233393934795192655714"
    }
  ],
  "authentication": [
       "did:gwm:c767:0x1e7115081c178459be8d3844dd129b2234edc6be#keys-0"
  ],
  "service": []
}
```

<br/> 

## CRUD Operations

did:gwm method(CRUD) are implemented by the Great Waall Distributed Identity (GWDID) service that generate the identifier and create DID documents to save in blockchain. 

To operate DID Documents, you should first execute prerequest which is creating an account of the [Great Wall Developer Platform](https://open.gwm.cn) service and GWDID service.

To improve interoperability, The identifier is calculated from the public key, then is published in decentralized blockchain.

### Prerequest

Create an account from open.gwm.cn at first, then operate following below:
1. create your owner DID service in the GWDID service
2. create a DID identifier on your owner DID service that created by the first step
3. DID CRUD can be operating on the console of the GWDID or called by Great Wall Developer Platform api

### Create

```bash
# endpoint
the great wall developer platform api url

# Input
{
    AK/SK, PUBICKEY, BLOCKCHAIN_ID
}

# Output
{transaction Id}
```

### Read

```bash
# endpoint
the great wall developer platform api url

# Input
{
    AK/SK, GWDID
}

# Output
{GWDID Document}
```

### Update

DID Document does not support update.

### Delete

```bash
# endpoint
the great wall developer platform api url
# Input
{
    AK/SK, TDID
}
# Output
{transaction Id}
```

<br/> 

## Security considerations

1. The CURD operation of GWDID on DID is exposed through Great Wall Developer Platform public cloud API. Users need to use AK/SK authentication to call the operation method of DID. AK/SK authentication helps to further improve the security of GWDID service.
2. GWDID uses the ChainMaker blockchain network as a verifiable data registry. ChainMaker  is a consortium chain with node access permission control. It is necessary to have a cloud account of a ChainMaker network node to call the operation method of DID.
3. The DID identifier of the GWDID service is generated by the operation of the public key, so it supports the user's own private key and private key escrow modes to register DID:
- The user automatically creates a public-private key pair through the system or imports the private key to register the DID, and the private key is hosted in the GWDID service
- The user enters the public key to create (agent mode) registration DID, and the private key needs to be held by the individual
4. The DID identifier of GWDID is calculated from the public key through the address conversion algorithm, similar to the account address of Ethereum.


<br/> 

## Privacy considerations

1. The DID document of GWDID does not contain the user's private data, but only saves the user's public key data. The DID entity (DID Subject) cannot be identified from the DID document.
2. The user issues a verifiable credential through GWDID to save his private information. The protection of user privacy depends on the security of VC.
3. The user's verifiable credentials are encrypted and stored in cloud storage through a symmetric encryption key such as SK or other negotiated passwords, and only the entity with the key can decrypt and view.
4. The user's verifiable credentials are stored under their cloud account and can only be read through AK/SK authentication on the cloud.

