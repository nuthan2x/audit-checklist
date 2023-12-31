## Staking / Vault

1. Reward distribution - is it implemented correctly according to docs/comments ? 
2. User issue - can a taker withdraw more than he should (ex:sandwichers) ? Or does he derserve more than he got when reward claimed/LP burn ?
3. Overflow/underflow protected -  ( int256 usafe, safe downcasting ?? )
4. Rounding issues - ( unsafe round down/ up, precision loss ??) Loop as an attacker to leverage the rounding issue ? Can avoid paying fee and unsatke/claim the reward ?
5. Abusing staking duration - (block.number/timestamp dependence) ( initially `last claimed` value will be zero, so abuse the default state ??)
6. BalanceOf attack - manipulate balance to either cause DOS/inflation attack / second LP paying huge inflated price/ set the system to  state where teh require statement fails internally/ force send/ flashloans/ sync() ? / doantion attack.
7. LP mint/burn - these actions should be exacct opposite and do state changes in polar opposite., check if any state needs update
8. Global state change - Does owner altering fee/pause/any global state affects the system/user ? can it be MEVed ? / does the new change effect old stakers ?
9. external calls - reentrancy(read/cross function/ cross contract), CEI pattern followed ? return bombs / griefing / DOS or permanent bricking / proper WETH/ETH handling - WETH has fallback function, so external call to WETH will always be success == true, abuse it or push over pull for ETH receiving DOSers
10. Weird token handling - decimals/Fee on transfer/rebasing/double address/safeERC usage/ custom ERC implementation or features ??
11. Oracle attack - abuse by flashloan / external oracle dependency and weak implementaion or stale prices/ TWAP abuse and impletation? / read or write or swap with any dexes internally??
12. DOS - duw to huge array read/write/ struct usage and not clearing or deleting when burn or storage keyword and pointer usage/ for loop exceeding whole blockspace ? what if a whale stakes and doesn't claim/unstake ??
13. MEV - how easy to MEV/ slippage protection of minOut and deadline implemented ??
14. Access control - is renounce overridden and added revert ? onlyOwner to all functions ? functions that are hidden inside inheried chain of contracts? / implement how OZeppelin says to ??
15. If protocol is a fork - run their tests here/ see contract difference and loopholes
16. What if someone autocompounds every 5 minutes to claim all the rewards by being a whale ?? Add minimum claim check

