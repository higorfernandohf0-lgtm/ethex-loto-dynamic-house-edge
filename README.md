# EthexLoto — Dynamic House Edge

A Solidity implementation that replaces fixed house edge logic
with a dynamic model based on player behavior.

## The Problem

Most on-chain lottery contracts use a fixed house edge regardless
of how many cells a player marks. This creates an imbalance —
players who take more risk (fewer cells) pay the same fee as
those who play it safe. A fair system should reward risk.

## Dynamic House Edge Rules

| Marked Cells | House Edge |
|---|---|
| 1 cell | 12% |
| 2–3 cells | 10% |
| 4–6 cells | 8% |

Players who take more risk pay lower fees. The math is transparent
and verifiable on-chain.

## What I Changed

The core change is a single internal function added to the contract:

```solidity
function getHouseEdge(uint8 markedCount)
    internal pure returns (uint256) {
    if (markedCount == 1) return 12;
    if (markedCount <= 3) return 10;
    return 8;
}
```

Applied inside `placeBet()` — no changes to the public interface,
jackpot logic, or settlement flow.

## What Stays Unchanged

- Public contract interface
- Jackpot registration and payout
- Settlement and refund behavior
- Existing marked cell counting logic

## Test Results

```bash
npx truffle test test/CandidateDynamicHouseEdgeTests.js

  ✓ Routes house fee correctly for every marked cell count (1 to 6)
  ✓ Reverts when bet has zero marked cells
  ✓ Uses dynamic house edge in expired bet refund

3 passing
```

## How to Run

```bash
npm install
npx truffle test
```

## Tech Stack

Solidity ^0.5.10 · Truffle · JavaScript (tests)

## What I Learned

Working on this contract taught me how Solidity handles integer
division and why fee calculations need to be validated at every
edge case — a single rounding error in a lottery contract can
drain the jackpot over thousands of bets.

---
Built by [Higor Fernando](https://x.com/HigorWeb3)
