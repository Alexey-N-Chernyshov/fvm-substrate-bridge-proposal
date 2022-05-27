# Open Grant Proposal: FVM <-> Substrate Bridge

**Name of Project:** FVM <-> Substrate Bridge

**Proposal Category:** Choose one of `app-dev`, `integration-adoption`, `metaverse` , `research`

**Proposer:** `replace with your GitHub username`

**(Optional) Technical Sponsor:** `If you have previously discussed this project with a member of the IPFS or Filecoin project teams and they have agreed to be a technical sponsor, include their name and/or github handle here`

**Do you agree to open source all work you do on behalf of this RFP and dual-license under MIT and APACHE2 licenses?: ** Please respond with either "Yes" or "No"

# Project Description

<!-- Please describe exactly what you are planning to build. Make sure to include the following: -->
<!-- - Start with the need or problem you are trying to solve with this project. -->
<!-- - Describe why your solution is going to adequately solve this problem. -->

<!-- This section should be 2-3 paragraphs long. -->
Blockchain interoperability is a cornerstone of Web 3.0. Introduction of FVM enables the bridge between Filecoin and Substrate [via Smart Contract](https://wiki.polkadot.network/docs/learn-bridges#via-smart-contracts). There are bridges for PoW (Bitcoin, Ethereum) and PoA blockchains for Substrate. Our proposal is to add PoST consensus as well. At first it allows to transfer FIL across blockchains, later with FVM contracts available it will be possible to delegete contract calls across chains.
More detailed [project specification](https://soramitsu.atlassian.net/wiki/spaces/FIL/pages/3651633155/FVM+-+Substrate+bridge).

## Value

<!-- Please describe in more detail why this proposal is valuable for the Filecoin ecosystem. Answer the following questions: -->
<!-- - What are the benefits to getting this right? -->
<!-- - What are the risks if you don't get it right? -->
<!-- - What are the risks that will make executing on this project difficult? -->

<!-- This section should be 1-3 paragraphs long. -->
Interoperability with Substrate. At first ability to transfer FIL across chains. Then, with programmable contract development on FVM, it will be possible to call contracts (transfer different tokens, add any logic: e.g. transfer market deals across chains).
Risks: bugs in protocol or implementation - funds lost. We can add emergency stop functionality.

PoST consensus based bridge for Substrate. Filecoin finalization on Substrate. This adds confidence for both chains.
Risks: bugs in protocol and implementation - once finalization is broken, contract will no longer syncronize. Need to redeploy and start from some block.

Risk: depends on programmable FVM and can be released only after contracts on Filecoin is available. We can fork FVM and hardcode bridge actor for local test network.

## Deliverables

<!-- Please describe in details what your final deliverable for this project will be. Include a specification of the project and what functionality the software will deliver when it is finished. -->
Decentrilized bridge between Filecoin and Substrate based blockchains.
- [Specification and documentation](https://soramitsu.atlassian.net/wiki/spaces/FIL/pages/3651633155/FVM+-+Substrate+bridge).
- Source code for Relayer daemon, Substrate pallete and Filecoin smart contracts.
- Filecoin listed on Polkaswap - TODO is it part of contract?

## Development Roadmap

<!-- Please break up your development work into a clear set of milestones. This section needs to be very detailed (will vary on the project, but aim for around 2 pages for this section). -->

<!-- For each milestone, please describe: -->
<!-- - The software functionality that we can expect after the completion of each milestone. This should be detailed enough that it can be used to ensure that the software meets the specification you outlined in the Deliverables. -->
<!-- - How many people will be working on each milestone and their roles -->
<!-- - The amount of funding required for each milestone -->
<!-- - How much time this milestone will take to achieve (using real dates) -->
1) PoC prototype - transfer blocks between networks without finalization. The stage includes following deliverables: relayer and substrate pallete. Definition of done: filecoin block headers are on substrate network and substrate transactions are on filecoin network. This stage doesn't implies any validation or finalization.
2) Finalization on substrate pallete. TODO describe tickets, blocks, miner signature validation, miner actor state diff, etc. May be broke down into more stages.
3) Fianlization on filecoin with BEEFY protocol. Programmable FVM with contracts is needed. For now we can substitute with predefined actor in FVM fork.
4) Replace hardcoded bridge actor with contract as soon as programmable FVM is released.
5) Intergration to Polkaswap, economical model.
6) Maintenance

## Total Budget Requested

<!--Sum up the total requested budget across all milestones, and include that figure here. Also, please include a budget breakdown to specify how you are planning to spend these funds. -->

## Maintenance and Upgrade Plans

<!-- Specify your team's long-term plans to maintain this software and upgrade it over time. -->
- FVM updates and new features.
- Filceoin finalization protocol updates to be used for transaction finalization on substrate.
- BEEFY protocol updates.
- Substrate protocol updates.
- Ready for feature requests.

# Team

## Team Members

<!-- - Team Member 1 -->
<!-- - Team Member 2 -->
<!-- - Team Member 3 -->
<!-- - ...

## Team Member LinkedIn Profiles

<!-- - Team Member 1 LinkedIn profile -->
<!-- - Team Member 2 LinkedIn profile -->
<!-- - Team Member 3 LinkedIn profile -->
<!-- - ...

## Team Website

<!-- Please link to your team's website here (make sure it's `https`) -->

## Relevant Experience

<!-- Please describe (in words) your team's relevant experience, and why you think you are the right team to build this project. You can cite your team's prior experience in similar domains, doing similar dev work, individual team members' backgrounds, etc. -->
* [Sora](TODO ADD LINK - private repository)
* [Hashi] (TODO ADD LINK - private repository) - Ethereum <-> Substrate bridge.
* [Fuhon](https://github.com/filecoin-project/cpp-filecoin) - C++ filecoin implementation

## Team code repositories

<!-- Please provide links to your team's prior code repos for similar or related projects. -->

# Additional Information

<!-- Please include any additional information that you think would be useful in helping us to evaluate your proposal. -->
