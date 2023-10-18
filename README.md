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

- <a href="#intro"> 1. INTRODUCTION</a>

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

- <a href="#findings"> 3.0 FINDINGS</a>

  - <a href="#Qanalysis"> 3.1 Qualitative Analysis</a>
  - <a href="#summary"> 3.2 Summarys</a>
  - <a href="#recom"> 3.2 Recommendations</a>

- <a href="#conclusion"> 4.0 CONCLUSION</a>

<h2 id="intro">1.0 INTRODUCTION </h2>

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

```bash
  function initialize(address timelock_, address comp_, uint votingPeriod_, uint votingDelay_, uint proposalThreshold_) public {
        require(address(timelock) == address(0), "GovernorBravo::initialize: can only initialize once");
        require(msg.sender == admin, "GovernorBravo::initialize: admin only");
        require(timelock_ != address(0), "GovernorBravo::initialize: invalid timelock address");
        require(comp_ != address(0), "GovernorBravo::initialize: invalid comp address");
        require(votingPeriod_ >= MIN_VOTING_PERIOD && votingPeriod_ <= MAX_VOTING_PERIOD, "GovernorBravo::initialize: invalid voting period");
        require(votingDelay_ >= MIN_VOTING_DELAY && votingDelay_ <= MAX_VOTING_DELAY, "GovernorBravo::initialize: invalid voting delay");
        require(proposalThreshold_ >= MIN_PROPOSAL_THRESHOLD && proposalThreshold_ <= MAX_PROPOSAL_THRESHOLD, "GovernorBravo::initialize: invalid proposal threshold");

        timelock = TimelockInterface(timelock_);
        comp = CompInterface(comp_);
        votingPeriod = votingPeriod_;
        votingDelay = votingDelay_;
        proposalThreshold = proposalThreshold_;
    }
```

This function initializes the contract. It is a public function with five input parameters: timelock*, comp address*, votingPeriod*, votingDelay*, and proposalThreshold\*. This function is used to initialize the contract during the delegator constructor.

It includes checks to ensure the timelock address is not already set, the caller of the function is the admin address, the timelock* and comp* address are not the null address, the votingPeriod*, votingDelay* and proposalThreshold\* parameters are within the valid range of values defined by their min and max constants.

It then sets the timelock, comp, votingPeriod, votingDelay, and proposalThreshold variables to the values passed in as arguments to the function

### 2.2 propose():

```bash
  function propose(address[] memory targets, uint[] memory values, string[] memory signatures, bytes[] memory calldatas, string memory description) public returns (uint) {
        // Reject proposals before initiating as Governor
        require(initialProposalId != 0, "GovernorBravo::propose: Governor Bravo not active");
        // Allow addresses above proposal threshold and whitelisted addresses to propose
        require(comp.getPriorVotes(msg.sender, sub256(block.number, 1)) > proposalThreshold || isWhitelisted(msg.sender), "GovernorBravo::propose: proposer votes below proposal threshold");
        require(targets.length == values.length && targets.length == signatures.length && targets.length == calldatas.length, "GovernorBravo::propose: proposal function information arity mismatch");
        require(targets.length != 0, "GovernorBravo::propose: must provide actions");
        require(targets.length <= proposalMaxOperations, "GovernorBravo::propose: too many actions");

        uint latestProposalId = latestProposalIds[msg.sender];
        if (latestProposalId != 0) {
          ProposalState proposersLatestProposalState = state(latestProposalId);
          require(proposersLatestProposalState != ProposalState.Active, "GovernorBravo::propose: one live proposal per proposer, found an already active proposal");
          require(proposersLatestProposalState != ProposalState.Pending, "GovernorBravo::propose: one live proposal per proposer, found an already pending proposal");
        }

        uint startBlock = add256(block.number, votingDelay);
        uint endBlock = add256(startBlock, votingPeriod);

        proposalCount++;
        Proposal memory newProposal = Proposal({
            id: proposalCount,
            proposer: msg.sender,
            eta: 0,
            targets: targets,
            values: values,
            signatures: signatures,
            calldatas: calldatas,
            startBlock: startBlock,
            endBlock: endBlock,
            forVotes: 0,
            againstVotes: 0,
            abstainVotes: 0,
            canceled: false,
            executed: false
        });

        proposals[newProposal.id] = newProposal;
        latestProposalIds[newProposal.proposer] = newProposal.id;

        emit ProposalCreated(newProposal.id, msg.sender, targets, values, signatures, calldatas, startBlock, endBlock, description);
        return newProposal.id;
    }
```

This function creates a new proposal. It is a public function with three input parameters: targets (an array of target addresses), values (an array of Eth values), signatures (an array of function signatures), calldatas (array) and description of the proposal.

It includes checks to ensure the Governor Bravo contract is active, the proposer has enough voting power to create a proposal except if whitelisted, the length of the targets, values, signatures, and calldatas arrays are equal. It also ensures the length of the targets array is not empty and not greater than the maximum number of operations allowed in a proposal.

After it calculates the start and end blocks of the voting period for the new proposal, based on the current block number, the voting delay, and the voting period, the function then checks whether the proposer has an active or pending proposal, creates a new proposal and set the state variable proposalCount to the proposalCount + 1. Then an event is emitted to signal the creation of the new proposal.

#### 2.3 queue():

```bash
      function queue(uint proposalId) external {
        require(state(proposalId) == ProposalState.Succeeded, "GovernorBravo::queue: proposal can only be queued if it is succeeded");
        Proposal storage proposal = proposals[proposalId];
        uint eta = add256(block.timestamp, timelock.delay());
        for (uint i = 0; i < proposal.targets.length; i++) {
            queueOrRevertInternal(proposal.targets[i], proposal.values[i], proposal.signatures[i], proposal.calldatas[i], eta);
        }
        proposal.eta = eta;
        emit ProposalQueued(proposalId, eta);
    }
```

This is an external function used to add a proposal to the queue in the Timelock contract. The function takes a single argument, proposalId, which is the ID of the proposal to be queued.

The function checks that the proposal with the specified proposalId is in the Succeeded state, retrieves the proposal from the proposals mapping, calculates the earliest time at which the proposal can be executed, and loops through the targets, values, signatures, and calldatas arrays of the proposal to add each action to the queue in the Timelock contract.

Finally, the eta value is stored in the eta field of the proposal, and a ProposalQueued event is emitted with the proposalId and eta values as arguments.

#### 2.4 queueOrRevertInternal():

```bash
  function queueOrRevertInternal(address target, uint value, string memory signature, bytes memory data, uint eta) internal {
    require(!timelock.queuedTransactions(keccak256(abi.encode(target, value, signature, data, eta))), "GovernorBravo::queueOrRevertInternal: identical proposal action already queued at eta");
      timelock.queueTransaction(target, value, signature, data, eta);
  }
```

This is an internal function that takes five arguments: target, value, signature, data, and eta. This function is used to add a transaction to the queue in the Timelock contract. The first line of the function checks whether the same transaction has already been queued at the same eta. If the same transaction has already been queued, the function will revert with an error message.

The next line of the function calls the queueTransaction function of the Timelock contract to add the transaction to the queue. Overall, it is a helper function that is used to add transactions to the queue in a safe and efficient manner.

#### 2.5 execute():

```bash
   function execute(uint proposalId) external payable {
        require(state(proposalId) == ProposalState.Queued, "GovernorBravo::execute: proposal can only be executed if it is queued");
        Proposal storage proposal = proposals[proposalId];
        proposal.executed = true;
        for (uint i = 0; i < proposal.targets.length; i++) {
            timelock.executeTransaction.value(proposal.values[i])(proposal.targets[i], proposal.values[i], proposal.signatures[i], proposal.calldatas[i], proposal.eta);
        }
        emit ProposalExecuted(proposalId);
    }
```

The execute function is a public function that is used to execute a proposal that has been queued in the contract. The function takes a single argument, proposalId, which is the ID of the proposal to be executed. It checks that the proposal with the specified proposalId is in the Queued state.

It retrieves the proposal with the specified proposalId from the proposals mapping, and sets the executed field of the proposal to true. It loops through the targets, values, signatures, and calldatas arrays of the proposal and calls the executeTransaction function in the Timelock contract. Finally, a ProposalExecuted event is emitted with the proposalId as an argument.

#### 2.6 cancel():

```bash
  function cancel(uint proposalId) external {
        require(state(proposalId) != ProposalState.Executed, "GovernorBravo::cancel: cannot cancel executed proposal");

        Proposal storage proposal = proposals[proposalId];

        // Proposer can cancel
        if(msg.sender != proposal.proposer) {
            // Whitelisted proposers can't be canceled for falling below proposal threshold
            if(isWhitelisted(proposal.proposer)) {
                require((comp.getPriorVotes(proposal.proposer, sub256(block.number, 1)) < proposalThreshold) && msg.sender == whitelistGuardian, "GovernorBravo::cancel: whitelisted proposer");
            }
            else {
                require((comp.getPriorVotes(proposal.proposer, sub256(block.number, 1)) < proposalThreshold), "GovernorBravo::cancel: proposer above threshold");
            }
        }

        proposal.canceled = true;
        for (uint i = 0; i < proposal.targets.length; i++) {
            timelock.cancelTransaction(proposal.targets[i], proposal.values[i], proposal.signatures[i], proposal.calldatas[i], proposal.eta);
        }

        emit ProposalCanceled(proposalId);
    }
```

This is an external function that is used to cancel a proposal that has not yet been executed. The function takes a single argument, proposalId, which is the ID of the proposal to be canceled. It checks that the proposal with the specified proposalId is not in the Executed state. It then checks that the sender of the transaction is either the proposer of the proposal, or the proposer is whitelisted and the sender is the whitelistGuardian. If the sender is the proposer, the function checks that the proposer has fallen below the proposal threshold. If the sender is the whitelistGuardian, the function checks that the proposer has fallen below the proposal threshold and the proposer is whitelisted.

If the checks pass, the function sets the canceled field of the proposal to true, and calls the cancelTransaction function of the Timelock contract to cancel each action in the proposal. Finally, the function emits a ProposalCanceled event with the proposalId value as an argument. Overall, the cancel function plays a critical role in the decentralized governance of the Compound protocol by allowing token holders to cancel proposals that are no longer desirable or feasible.

##### 2.7 getActions():

```bash
    function getActions(uint proposalId) external view returns (address[] memory targets, uint[] memory values, string[] memory signatures, bytes[] memory calldatas) {
        Proposal storage p = proposals[proposalId];
        return (p.targets, p.values, p.signatures, p.calldatas);
    }
```

This is a public function that is used to retrieve the targets, values, signatures, and calldatas of a proposal. The function takes a single argument, proposalId, which is the ID of the proposal to be retrieved. It retrieves the proposal with the specified proposalId from the proposals mapping, and returns the targets, values, signatures, and calldatas of the proposal.

##### 2.8 getReceipt():

```bash
     function getReceipt(uint proposalId, address voter) external view returns (Receipt memory) {
        return proposals[proposalId].receipts[voter];
    }
```

This is a public function that is used to retrieve the receipt of a proposal. The function takes two arguments, proposalId and voter, which are the ID of the proposal and the address of the voter. It retrieves the proposal with the specified proposalId from the proposals mapping, and returns the receipt of the proposal for the specified voter.

##### 2.9 state():

```bash
     function state(uint proposalId) public view returns (ProposalState) {
        require(proposalCount >= proposalId && proposalId > initialProposalId, "GovernorBravo::state: invalid proposal id");
        Proposal storage proposal = proposals[proposalId];
        if (proposal.canceled) {
            return ProposalState.Canceled;
        } else if (block.number <= proposal.startBlock) {
            return ProposalState.Pending;
        } else if (block.number <= proposal.endBlock) {
            return ProposalState.Active;
        } else if (proposal.forVotes <= proposal.againstVotes || proposal.forVotes < quorumVotes) {
            return ProposalState.Defeated;
        } else if (proposal.eta == 0) {
            return ProposalState.Succeeded;
        } else if (proposal.executed) {
            return ProposalState.Executed;
        } else if (block.timestamp >= add256(proposal.eta, timelock.GRACE_PERIOD())) {
            return ProposalState.Expired;
        } else {
            return ProposalState.Queued;
        }
    }
```

This is a public view function that is used to retrieve the current state of a proposal. The function takes a single argument, proposalId, which is the ID of the proposal to retrieve. It checks that the proposalId is valid by ensuring that it is greater than the initialProposalId and less than or equal to the proposalCount. It then retrieves the proposal with the specified proposalId from the proposals mapping.

If the canceled field of the proposal is true, the function returns the Canceled state. If the block number is less than or equal to the startBlock of the proposal, the function returns the Pending state. If the block number is less than or equal to the endBlock of the proposal, the function returns the Active state. If the number of votes in favor of the proposal is less than or equal to the number of votes against the proposal, or the number of votes in favor of the proposal is less than the quorumVotes threshold, the function returns ProposalState.Defeated. If the eta field of the proposal is 0, the function returns Succeeded state. If the executed field of the proposal is true, the function returns the Executed state. If the block timestamp is greater than or equal to the eta plus the GRACE_PERIOD of the Timelock contract, the function returns the Expired state.

Otherwise, the function returns the Queued state.

#### 2.10 castVote();

```bash
   function castVote(uint proposalId, uint8 support) external {
        emit VoteCast(msg.sender, proposalId, support, castVoteInternal(msg.sender, proposalId, support), "");
    }
```

This is an external function that is used to cast a vote on a proposal. The function takes two arguments, proposalId and support, which are the ID of the proposal and support, which is a uint indicating whether the voter opposes (0), supports(1) or abstains(2) the proposal. The function then emits a VoteCast event with the following parameters - msg.sender (the address of the voter who cast the vote), proposalId, support, castVoteInternal(msg.sender, proposalId, support), and "" (an empty string).

The castVoteInternal function is called with the same arguments as the castVote function, and is responsible for actually casting the vote. The castVote function simply emits the VoteCast event and returns the result of the castVoteInternal function. Overall, the castVote function is a critical part of the Compound governance system, as it allows token holders to cast votes on proposals and participate in the decentralized decision-making process.

##### 2.11 castVoteWithReason():

```bash
    function castVoteWithReason(uint proposalId, uint8 support, string calldata reason) external {
        emit VoteCast(msg.sender, proposalId, support, castVoteInternal(msg.sender, proposalId, support), reason);
    }
```

This is an external function that is used to cast a vote on a proposal with a reason. . The function takes three arguments: proposalId, which is the ID of the proposal to vote on, support, which is a uint indicating whether the voter opposes (0), supports(1) or abstains(2) the proposal, and reason, which is a string that provides a reason for the voter's vote. The function then emits a VoteCast event with the following parameters - msg.sender (the address of the voter who cast the vote), proposalId, support, castVoteInternal(msg.sender, proposalId, support), and reason.

The castVoteInternal function is called with the same arguments as the castVoteWithReason function, and is responsible for actually casting the vote. The castVoteWithReason function simply emits the VoteCast event with the additional reason parameter and returns the result of the castVoteInternal function. The castVoteWithReason function can be useful for providing additional context and transparency around the decision-making process in the Compound governance system.

##### 2.12 castVoteBySig():

```bash
    function castVoteBySig(uint proposalId, uint8 support, uint8 v, bytes32 r, bytes32 s) external {
      bytes32 domainSeparator = keccak256(abi.encode(DOMAIN_TYPEHASH, keccak256(byte(name)), getChainIdInternal(), address(this)));
      bytes32 structHash = keccak256(abi.encode(BALLOT_TYPEHASH, proposalId, support));
      bytes32 digest = keccak256(abi.encodePacked("\x19\x01", domainSeparator,structHash));
      address signatory = ecrecover(digest, v, r, s);
      require(signatory != address(0), "GovernorBravo::castVoteBySig: invalid signature");
      emit VoteCast(signatory, proposalId, support, castVoteInternal(signatory, proposalId, support), "");
    }
```

This is an external function that is used to cast a vote on a proposal using a signature. The function takes five arguments: proposalId, which is the ID of the proposal to vote on, support, which is a uint indicating whether the voter opposes (0), supports(1) or abstains(2) the proposal, v, r, and s, which are the components of the signature.

The function first calculates the domainSeparator by hashing together the DOMAIN_TYPEHASH, the hash of the name of the contract, the getChainIdInternal function, and the address of the contract. It then calculates the structHash by hashing together the BALLOT_TYPEHASH, the proposalId, and the support value.

It then calculates the digest by hashing together the prefix "\x19\x01", the domainSeparator, and the structHash, and recovers the address of the signer using the ecrecover function with digest and the v, r, and s components of the signature.

If the recovered signatory address is not zero, the function emits a VoteCast event with the following parameters - signatory (the address of the voter who cast the vote), proposalId, support, castVoteInternal(signatory,proposalId, support), and "" (an empty string). Overall, the castVoteBySig function is a helper function that is used to cast a vote on a proposal using a signature. This can be useful for allowing users to cast votes without having to interact directly with the contract, and can help to improve the usability and accessibility of the Compound governance system.

#### 2.13 castVoteInternal();

```bash
      function castVoteInternal(address voter, uint proposalId, uint8 support) internal returns (uint96) {
        require(state(proposalId) == ProposalState.Active, "GovernorBravo::castVoteInternal: voting is closed");
        require(support <= 2, "GovernorBravo::castVoteInternal: invalid vote type");
        Proposal storage proposal = proposals[proposalId];
        Receipt storage receipt = proposal.receipts[voter];
        require(receipt.hasVoted == false, "GovernorBravo::castVoteInternal: voter already voted");
        uint96 votes = comp.getPriorVotes(voter, proposal.startBlock);

        if (support == 0) {
            proposal.againstVotes = add256(proposal.againstVotes, votes);
        } else if (support == 1) {
            proposal.forVotes = add256(proposal.forVotes, votes);
        } else if (support == 2) {
            proposal.abstainVotes = add256(proposal.abstainVotes, votes);
        }

        receipt.hasVoted = true;
        receipt.support = support;
        receipt.votes = votes;

        return votes;
    }
```

This is an internal function that is used to cast a vote on a proposal. The function takes three arguments: voter, which is the address of the voter who is casting the vote, proposalId, which is the ID of the proposal to vote on, and support, which is a uint indicating whether the voter opposes (0), supports(1) or abstains(2) the proposal. The function first checks that the proposal is in the Active state, meaning that voting is currently open for the proposal. It then checks that the support value is valid (i.e. 0, 1, or 2).

The function retrieves the Proposal struct for the specified proposalId from the proposals mapping, and then retrieves the Receipt struct for the specified voter from the receipts mapping of the proposal. The function then checks that the voter has not already voted on the proposal. It then calculates the votes that the voter has cast by calling the getPriorVotes function with the voter and proposal.startBlock as arguments.

If the support value is 0, the function adds the votes to the proposal.againstVotes value. If the support value is 1, the function adds the votes to the proposal.forVotes value. If the support value is 2, the function adds the votes to the proposal.abstainVotes value. The function then sets the receipt.hasVoted value to true, and the receipt.support value to the support value. The receipt.votes value is set to the votes value. Finally, function returns the votes value.

#### 2.14 isWhitelisted();

```bash
   function isWhitelisted(address account) public view returns (bool) {
        return (whitelistAccountExpirations[account] > now);
    }
```

The isWhitelisted function is a public view function that checks whether an account is currently whitelisted. The function takes one argument: account, which is the address of the account to check.

The function returns a boolean value indicating whether the account is currently whitelisted. It does this by checking whether the value stored in the whitelistAccountExpirations mapping for the specified account is greater than the current time (now). If the value is greater than now, then the account is considered to be whitelisted and the function returns true. Otherwise, the account is considered to be not whitelisted and the function returns false.

Overall, the isWhitelisted function is a helper function that is used to check whether an account is currently whitelisted. This can be useful for enforcing access control and ensuring that only authorized accounts are able to perform certain actions in the system.

#### 2.15 \_setVotingDelay();

```bash
  function _setVotingDelay(uint newVotingDelay) external {
        require(msg.sender == admin, "GovernorBravo::_setVotingDelay: admin only");
        require(newVotingDelay >= MIN_VOTING_DELAY && newVotingDelay <= MAX_VOTING_DELAY, "GovernorBravo::_setVotingDelay: invalid voting delay");
        uint oldVotingDelay = votingDelay;
        votingDelay = newVotingDelay;

        emit VotingDelaySet(oldVotingDelay,votingDelay);
    }
```

The \_setVotingDelay function is used to set the voting delay for proposals, and takes in one argument: newVotingDelay. It requires the caller to be the admin address and the new voting delay to be within a valid range. It updates the votingDelay variable and emits a VotingDelaySet event with the old and new voting delay values.

#### 2.16 \_setVotingPeriod();

```bash
      function _setVotingPeriod(uint newVotingPeriod) external {
        require(msg.sender == admin, "GovernorBravo::_setVotingPeriod: admin only");
        require(newVotingPeriod >= MIN_VOTING_PERIOD && newVotingPeriod <= MAX_VOTING_PERIOD, "GovernorBravo::_setVotingPeriod: invalid voting period");
        uint oldVotingPeriod = votingPeriod;
        votingPeriod = newVotingPeriod;

        emit VotingPeriodSet(oldVotingPeriod, votingPeriod);
    }
```

The \_setVotingPeriod function is used to set the voting period for proposals, and takes in one argument: newVotingPeriod. It requires the caller to be the admin address and the new voting period to be within a valid range. It updates the votingPeriod variable and emits a VotingPeriodSet event with the old and new voting period values.

#### 2.17 \_setProposalThreshold();

```bash
  function _setProposalThreshold(uint newProposalThreshold) external {
        require(msg.sender == admin, "GovernorBravo::_setProposalThreshold: admin only");
        require(newProposalThreshold >= MIN_PROPOSAL_THRESHOLD && newProposalThreshold <= MAX_PROPOSAL_THRESHOLD, "GovernorBravo::_setProposalThreshold: invalid proposal threshold");
        uint oldProposalThreshold = proposalThreshold;
        proposalThreshold = newProposalThreshold;

        emit ProposalThresholdSet(oldProposalThreshold, proposalThreshold);
    }
```

The \_setProposalThreshold function is used to set the proposal threshold for proposals, and takes in one argument: newProposalThreshold. It requires the caller to be the admin address and the new proposal threshold to be within a valid range. It updates the proposalThreshold variable and emits a ProposalThresholdSet event with the old and new proposal threshold values.

#### 2.18 \_setWhitelistAccountExpiration();

```bash
      function _setWhitelistAccountExpiration(address account, uint expiration) external {
        require(msg.sender == admin || msg.sender == whitelistGuardian, "GovernorBravo::_setWhitelistAccountExpiration: admin only");
        whitelistAccountExpirations[account] = expiration;

        emit WhitelistAccountExpirationSet(account, expiration);
    }
```

The \_setWhitelistAccountExpiration function is used to set the expiration for a whitelisted account, and takes in two arguments: account and expiration. It requires the caller to be the admin address or the whitelistGuardian address. It updates the value stored in the whitelistAccountExpirations mapping for the specified account to the specified expiration value and emits a WhitelistAccountExpirationSet event with the account and expiration values.

#### 2.19 \_setWhitelistGuardian();

```bash
     function _setWhitelistGuardian(address account) external {
        require(msg.sender == admin, "GovernorBravo::_setWhitelistGuardian: admin only");
        address oldGuardian = whitelistGuardian;
        whitelistGuardian = account;

        emit WhitelistGuardianSet(oldGuardian, whitelistGuardian);
     }
```

The \_setWhitelistGuardian function is used to set the whitelist guardian address, and takes in one argument: account. It requires the caller to be the admin address. It updates the value of the whitelistGuardian variable and emits a WhitelistGuardianSet event with the old and new whitelist guardian values.

#### 2.20 \_initiate();

```bash
      function _initiate(address governorAlpha) external {
        require(msg.sender == admin, "GovernorBravo::_initiate: admin only");
        require(initialProposalId == 0, "GovernorBravo::_initiate: can only initiate once");
        proposalCount = GovernorAlpha(governorAlpha).proposalCount();
        initialProposalId = proposalCount;
        timelock.acceptAdmin();
    }
```

The \_initiate function is used to initiate the GovernorBravo contract, and takes in one argument: governorAlpha. It requires the caller to be the admin address, and ensures the initialProposalId variable is set to 0, which indicates that the contract has not yet been initiated. It then calls the acceptAdmin function on the timelock contract to accept the admin role. It then updates the proposalCount variable to the current proposal count of the governorAlpha contract and the initialProposalId variable to the current proposal count.

The function then sets the proposalCount value to the proposalCount value of the governorAlpha contract and sets the initialProposalId value to the proposalCount value. Finally, the function calls the acceptAdmin function of the timelock contract.

#### 2.21 \_setPendingAdmin();

```bash
      function _setPendingAdmin(address newPendingAdmin) external {
        require(msg.sender == admin, "GovernorBravo:_setPendingAdmin: admin only");

        address oldPendingAdmin = pendingAdmin;

        pendingAdmin = newPendingAdmin;

        emit NewPendingAdmin(oldPendingAdmin, newPendingAdmin);
    }
```

The \_setPendingAdmin function is used to set the pending admin address, and takes in one argument: newPendingAdmin. It requires the caller to be the admin address, saves the current value of the pendingAdmin variable in the oldPendingAdmin variable for inclusion in the log and updates the pendingAdmin variable to the newPendingAdmin value. It then emits a NewPendingAdmin event with the old and new pending admin values. This can be useful for transferring the admin role to a new address, which can help to ensure the ongoing maintenance and security of the contract.

#### 2.22 \_acceptPendingAdmin();

```bash
    function _acceptAdmin() external {
        require(msg.sender == pendingAdmin && msg.sender != address(0), "GovernorBravo:_acceptAdmin: pending admin only");

        address oldAdmin = admin;
        address oldPendingAdmin = pendingAdmin;

        admin = pendingAdmin;

        pendingAdmin = address(0);

        emit NewAdmin(oldAdmin, admin);
        emit NewPendingAdmin(oldPendingAdmin, pendingAdmin);
    }
```

The \_acceptPendingAdmin function is used to accept the pending admin address, and takes no arguments. It ensures the caller is the pending admin address and is not the zero address. It saves the current value of the admin and pendingAdmin variables in the oldAdmin and oldPendingAdmin variables for inclusion in the log, and updates the admin and pendingAdmin variables to the pendingAdmin value. It clears the pendingAdmin variable, and then emits a NewAdmin and NewPendingAdmin event with the old and new admin and pending admin values.

#### 2.23 add256();

```bash
    function add256(uint256 a, uint256 b) internal pure returns (uint256) {
        uint256 c = a + b;
        require(c >= a, "GovernorBravo::add256: addition overflow");
        return c;
    }
```

The add256 function takes two uint256 arguments (a and b) and returns their sum as a uint. It first adds the two arguments together and stores the result in a new variable c. It then checks that the result is greater than or equal to the original value of a, and reverts with an error message if it is not. Finally, it returns the sum c.

#### 2.24 sub256();

```bash
    function sub256(uint256 a, uint256 b) internal pure returns (uint) {
    require(b <= a, "subtraction underflow");
    return a - b;
    }
```

The sub256 function takes two uint256 arguments (a and b) and returns their difference as a uint. It first checks that b is less than or equal to a, and reverts with an error message if it is not. It then subtracts the b from the first and returns the result.

#### 2.24 getChainIdInternal();

```bash
    function getChainIdInternal() internal pure returns (uint) {
        uint chainId;
        assembly { chainId := chainid() }
        return chainId;
    }
```

The getChainIdInternal function returns the current chain ID as a uint. It does this by using inline assembly to call the chainid() opcode, which returns the current chain ID.

## <h2 id="findings">3.0 FINDINGS </h2>

### <h3 id="Qanalysis"> 3.1 Qualitative Analysis<h3>

_(**Table: 3.1**: GovernorBravoDelegate G2 Qualitative Analysis)_
| Metric | Rating | Comment |
| :-------- | :------- | :----- |
| Code Complexity | Excellent | Functionality is very simple and organized |
| Documentation | Moderate | Documentation could be improved |
| Best Practices | Moderate | Some best practices were implemented but also found lacking in certain areas |

### <h3 id="summary">3.2 Summary<h3>

In summary, the code appears to be well-structured and follows best practices for a Solidity smart contract. It includes essential functions for proposal creation, voting, and execution in a decentralized governance system. The code uses appropriate validation checks to ensure the integrity and security of the proposals. However, as with any code, continuous monitoring, testing, and potential optimizations are recommended to maintain its efficiency and reliability.

### <h3 id="recom">3.2 Recommendations<h3>

Consider using the SafeMath library to ensure safe arithmetic operations to prevent overflow/underflow, instead of manually checking for overflow/underflow.

```bash
    using SafeMath for uint256;

// Use like this: a.add(b) instead of a + b
```

## <h2 id="conclusion">4.0 CONCLUSION </h2>

In this audit, I have thoroughly examined the "GovernorBravoDelegate" Solidity smart contract, focusing on its design and implementation. "GovernorBravoDelegate" is a critical component for decentralized governance within a blockchain-based application. It facilitates proposal creation, voting, execution, and administrative actions, essential for effective decentralized decision-making.

The code is well-organized, following established best practices in Solidity development. It demonstrates a robust approach to decentralized governance and aligns with the principles of secure and efficient smart contract programming. The contract incorporates necessary validation checks to ensure the integrity and security of the governance processes.

However, considering the evolving nature of blockchain technology and smart contract security, continued testing, auditing, and potential updates are recommended to maintain and enhance the contract's reliability and functionality.

Overall, the "GovernorBravoDelegate" contract presents a solid foundation for decentralized governance, contributing positively to the broader blockchain ecosystem. The identified suggestions can be valuable for refining the contract and informing future implementations in a more efficient and maintainable manner.
