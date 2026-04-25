#  Secure Voting System (Solidity)

A Solidity smart contract for decentralized voting that allows an owner to create elections, add candidates, and enable secure one-wallet-one-vote participation with time-based restrictions.

## Features
- Create elections (admin only)
- Add candidates before voting starts
- One wallet = one vote per election
- Time-based voting (start/end)
- Vote tracking per candidate
- Event logging for transparency

## Functions
- createElection() – create a new election
- addCandidate() – add candidates to an election
- vote() – cast a vote securely
- getCandidates() – view candidates and votes

## Limitation
Prevents double voting per wallet, but does not prevent users from using multiple wallets.

## Tech
- Solidity ^0.8.13
- Ethereum Smart Contracts
