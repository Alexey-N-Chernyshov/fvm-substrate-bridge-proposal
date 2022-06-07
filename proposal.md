# Open Grant Proposal: FVM <-> Substrate Bridge

**Name of Project:** FVM <-> Substrate Bridge

**Proposal Category:** Multiple categories, including: `app-dev`, `integration-adoption`, `research`

**Proposer:** `Alexey-N-Chernyshov`

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
- Additionally, Filecoin listed on [Polkaswap](https://polkaswap.io/) (Substrate-based DEX in
  the SORA network)

## Development Roadmap

<!-- Please break up your development work into a clear set of milestones. This section needs to be very detailed (will vary on the project, but aim for around 2 pages for this section). -->

<!-- For each milestone, please describe: -->
<!-- - The software functionality that we can expect after the completion of each milestone. This should be detailed enough that it can be used to ensure that the software meets the specification you outlined in the Deliverables. -->
<!-- - How many people will be working on each milestone and their roles -->
<!-- - The amount of funding required for each milestone -->
<!-- - How much time this milestone will take to achieve (using real dates) -->
### Milestone 1 - PoC prototype

Drafting architecture and building a prototype which transfers blocks between networks without finalization. Deploybg a local network with Filecoin and Substrate nodes.

* The stage includes following deliverables: relayer application, filecoin actor and substrate pallete.
* Definition of done: filecoin block headers are on substrate network and substrate transactions are on filecoin network. This stage doesn't imply any validation or finalization.
* Team: full team involved.
* Estimates: 
	* Relayer: 80 hours
	* Substrate pallet: 40 h
	* Filecoin actor: 40 h
	* Frontend: 60 h
	* Local network deployment: 20 h
	* Testing: 40 h
	* **Total**: 280 h
* Funding requested: $22400

### Milestone 2 - Finalization

Finalization on Filecoin and finalization on Substrate.

**Finalization of Substrate on Filecoin with [BEEFY protocol](https://github.com/paritytech/grandpa-bridge-gadget)** - implementation of effective finalisation of Substrate blocks on Filecoin network. The protocol was developed for Ethereum VM, but it can be adopted for FVM. In the meantime, when programmable FVM is missing, it can be substituted with a predefined builtin actor in FVM fork. Later, with FVM full release code of programmable actor will be compiled in FVM WASM.

**Finalization of Filecoin blocks on Substrate pallet** - Filecoin block validation - checks of miner pubkeys, power, election ticket and drand. Validation requires lookback state since miner can change public key or power, so state changes are needed. We can effectevly compute change diffs and build Merkle proofs with this changes.

* Definition of done: Filecoin blocks are finalized on Substrate and Substrate blocks are finalized on Filecoin chain in local network.
* Team: full team involved.
* Estimates: 
	* Substrate pallet finalization: 40 h
	* Filecoin actor: 80 h
	* Frontend: 60 h
	* Local network deployment: 20 h
	* Testing: 40 h
	* **Total**: 240 h
* Funding requested: $19200

### Milestone 3 - Replace hardcoded bridge actor with programmable

Since finalization on Filecoin is required and bridge actors cannot be deployed on Filecoin mainnet without the programmable FVM, project cannot be released before programmable FVM is launched. After the programmable FVM is released and Filecoin bridge actor can be adopted for programmbale FVM and deployed in Filecoin mainnet in testing mode.

* Definition of done: Filecoin bridge actor deployed on Filecoin testnet.
* Team: full team involved.
* Estimates: 
	* Filecoin actor: 40 h
	* Deployment: 40 h
	* Testing: 40 h
	* **Total**: 120 h
* Funding requested: $9600

### Milestone 4 - Intergration with Polkaswap

Development of economical model and integration into Sora ecosystem. Deployment of relayer application, integration of Substrate pallet into Soranet mainnet, deployment of actor bridge contract on Filecoin mainnet, integration into Polkaswap dApp interfaces.
* Team: N/A
* Estimates: N/A

### Milestone 5 - Maintenance 

Node and realy application maintenance, updates and security, further features that will come with development of FVM.
* Team: N/A
* Estimates: N/A

## Total Budget Requested

<!--Sum up the total requested budget across all milestones, and include that figure here. Also, please include a budget breakdown to specify how you are planning to spend these funds. -->
Total estimated: 640 h
Total funding requested: $51200

## Maintenance and Upgrade Plans

<!-- Specify your team's long-term plans to maintain this software and upgrade it over time. -->
Github repository will be open and will be maintained by team as a part of [Soramitsu organization](https://github.com/soramitsu).
Long term maintanance will be provided as FVM updates and new features. These include, but are not limited to:
- Filecoin finalization protocol updates to be used for transaction finalization on substrate,
- BEEFY protocol updates,
- Feature requests implementation.
With the development of FVM infrastracture, new application will arise on Filecoin and they can be integrated into Substrate based networks with our bridge.

# Team

## Team Members

* Alexey Chernyshov - [LinkedIn](https://www.linkedin.com/in/alexey-chernyshov-029b3912b/) [GitHub](https://github.com/Alexey-N-Chernyshov) - Tech lead, participated in Fuhon - Filecoin C++ implementation.
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
  * [Polkaswap](https://polkaswap.io) - DEX on SORA Network. The project was launched in april 2021.
  * [Hashi bridge](https://polkaswap.io/#/bridge) - Polkaswap bridge between Ethereum and Sora Substrate network. Allows transfer of ETH and ERC20 tokens. 
* [Fuhon](https://github.com/filecoin-project/cpp-filecoin) - C++ Filecoin node and miner implementation.

# Additional Information

<!-- Please include any additional information that you think would be useful in helping us to evaluate your proposal. -->
