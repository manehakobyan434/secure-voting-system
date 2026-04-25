#  Secure Voting System (Solidity)

# A decentralized voting smart contract built in Solidity that allows an owner to create elections, add candidates, and enable secure one-wallet-one-vote voting.

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.13;

contract VotingSystem {
    address public owner;
    uint public electionCount;

    mapping(uint => Election) public elections;
    mapping(uint => Candidate[]) public electionCandidates;
    mapping(uint => mapping(address => bool)) public hasVoted;

    event ElectionCreated(uint indexed electionId, string name);
    event CandidateAdded(uint indexed electionId, string name);
    event Voted(uint indexed electionId, address voter, uint candidateIndex);

    modifier onlyOwner() {
        require(msg.sender == owner, "Only owner can call this function");
        _;
    }

    constructor() {
        owner = msg.sender;
    }

    struct Election {
        string name;
        uint startTime;
        uint endTime;
        bool exists;
    }

    struct Candidate {
        string name;
        uint voteCount;
    }

    function createElection(string memory _name, uint _duration) public onlyOwner {
        require(_duration > 0, "Duration must be greater than 0");

        electionCount++;

        elections[electionCount] = Election({
            name: _name,
            startTime: block.timestamp,
            endTime: block.timestamp + _duration,
            exists: true
        });

        emit ElectionCreated(electionCount, _name);
    }

    
    function addCandidate(uint _electionId, string memory _name) public onlyOwner {
        require(elections[_electionId].exists, "Election does not exist");
        require(block.timestamp < elections[_electionId].startTime, "Election already started");

        electionCandidates[_electionId].push(
            Candidate({
                name: _name,
                voteCount: 0
            })
        );

        emit CandidateAdded(_electionId, _name);
    }

    function vote(uint _electionId, uint _candidateIndex) public {
        require(elections[_electionId].exists, "Election does not exist");

        Election storage election = elections[_electionId];

        require(block.timestamp >= election.startTime, "Election not started");
        require(block.timestamp <= election.endTime, "Election ended");

        require(!hasVoted[_electionId][msg.sender], "Already voted");

        Candidate[] storage candidates = electionCandidates[_electionId];
        require(_candidateIndex < candidates.length, "Invalid candidate");

        candidates[_candidateIndex].voteCount++;

        hasVoted[_electionId][msg.sender] = true;

        emit Voted(_electionId, msg.sender, _candidateIndex);
    }

    function getCandidates(uint _electionId)public view returns (Candidate[] memory)
    {
        return electionCandidates[_electionId];
    }
}
