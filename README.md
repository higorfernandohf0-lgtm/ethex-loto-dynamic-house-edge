# EthexLoto Dynamic House Edge

This project implements a dynamic house edge system for a Solidity lottery contract.

## Overview

The original lottery contract used a fixed house edge for all bets.

The goal of this project was to make the house edge dynamic based on the number of selected bet slots while preserving the existing jackpot behavior.

## Dynamic House Edge Rules

- 1 selected slot: 12%
- 2–3 selected slots: 10%
- 4–6 selected slots: 8%

## What I Changed

- Added dynamic fee calculation
- Preserved jackpot behavior
- Preserved the existing contract interface
- Updated bet fee logic
- Ensured expired bet refunds use the correct dynamic fee

## Tech Stack

- Solidity
- Truffle
- JavaScript tests
- Smart contract testing

## What I Learned

- Reading existing Solidity code
- Implementing business logic in smart contracts
- Working with technical requirements
- Understanding fee models
- Debugging smart contract behavior

## Portfolio Note

This project is part of my Web3 learning journey and helped me practice Solidity, contract logic, and test-driven development.

## Test Status

All candidate tests passed successfully using Truffle.
