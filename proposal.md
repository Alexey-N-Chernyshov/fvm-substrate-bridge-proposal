# Open Grant Proposal: FVM <-> Substrate Bridge

**Name of Project:** FVM <-> Substrate Bridge

**Proposal Category:** Multiple categories, including: `app-dev`, `integration-adoption`, `research`

**Proposer:** `replace with your GitHub username`

**(Optional) Technical Sponsor:** N/A

**Do you agree to open source all work you do on behalf of this RFP and dual-license under MIT and APACHE2 licenses?**:  Yes

# Project Description

<!-- Please describe exactly what you are planning to build. Make sure to include the following: -->
<!-- - Start with the need or problem you are trying to solve with this project. -->
<!-- - Describe why your solution is going to adequately solve this problem. -->

<!-- This section should be 2-3 paragraphs long. -->
Blockchain interoperability is a cornerstone of Web 3.0. The
introduction of the FVM enables the implementation of a bridge between
Filecoin and Substrate [via Smart
Contracts](https://wiki.polkadot.network/docs/learn-bridges#via-smart-contracts). There
are existing bridges for PoW (Bitcoin, Ethereum) and PoA blockchains
to Substrate. Our proposal is to add PoST consensus as well. At
first, this bridge will allow FIL transfers across blockchains, at a
later point, with FVM contracts available, it will be possible to delegete contract calls across chains.
More detailed [project specification is available here](https://soramitsu.atlassian.net/wiki/spaces/FIL/pages/3651633155/FVM+-+Substrate+bridge).

## Value

<!-- Please describe in more detail why this proposal is valuable for the Filecoin ecosystem. Answer the following questions: -->
<!-- - What are the benefits to getting this right? -->
<!-- - What are the risks if you don't get it right? -->
<!-- - What are the risks that will make executing on this project difficult? -->

<!-- This section should be 1-3 paragraphs long. -->
The value this proposal brings can be summarised as follows: 
Substrate Interoperability. This will initially consist of the ability
to transfer FIL across chains. Subsequently, with programmable
contract development on FVM, it will be possible to call contracts
(transfer different tokens, add any logic: e.g. transfer market deals
across chains) across chains.
Possible risks to this include bugs in the protocol or
implementation, which could result in funds lost. In order to mitigate
this risk, it is possible to add emergency stop functionality.

PoST consensus based bridge for Substrate. Filecoin finalization on
Substrate will provide confidence for both chains.
Possible risks to this include bugs in the protocol and
implementation, if finalization is broken the contract will no longer
syncronize. In order to solve this, it would be necessary to redeploy and start from some block.

Overall risks depend on programmable FVM, and can be released only
after contracts on Filecoin are available. It is possible to fork FVM
and the hardcode bridge actor to our local test network to fully
determine them.

## Deliverables

<!-- Please describe in details what your final deliverable for this project will be. Include a specification of the project and what functionality the software will deliver when it is finished. -->
Decentralized bridge infrastructure between Filecoin and Substrate based blockchains.
- [Specification and documentation](https://soramitsu.atlassian.net/wiki/spaces/FIL/pages/3651633155/FVM+-+Substrate+bridge).
- Source code for Relayer daemon, Substrate pallet and Filecoin smart contracts.
- Additionally, Filecoin listed on Polkaswap (Substrate-based DEX in
  the SORA network)

## Development Roadmap

<!-- Please break up your development work into a clear set of milestones. This section needs to be very detailed (will vary on the project, but aim for around 2 pages for this section). -->

<!-- For each milestone, please describe: -->
<!-- - The software functionality that we can expect after the completion of each milestone. This should be detailed enough that it can be used to ensure that the software meets the specification you outlined in the Deliverables. -->
<!-- - How many people will be working on each milestone and their roles -->
<!-- - The amount of funding required for each milestone -->
<!-- - How much time this milestone will take to achieve (using real dates) -->
1) **PoC prototype** - transfer blocks between networks without
finalization. 
	* The stage includes following deliverables: relayer and substrate pallete. 
	* Definition of done: filecoin block headers are on substrate network and substrate transactions are on filecoin network. This stage doesn't imply any validation or finalization.
2) **Finalization on Substrate pallet**; TODO describe tickets, blocks, miner signature validation, miner actor state diff, etc. May be broken down into more stages.
3) **Finalization on Filecoin with BEEFY protocol**; Programmable FVM with
contracts is needed. In the meantime, it can be substituted with a predefined actor in FVM fork.
4) **Replace hardcoded bridge actor** with contract as soon as programmable FVM is released.
5) **Intergration to Polkaswap**, economical model.
6) **Maintenance**

## Total Budget Requested

<!--Sum up the total requested budget across all milestones, and include that figure here. Also, please include a budget breakdown to specify how you are planning to spend these funds. -->

## Maintenance and Upgrade Plans

<!-- Specify your team's long-term plans to maintain this software and upgrade it over time. -->
Long term maintanance will be provided as FVM updates and new
features. These include, but are not limited to;
- Filecoin finalization protocol updates to be used for transaction finalization on substrate.
- BEEFY protocol updates.
- Substrate protocol updates.
- Feature request implementations.

# Team

## Team Members

* Alexey Chernyshov - [LinkedIn](https://www.linkedin.com/in/alexey-chernyshov-029b3912b/) [GitHub](https://github.com/Alexey-N-Chernyshov) - Tech lead,participated in Fuhon - Filecoin C++ implementation.
* Vladimir Stepanenko - [LinkedIn](https://www.linkedin.com/in/vovac12/) [GitHub](https://github.com/vovac12) - Substrate pallet developer.
* Ruslan Tushov - [LinkedIn](https://www.linkedin.com/in/ruslan-tushov-5b4581240/) [GitHub](https://github.com/turuslan) - Cryptographer, filecoin developer, participated in Fuhon - Filecoin C++ implementation.
* Stefan Popov - [LinkedIn](https://www.linkedin.com/in/stefan-popov-072932170/) [GitHub](https://github.com/stefashkaa) - Frontend developer
* Ivan Nikonorov - [LinkedIn](https://www.linkedin.com/in/ivan-nikanorov-b6922b174/) [GitHub](https://github.com/ra9mls) - QA engineer

## Team Website

<!-- Please link to your team's website here (make sure it's `https`) -->

[SORAMITSU](https://soramitsu.co.jp/)

## Relevant Experience

<!-- Please describe (in words) your team's relevant experience, and why you think you are the right team to build this project. You can cite your team's prior experience in similar domains, doing similar dev work, individual team members' backgrounds, etc. -->
SORAMITSU is a global technology company was established in 2016 and delivers blockchain-based solutions. Our most relevant projects are:
* [Sora Network](https://sora.org) - [Kusama parachain](https://parachains.info/details/sora#about). The SORA Network is a Substrate network providing tools for decentralized applications including bridging tokens to other blockchains. [GitHub repositories](https://github.com/sora-xor). The project includes:
  * [Polkaswap](https://polkaswap.io) - DEX on SORA Network. The project was launched in may 2021.
  * [Hashi bridge](https://polkaswap.io/#/bridge) - Polkaswap bridge between Ethereum and Sora Substrate network. Allows transfer of ETH and ERC20 tokens. 
* [Fuhon](https://github.com/filecoin-project/cpp-filecoin) - C++ Filecoin node and miner implementation.

# Additional Information

<!-- Please include any additional information that you think would be useful in helping us to evaluate your proposal. -->
