| Client         | Compound Protocol Governance                    |
| :------------- | :---------------------------------------------- |
| Title          | Smart Contract Audit Report                     |
| Target         | GovernorBravoDelegateG2                         |
| Version        | 1.0                                             |
| Author         | [Samuel Dahunsi](https://github.com/psalmuel01) |
| Classification | Public                                          |
| Status         | Draft                                           |
| Date Created   | October 17, 2023                                |

## Table of contents

- <a href="#dsds"> 1. INTRODUCTION</a>

  - <a href="#Disclaim"> 1.1 Disclaimer</a>
  - <a href="#About"> 1.2 About Me </a>
  - <a href="#Skills"> 1.3 Skills</a>
  - <a href="#links"> 1.4 Link</a>
  - <a href="#Cpg"> 1.5 Compound Governance</a>
  - <a href="#Gbd"> 1.6 GovernorBravoDelegate</a>
  - <a href="#scope"> 1.7 Scope</a>
  - <a href="#roles"> 1.8 Roles</a>
  - <a href="#overview"> 1.9 System Overview</a>

- <a href="#review"> 2.0 CONTRACT REVIEW</a>
<!-- - <a href="#findings"> 3.0 FINDINGS</a>
  - <a href="#summary"> 3.1 Summary</a>
  - <a href="#Qanalysis"> 3.2 Qualitative Analysis</a>
  - <a href="#keyF"> 3.3 Key Findings</a>
- <a href="#Dresult"> 4.0 DETAILED RESULT</a>
  - <a href="#dr1"> 4.1 Missing address(0) check in constructor</a>
  - <a href="#dr2"> 4.2 Function claim() reverts without a specific pointer</a>
  - <a href="#dr3"> 4.3 BetBull/ BetBear Epoch errors could be more specific</a>
  - <a href="#dr4"> 4.4 Redundant State/ code removal in BetBear/BetBull</a>
  - <a href="#dr5"> 4.5 Redundant State/ code removal in Claim() function </a>
- <a href="#conclusion"> 5.0 CONCLUSION</a> -->

<h2 id="dsds">1.0 INTRODUCTION </h2>

### <h3 id="Disclaim">1.1 Disclaimer <h3>

My audit of this smart contract is based on the provided information and my expertise in the field. It's essential to clarify that this audit does not serve as a guarantee for the security or functionality of the smart contract, nor does it eliminate all potential risks. Investing in cryptocurrencies involves inherent risks, and I cannot be held accountable for any financial losses that may arise from investing in this smart contract or engaging in cryptocurrency-related activities. Investors are strongly advised to conduct their own research and due diligence before making any investment decisions.

### <h3 id="About">1.2 🚀 About Me <h3>

Hello, I'm Samuel Dahunsi, a Smart Contract Developer. Currently, I'm gaining experience through an internship at Web3bridge, where I am focused on advancing my knowledge and skills in blockchain development.

As a developer, I have a strong passion for creating smart contracts that prioritize security and efficiency, with the potential to revolutionize our interactions with technology. I am dedicated to continuously learning and exploring new technologies to stay at the forefront of this rapidly evolving field.

### <h3 id="Skills">1.3 🛠 Skills <h3>

Solidity, Diamond Standard, Foundry, Hardhat, Wagmi, Ethers.js, React, Javascript, HTML, CSS ...

### <h3 id="links">1.4 🔗 Links <h3>

[![portfolio](https://img.shields.io/badge/my_portfolio-000?style=for-the-badge&logo=ko-fi&logoColor=white)](https://portfolio-sammy.vercel.app/)
[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/samuel-dahunsi/)
[![twitter](https://img.shields.io/badge/twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/psalmuel1st)

### <h3 id="Cpg">1.5 Compound Governance<h3>

Compound protocol is a decentralized protocol which establishes money markets with
algorithmically set interest rates based on supply and demand, allowing users to frictionlessly
exchange the time value of Ethereum assets.

Compound Governance refers to the decentralized governance system employed by Compound Finance, a prominent decentralized finance (DeFi) protocol. Compound Finance is built on the Ethereum blockchain and provides lending and borrowing services for various cryptocurrencies.

The governance mechanism allows token holders to participate in the decision-making process regarding the protocol's development, changes, and upgrades. The native token of Compound, COMP, plays a central role in this governance system.

#### Key aspects of Compound Governance include:

1. COMP Token: COMP is the governance token of the Compound protocol. Holders of COMP can propose, discuss, and vote on changes to the protocol. The number of COMP tokens held by an individual determines their voting power.

2. Proposal Creation: Any COMP holder can create a proposal to suggest changes to the protocol. Proposals can range from protocol parameter adjustments to adding new features.

3. Voting: COMP holders can vote "for," "against," or "abstain" on proposed changes. The voting power is directly proportional to the number of COMP tokens held by the voter.

4. Quorum and Approval: Proposals must meet a minimum quorum (a minimum number of votes) to be considered valid. Additionally, they require a certain percentage of "for" votes to be approved.

5. Execution of Proposals: Once a proposal is approved, it can be executed, resulting in the implementation of the proposed changes.

Compound Governance empowers the community to collectively govern the protocol, ensuring a decentralized and inclusive decision-making process for the platform's evolution and improvements.

### <h3 id="Gbd">1.6 GovernorBravoDelegate<h3>

The GovernorBravoDelegate contract is an implementation of the GovernorBravoDelegateStorageV2 and GovernorBravoEvents contracts, which are part of the governance system of the Compound protocol. The purpose of this contract is to allow token holders to propose and vote on changes to the protocol, such as adding new assets to the protocol or changing the interest rates of existing assets. The contract defines various constants and functions that set the parameters for the governance process, such as the minimum and maximum voting periods, the quorum votes required for a proposal to succeed, and the maximum number of actions that can be included in a proposal. Overall, the GovernorBravoDelegate contract plays a critical role in the decentralized governance of the Compound protocol.

### <h3 id="scope">1.7 Scope <h3>

_(**Table: 1.7**: Compound GovernorBravoDelegate G2 Audit Scope)_
| Files in scope | SLOC |
| :-------- | :------- |
| Contracts: 1 | |
| `CompoundBravoDelegateG2.sol` | `432` |
| | |
| Imports: 7 | |
| `GovernorBravoEvents.sol` | `67` |
| `GovernorBravoDelegateStorageV2.sol` | `7` |
| `GovernorBravoDelegateStorageV1.sol` | `60` |
| `GovernorBravoDelegatorStorage.sol` | `10` |
| `TimelockInterface.sol` | `33` |
| `CompInterface.sol` | `6` |
| `GovernorAlpha.sol` | `4` |

### <h3 id="roles"> 1.8 Roles <h3>

- #### Operator

  - Initialize contract.
  - Propose a proposal.
  - Queue a proposal.
  - Execute proposal.
  - Cancel proposal.
  - Vote on proposal.
  - Whitelist a user.
  - Set admin.

- #### Admin

  - Set voting delay.
  - Set voting period.
  - Set proposal threshold.
  - Whitelist user.
  - Set admin.

- #### User

  - Call the propose function to propose a proposal.
  - Call the queue function to queue a proposal.
  - Call the execute function to execute a proposal.
  - Call the cancel function to cancel a proposal.
  - Call the vote function to vote on a proposal.

### <h3 id="overview"> 1.9 System Overview <h3>

- #### GovernorBravoDelegateStorageV2.sol

  This contract is designed for decentralized governance using a voting system, allowing users to propose, vote on, and execute actions. It also includes functionality for whitelisting and administration. It implements safety checks and ensures proper governance mechanisms are in place to manage proposals and voting.

- #### GovernorBravoEvents.sol

  This contract defines events that are emitted during various actions in the governance system, such as proposal creation, voting, proposal cancellation, and more.

- #### GovernorBravoDelegateStorage.sol

  This contract defines the storage variables used in the governance system, including the administrator, pending administrator, and the active implementation (logic) of the Governor.

- #### GovernorBravoDelegateStorageV1:

  This contract extends GovernorBravoDelegatorStorage and adds more storage variables related to the governance parameters and proposals. It includes variables like voting delay, voting period, proposal threshold, proposal count, and more.

- #### GovernorBravoDelegateStorageV2:

  This contract extends GovernorBravoDelegateStorageV1 and adds additional storage variables related to whitelist management. It includes whitelist account expiration timestamps and the whitelist guardian's address.

  - #### TimelockInterface

  This interface defines the functions that can be called on the Timelock contract. The delay function returns the delay period specified in the Timelock contract. The GRACE_PERIOD function returns the grace period specified in the Timelock contract. The acceptAdmin function is used to accept the admin role for the Timelock contract. The queuedTransactions function is used to check whether a transaction with the specified hash has been queued in the Timelock contract. The queueTransaction function is used to add a transaction to the queue in the Timelock contract. The cancelTransaction function is used to cancel a transaction that has been queued in the Timelock contract. The executeTransaction function is used to execute a transaction that has been queued in the Timelock contract.

- #### CompInterface:

  This interface defines the functions that can be called on the COMP token contract. The getPriorVotes function is used to get the number of votes that an account had at a specific block number. This function is used in the governance system of the Compound protocol to determine the voting power of token holders.

- #### GovernorAlpha:

  This interface defines the function that can be called on the GovernorAlpha contract. The proposalCount function returns the total number of proposals (state variable) that have been created in the governance system of the Compound protocol. This function is used to keep track of the number of proposals.

## <h2 id="review"> 2.0 CONTRACT REVIEW <h2>

The contract contains the following state constant variables:

```bash
    string public constant name = "Compound Governor Bravo";
```

This line defines a public constant string variable named name and assigns it the value "Compound Governor Bravo". This variable is used to store the name of the Governor Bravo contract.

```bash
    uint public constant MIN_PROPOSAL_THRESHOLD = 50000e18; // 50,000 Comp
```

This line defines a public constant unsigned integer variable named MIN_PROPOSAL_THRESHOLD and assigns it the value 50000e18. This variable is used to store the minimum amount of COMP tokens that a proposer must hold in order to create a proposal.

```bash
    uint public constant MAX_PROPOSAL_THRESHOLD = 100000e18; //100,000 Comp
```

This line defines a public constant unsigned integer variable named MIN_PROPOSAL_THRESHOLD and assigns it the value 50000e18. This variable is used to store the minimum amount of COMP tokens that a proposer must hold in order to create a proposal.

```bash
    uint public constant MIN_VOTING_PERIOD = 5760; // About 24 hours
```

This line defines a public constant variable called MIN_VOTING_PERIOD with a value of 5760. This value represents the minimum voting period that can be set in the governance system of the Compound protocol.

```bash
    uint public constant MAX_VOTING_PERIOD = 80640; // About 2 weeks
```

This line defines a public constant variable called MAX_VOTING_PERIOD with a value of 80640. This value represents the maximum voting period that can be set in the governance system of the Compound protocol.

```bash
    uint public constant MIN_VOTING_DELAY = 1;
```

This line defines a public constant variable called MIN_VOTING_DELAY with a value of 1. This value represents the minimum voting delay that can be set in the governance system of the Compound protocol.

```bash
    uint public constant MAX_VOTING_DELAY = 40320; // About 1 week
```

This line defines a public constant variable called MAX_VOTING_DELAY with a value of 40320. This value represents the maximum voting delay that can be set in the governance system of the Compound protocol.

```bash
    uint public constant quorumVotes = 400000e18; // 400,000 = 4% of Comp
```

This line defines a public constant variable called quorumVotes with a value of 400,000 multiplied by 10^18. This value represents the number of votes required for a quorum to be reached and for a vote to succeed in the governance system of the Compound protocol.

```bash
    uint public constant proposalMaxOperations = 10; // 10 actions
```

This line defines a public constant variable called proposalMaxOperations with a value of 10. This value represents the maximum number of actions that can be included in a proposal in the governance system of the Compound protocol.

```bash
    bytes32 public constant DOMAIN_TYPEHASH = keccak256("EIP712Domain(string name,uint256 chainId,address verifyingContract)");
```

This line defines a public constant variable called DOMAIN_TYPEHASH with a value generated by hashing the string "EIP712Domain(string name,uint256 chainId,address verifyingContract)" using the keccak256 hash function. This value represents the type hash of the contract's domain for use in EIP-712 signatures.

```bash
    bytes32 public constant BALLOT_TYPEHASH = keccak256("Ballot(uint256 proposalId,uint8 support)");
```

This line defines a public constant variable called BALLOT_TYPEHASH with a value generated by hashing the string "Ballot(uint256 proposalId,uint8 support)" using the keccak256 hash function. This value represents the type hash of the ballot struct used by the contract for use in EIP-712 signatures.

The following functions are part of the compound governance contract and are all carefully and thoroghly intertwined for optimum performance.

### 2.1 initialize():

This function initializes the contract. It is a public function with five input parameters: timelock*, comp address*, votingPeriod*, votingDelay*, and proposalThreshold*. This function is used to initialize the contract during the delegator constructor. It includes checks to ensure the timelock address is not already set, the caller of the function is the admin address, the timelock* and comp* address are not the null address, the votingPeriod*, votingDelay* and proposalThreshold* parameters are within the valid range of values defined by their min and max constants. It then sets the timelock, comp, votingPeriod, votingDelay, and proposalThreshold variables to the values passed in as arguments to the function

### 2.2 propose():

This function creates a new proposal. It is a public function with three input parameters: targets (an array of target addresses), values (an array of Eth values), signatures (an array of function signatures), calldatas (array) and description of the proposal This function is used to create a new proposal. It includes checks to ensure the Governor Bravo contract is active, the proposer has enough voting power to create a proposal except if whitelisted, the length of the targets, values, signatures, and calldatas arrays are equal. It also ensures the length of the targets array is not empty and not greater than the maximum number of operations allowed in a proposal. After it calculates the start and end blocks of the voting period for the new proposal, based on the current block number, the voting delay, and the voting period, the function then checks whether the proposer has an active or pending proposal, creates a new proposal and set the state variable proposalCount to the proposalCount + 1. Then an event is emitted to signal the creation of the new proposal.

#### 2.3 queue():

This function is used to add a proposal to the queue in the Timelock contract. The function takes a single argument, proposalId, which is the ID of the proposal to be queued. The function checks that the proposal with the specified proposalId is in the Succeeded state, retrieves the proposal from the proposals mapping, calculates the earliest time at which the proposal can be executed, and loops through the targets, values, signatures, and calldatas arrays of the proposal to add each action to the queue in the Timelock contract. Finally, the eta value is stored in the eta field of the proposal, and a ProposalQueued event is emitted with the proposalId and eta values as arguments.
