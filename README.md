# 🗳️ Secure Voting System (Solidity)

A decentralized voting smart contract built in Solidity that allows an owner to create elections, add candidates, and enable secure one-wallet-one-vote voting.

---

## 🚀 Features

- Create multiple elections
- Add candidates before voting starts
- One wallet = one vote per election
- Time-based voting system
- Event logging for frontend integration
- Anti double-voting protection

---

## 🧠 Key Concepts Used

- Mappings (data storage)
- Structs (Election, Candidate)
- Access control (onlyOwner modifier)
- Events (Blockchain logging)
- Time-based restrictions (block.timestamp)
- Storage vs Memory usage

---

## ⚠️ Known Limitation

This system prevents double voting per wallet, but does not prevent users from creating multiple wallets (Sybil attack problem), which is a known limitation in most blockchain voting systems.

---

## 🛠️ Future Improvements

- Add frontend (React + Ethers.js)
- Add candidate IDs instead of index
- Add results / winner function
- Add whitelist or identity verification system

---

## 👨‍💻 Author

Built while learning Solidity & Smart Contracts.
