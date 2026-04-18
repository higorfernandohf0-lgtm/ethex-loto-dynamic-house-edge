# Ethex Loto - Dynamic House Edge

## Overview
This repository contains my implementation for the technical assessment: adding **dynamic house edge** logic to the `EthexLoto` smart contract.

The fixed house edge was replaced with a dynamic calculation based on the number of marked cells, while **strictly preserving** all existing behaviors (public interface, jackpot logic and settlement flow).

## Task Requirements
The house edge must be calculated dynamically as follows:

- **1 marked cell** → 12% house edge  
- **2–3 marked cells** → 10% house edge  
- **4–6 marked cells** → 8% house edge  

**Constraints:**
- Do not change any public interfaces
- Keep jackpot logic unchanged
- Keep settlement and refund behavior unchanged
- All provided tests must pass

## Key Changes
- Added `getHouseEdge(uint8 markedCount)` internal pure function
- Updated `placeBet` to calculate marked cells using existing logic and apply dynamic house edge
- Replaced all fixed `HOUSE_EDGE` references with the new dynamic calculation
- Adjusted bet amount and fee routing accordingly

## Why This Implementation Is Safe
- Public contract interface was not modified
- Jackpot registration and payout logic fully preserved
- Settlement flow (`settleBets`) remains unchanged
- Reuses existing marked cell counting logic
- No new state variables or complex mechanisms introduced

## Edge Cases Considered
- Bets with zero marked cells still revert as expected
- Expired bets refund the correct dynamic fee-adjusted amount
- All ranges (1, 2-3, 4-6) apply the right house edge percentage

## Test Results
All candidate tests are **passing**:

```bash
npx truffle test test/CandidateDynamicHouseEdgeTests.js

 Routes house fee correctly for every marked cell count (1 to 6)
 Reverts when bet has zero marked cells
 Uses dynamic house edge in expired bet refund

How to Runbash

# Install dependencies
npm install

# Run the candidate task tests
npx truffle test test/CandidateDynamicHouseEdgeTests.js

# Run all tests
npx truffle test

Tech StackSolidity ^0.5.10
Truffle Framework
JavaScript (tests)

