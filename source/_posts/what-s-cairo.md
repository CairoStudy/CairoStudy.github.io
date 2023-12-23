---
title: What's Cairo
date: 2022-12-01 15:02:46
tags:
---


### Background Introduction

- Built on cryptographic zero-knowledge proofs, zero-knowledge proofs can provide computational privacy. Simultaneously, in the blockchain ecosystem, they are also used to enhance scalability. It allows the verification of a computation that originally required 1000 seconds of computational resources to be validated with only 10 seconds of computation.
- Similar to the more well-known SNARK, STARK is also a zero-knowledge proof system. However, the current focus of STARK is on scalability rather than the privacy features commonly associated with zero-knowledge proofs. Currently, SNARK-based Rollup projects such as zkSync, Loopring, Aztec, and zkopru, with the exception of Aztec, use SNARK to enhance scalability. The information on these Rollups is publicly available, without privacy.
- StarkWare is currently the only development team based on STARK.
- Adding privacy protection to STARK is not expected to be too difficult, but StarkWare has not yet included this feature in its future plans.

### Introduction to Cairo

Billed as a Turing-complete zero-knowledge proof system language, Cairo may be challenging and unfamiliar for developers familiar with Solidity. Additionally, the library support is not yet sufficient, with the currently supported hash function being Pedersen, and the digital signature algorithm being ECDSA (compared to SNARK, EdDSA's performance is relatively poorer, so it is not supported).
However, Cairo is still in the early stages of development, and it is expected that the development experience will improve over time.
It's important to note that as a proof system, there are roles for both Prover and Verifier. The STARK Verifier is open source, but the Prover software is expected to be protected by a license. In general, the Prover software may not be used for commercial purposes unless the proof is uploaded to the official Verifier.
The letters in CAIRO represent:

- C: CPU
- AIR: Algebra Intermediate Representation
- O: One AIR (verifier smart contract) to rule them all
While details about C and AIR are skipped due to their focus on the details and experience of writing zero-knowledge proof applications, O: One AIR (verifier smart contract) to rule them all represents that any program written in Cairo can be verified using the same Verifier. Each application no longer needs to generate its own Verifier contract.

Developers do not need to run a trusted setup for their applications (as STARKs do not require it), and they do not need to worry about the Verifier's part. If you have developed applications based on SNARK, you will understand this better.

Finally, it should be mentioned that the first version of Cairo is designed to facilitate the migration of DApp computations off-chain for developers. Unlike Rollup, this off-chain will only have one DApp. The project maintains the state of its own DApp. (Rollup, on the other hand, has the operator maintaining the state of all DApps, so DApp developers do not need to worry about it.)

This may be a bit difficult to understand. If you are writing Solidity, imagine that today, when you declare a storage variable in a contract, you have to provide the merkle proof yourself to prove that the storage variable is indeed that value. This is what developers mean when they have to maintain the state themselves.

The second version of Cairo, on the other hand, is the Cairo used in StarkNet (the first and second versions are different compilers). This version of Cairo is used for DApps in Rollup development. Developers can declare variables in the contract, and the values of the variables do not need to be maintained by the developer; they can be assumed to exist directly.

**Note 1**: StarkWare does not like the term Rollup. They believe that the need for Data Availability is a spectrum: it doesn't necessarily have to send all data to L1; there are other ways to achieve different levels of Data Availability.

**Note 2**: The first and second versions are actually 0.0.1 and 0.0.2 in the official versions, and as of the current writing, the latest version is 0.0.2.

Official Website: https://www.cairo-lang.org

Developer Documentation: https://www.cairo-lang.org/docs/