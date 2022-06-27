# Open Grant Proposal: FVM <-> Substrate Bridge

**Name of Project:** FVM <-> Substrate Bridge

**Proposal Category:** Multiple categories, including: `app-dev`, `integration-adoption`, `research`

**Proposer:** `kamilsa`

**(Optional) Technical Sponsor:** N/A

**Do you agree to open source all work you do on behalf of this RFP and dual-license under MIT and APACHE2 licenses?**:  Yes

# Project Description

<!-- Please describe exactly what you are planning to build. Make sure to include the following: -->
<!-- - Start with the need or problem you are trying to solve with this project. -->
<!-- - Describe why your solution is going to adequately solve this problem. -->

<!-- This section should be 2-3 paragraphs long. -->
We are planning to build a bridge between Filecoin and Substrate-based networks that utilizes [FVM](https://filecoin.io/blog/posts/introducing-the-filecoin-virtual-machine/).


Initially, the bridge will allow FIL transfers across blockchains, then at a later point, with FVM contracts available, it will be possible to delegate contract calls across chains.


The idea behind the project is to build a bridge between Filecoin and Substrate-based networks using a combination of Filecoin FVM [smartcontracts](https://wiki.polkadot.network/docs/learn-bridges#via-smart-contracts), Substrate pallets, and external daemons called relayers. The component that resides on the target chain is able to follow the source chain consensus. Thus FVM contracts must be able to accept and verify Substrate headers. It will use the efficient [BEEFY finality protocol](https://github.com/paritytech/grandpa-bridge-gadget) for the non-substrate network. On the Substrate side, a new protocol for Filecoin message validation and finalization is being designed. It will use a partial Filecoin state for this purpose.

## Value

<!-- Please describe in more detail why this proposal is valuable for the Filecoin ecosystem. Answer the following questions: -->
<!-- - What are the benefits to getting this right? -->
<!-- - What are the risks if you don't get it right? -->
<!-- - What are the risks that will make executing on this project difficult? -->

<!-- This section should be 1-3 paragraphs long. -->
The value this proposal brings can be summarized as follows: Substrate Interoperability, which is a cornerstone of Web 3.0 will initially consist of the ability to transfer FIL between Filecoin and Substrate-based chains. Subsequently, with programmable contract development on FVM, it will be possible to call contracts (transfer different tokens, add any logic: e.g. transfer market deals) across chains which will increase the value that a bridge such as the one we are proposing can provide.
<!-- Possible risks to this include bugs in the protocol or implementation, which could result in funds lost. In order to mitigate this risk, it is possible to add emergency stop functionality. -->

<!-- PoST consensus based bridge for Substrate.
Filecoin finalization on
Substrate will provide confidence for both chains.
Possible risks to this include bugs in the protocol and
implementation, if finalization is broken the contract will no longer
synchronize. In order to solve this, it would be necessary to redeploy and start from some block.
 -->

A bridge to Substrate will allow FIL to take advantage of the growing DeFi ecosystem in the Polkadot and Kusama networks. Taking into account that the main delivery will be code for Substrate's Runtime pallets, any Substrate-based chain will be able to reuse this code to bring FIL to their network.

Overall risks depend on programmable FVM and can be released only after contracts on Filecoin are available. It is possible to fork FVM and the hardcode bridge actor to our local test network to fully determine them.

Another risk is the immaturity of FVM, which can lead to bugs and attacks on the protocol. This risk will be keept in mind during development and close attention will be paid during extensive testing on Filecoin and Substrate test networks.

## Deliverables

<!-- Please describe in details what your final deliverable for this project will be. Include a specification of the project and what functionality the software will deliver when it is finished. -->
Decentralized bridge infrastructure between Filecoin and Substrate-based blockchains.
- Specification and documentation.
- Source code for Relayer daemon, Substrate pallet and Filecoin smart contracts.
- Additionally, Filecoin is listed on a Test version of [Polkaswap](https://test.polkaswap.io/#/swap) (Substrate-based DEX in the SORA network) and will be listed eventually in the mainnet.

### Architecture
![image](https://github.com/Alexey-N-Chernyshov/fvm-substrate-bridge-proposal/raw/master/pics/bridge_diagram.svg)

Main components:
- Filecoin FVM contracts - The core bridge component on the Filecoin side. This locks and unlocks FIL during deposits and withdrawals, and validates and finalizes Substrate blocks on Filecoin using the BEEFY algorithm. We are planning to begin with a hardcoded bridge actor written in Rust, and then reuse the code for an FVM contract.
- Substrate pallet - The main bridge component on the Substrate-based chain. It is responsible for minting tokens during deposit to the Substrate chain and for burning them during withdrawal. It also validates and finalizes Filecoin messages on the Substrate chain. To achieve this, the pallet stores the partial Filecoin state needed for validation.
- Relayer - A daemon running off-chain that monitors both blockchains and relays messages across chains in both directions.

## Development Roadmap

<!-- Please break up your development work into a clear set of milestones. This section needs to be very detailed (will vary on the project, but aim for around 2 pages for this section). -->

<!-- For each milestone, please describe: -->
<!-- - The software functionality that we can expect after the completion of each milestone. This should be detailed enough that it can be used to ensure that the software meets the specification you outlined in the Deliverables. -->
<!-- - How many people will be working on each milestone and their roles -->
<!-- - The amount of funding required for each milestone -->
<!-- - How much time this milestone will take to achieve (using real dates) -->
### Milestone 1 - PoC prototype

Drafting architecture and building a prototype that transfers blocks between networks without finalization. Deploying a local network with Filecoin and Substrate nodes.

* This stage includes the following deliverables: Relayer application, Filecoin actor, and Substrate pallet.
* Definition of done: Filecoin block headers are on the Substrate network and Substrate transactions are on the Filecoin network. This stage doesn't imply any validation or finalization.
* Team: Alexey Chernyshov, Vladimir Stepanenko, Ruslan Tushov, Ivan Nikonorov.
* Estimates:
	* Relayer: 80 hours
	* Substrate pallet: 120 hrs
	* Filecoin actor: 120 hrs
	* Local network deployment: 20 hrs
	* Testing: 40 hrs
	* **Total**: 380 hrs
* Funding requested: $30400

### Milestone 2 - Finalization

Finalization on Filecoin and finalization on Substrate.

**Finalization of Substrate on Filecoin with the [BEEFY protocol](https://github.com/paritytech/grandpa-bridge-gadget)** - Implementation of effective finalization of Substrate blocks on the Filecoin network. The protocol was developed for Ethereum VM, but it can be adopted for FVM. In the meantime, when programmable FVM is missing, it can be substituted with a predefined built-in actor in the FVM fork. Later, with FVM full release, the code of the programmable actor will be compiled in the FVM WASM.

**Finalization of Filecoin blocks on Substrate pallet** - Filecoin block validation - This checks miner public keys, power, election ticket, and drand. Validation requires a lookback state since the miner can change their public key or power, so state changes are needed. We can effectively compute change diffs and build Merkle proofs with these changes.

* Definition of done: Filecoin blocks are finalized on Substrate and Substrate blocks are finalized on the Filecoin chain in a local network.
* Team: full team involvement.
* Estimates:
	* Substrate pallet finalization: 120 hrs
	* Filecoin actor: 120 hrs
	* Local network deployment: 40 hrs
	* Testing: 40 hrs
	* **Total**: 320 hrs
* Funding requested: $25600

### Milestone 3 - Replace hardcoded bridge actor with the programmable

Since finalization on Filecoin is required, and bridge actors cannot be deployed on Filecoin mainnet without the programmable FVM, the project cannot be released before the programmable FVM is launched. After the programmable FVM is released, the Filecoin bridge actor can be adopted for programmable FVM and deployed to the Filecoin mainnet in testing mode. We are planning to reuse the hardcoded Filecoin bridge actor code written in Rust in the previous stage and compile it into WASM programmable actor.

* Definition of done: Filecoin bridge actor deployed on Filecoin testnet.
* Team: Alexey Chernyshov, Vladimir Stepanenko, Ruslan Tushov, Ivan Nikonorov.
* Estimates:
	* Filecoin actor: 40 hrs
	* Deployment: 40 hrs
	* Testing: 40 hrs
	* **Total**: 120 hrs
* Funding requested: $9600

### Milestone 4 - Integration into Mainnet

Deployment of relayer application, integration of Substrate pallet into a Polkadot/Kusama parachain i.e. the Sora network, deployment of actor bridge contract on Filecoin mainnet.
* Team: full team involvement
* Estimates: TBD
* Funding requested: To be funded by other sources: Kusama treasury or by a Parachain's DAO


## Total Budget Requested

<!--Sum up the total requested budget across all milestones, and include that figure here. Also, please include a budget breakdown to specify how you are planning to spend these funds. -->
Total estimated: 660 hrs

Cost of infrastructure for testing: $2000

Total funding requested: $67600

## Maintenance and Upgrade Plans

<!-- Specify your team's long-term plans to maintain this software and upgrade it over time. -->



The Github repository will be open and maintained by a team from the [Soramitsu organization](https://github.com/soramitsu) for at least a year from the moment of launch.
Long-term maintenance will be provided as FVM updates and new features. These include, but are not limited to:
- Filecoin finalization protocol updates to be used for transaction finalization on Substrate,
- BEEFY protocol updates,
- Feature requests implementation.
With the development of FVM infrastructure, any new application developed on Filecoin can be integrated into Substrate-based networks with our bridge.

# Team

## Team Members

* Alexey Chernyshov - [GitHub](https://github.com/Alexey-N-Chernyshov) - Tech lead, participated in Fuhon - Filecoin C++ implementation.
* Vladimir Stepanenko - [GitHub](https://github.com/vovac12) - Substrate pallet developer.
* Ruslan Tushov - [GitHub](https://github.com/turuslan) - Cryptographer, Filecoin developer, participated in Fuhon - Filecoin C++ implementation.
* Stefan Popov - [GitHub](https://github.com/stefashkaa) - Frontend developer
* Ivan Nikonorov - [GitHub](https://github.com/ra9mls) - QA engineer

## Team Member LinkedIn Profiles

* [Alexey Chernyshov](https://www.linkedin.com/in/alexey-chernyshov-029b3912b)
* [Vladimir Stepanenko](https://www.linkedin.com/in/vovac12)
* [Ruslan Tushov](https://www.linkedin.com/in/ruslan-tushov-5b4581240)
* [Stefan Popov](https://www.linkedin.com/in/stefan-popov-072932170)
* [Ivan Nikonorov](https://www.linkedin.com/in/ivan-nikanorov-b6922b174)

## Team Website

<!-- Please link to your team's website here (make sure it's `https`) -->

[SORAMITSU](https://soramitsu.co.jp/)

## Relevant Experience

<!-- Please describe (in words) your team's relevant experience, and why you think you are the right team to build this project. You can cite your team's prior experience in similar domains, doing similar dev work, individual team members' backgrounds, etc. -->
SORAMITSU is a global technology company established in 2016 delivering blockchain-based solutions. Our most relevant projects are:
* The [Sora network](https://sora.org) - [Kusama parachain](https://parachains.info/details/sora#about). The SORA network is a Substrate-based network providing tools for decentralized applications including bridging tokens to other blockchains. [GitHub repositories](https://github.com/sora-xor). This project includes:
  * [Polkaswap](https://polkaswap.io) - An AMM DEX on the SORA network. The project was launched in April 2021.
  * [Hashi bridge](https://polkaswap.io/#/bridge) - A bridge between Ethereum and Sora Substrate network on Polkaswap. The Hashi bridge allows the transfer of ETH and ERC20 tokens from the Ethereum mainnet to the SORA network.
* [Fuhon](https://github.com/filecoin-project/cpp-filecoin) - A Filecoin node and miner implementation in C++.

# Additional Information

<!-- Please include any additional information that you think would be useful in helping us to evaluate your proposal. -->

SORAMITSU is a Japanese fintech company with expertise in developing blockchain-based solutions for digital asset and identity management. Our mission is to use blockchain to promote innovation to solve pressing societal challenges.

SORAMITSU is the developer of and major contributor to the open-source blockchain platform Hyperledger Iroha, which is tailored for enterprise and public-sector use. Part of the Linux Foundation's Hyperledger Project, the Iroha blockchain's flexible permissions system and scalable, performant architecture suit it to digital asset and identity management in high-traffic, multi-stakeholder environments.

Utilizing blockchain, SORAMITSU has developed a digital currency for the National Bank of Cambodia, an identity verification system prototype for Bank Central Asia in Indonesia, among others. We have also conducted proof-of-concept tests for several major Japanese enterprises, and are active contributors to open source projects, such as the SORA cryptoeconomic system, the Polkaswap DEX, and the DeFi wallet, Fearless Wallet.

Based on these experiences, SORAMITSU aims to deploy cutting-edge technology on a global level in order to expedite financial inclusion and health, mitigate economic inefficiencies, and contribute to economic growth and development
