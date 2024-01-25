1. Frontrun/backrun
    - MEV / andwich attack to extract value ex: improper deadline/slippage used.
    - cause DOS / block the auction
    - frontrun arotocol owneraction ex: claim rewards, important parameter changes like feePercent/base price/interest rate/reward rate etc.,

2. using samll amounts
    - pass in 1 wei/amount to abuse the contracts (ex. may lead to DOS mostly)
    - First Lp infaltion attack

3. Passing 0 as input
    - abuse dev's intentions (ex: supply 0 values to make unbound huge array)
    - if there's no minimum cost/input validation, then abuse with 0 values.

4. Using contracts that doesn't accept ETH
    - look for ways to DOS by injecting a contract that reverts on ETH/safeTransfer of Nfts

5. Gas griefing external calls
    - if  some action depends on external calls, then see if that contract can gas grief that call flow.
    - example: NFT safe transfer call. 

6. Weird ERC20 tokens
    - ERC777, Fee-on-Transfer, blacklisting tokens, USDT/BNB approval implemntation, hardcoded decimals, 2 contract address per tkken, low decimal token + rounding attack/precision loss, tokens  use u96 for tok amonts like $UNI.

7. Price manipulation
    - amm pool reserve/balanceOf dependence manipulation

8. Balcklisted addresses
    - ex: id some EOA blacklisted by USDC/USDT that holds a collateral of a debt, then liquidation will revert leaving a bad debt to LPs.

9. underflow/overflow
    - unsafe casting, more at <https://faizannehal.medium.com/how-solidity-0-8-protect-against-integer-underflow-overflow-and-how-they-can-still-happen-7be22c4ab92f> or go to solodit.xyz and type search `unsafe cast`

10. block re-orgs
    - make transaction that can benefit fron reorgs ex: [here](https://solodit.xyz/issues/m-01-questfactory-is-suspicious-of-the-reorg-attack-code4rena-rabbithole-rabbithole-quest-protocol-contest-git) and [here](https://solodit.xyz/issues/m-01-identifying-publications-using-its-id-makes-the-protocol-vulnerable-to-blockchain-re-orgs-code4rena-lens-protocol-lens-protocol-git)

11. Reentrancy
    - read only, same function/cross function/cross contract re-entrancy

12. sybil attacks on incentives
    - stake with multiple accounts and earn more rewards ??
    - frontrun stepwise txn's like, increase reward rate..,

13. Flashloans
    - AMMs, staking vaults

14. Accepting data from external call
    - return bomb DOS by consuming huge gas by returning a length data return

15. balanceOf dependence
    - break the accounting of contract by donating some tokens ? Inflate by being first LP

16. forced precision loss
    - find a way to make function revert by making those `require` lines true, leading to DOS
    - ex: balanceOf validation, 

17. abuse this "contract before deployment and after deployment"
    - contract addresses can be predicted, so any code/codehash/balance dependence can be DOSed by abusing create/create2/using metamorphic contracts

18. external call DOS
    - revrt on call, return bomb, gas grief, reentrancy

19. unexepcted parameter passing to revrt critical functions
    - find a way if passing some address as input, then somewhere in system, using that data will revert
    - This is just another way to cause revert by breaking the `require` validation DOS

20. selecter clashing
    - proxy vs implementation's selector clashing

21. signatures
    - replaying (same chain/coss chain/cross contract), malleable, ecrecover doent validate zero address return
    - not using nonces/OZ's ECDSA like implementations/EIP712 not followed ?
    - not encoding nonce/msg.sender is a redflag

22. hash collion
    - hashing encode packed on dynamic data will lead to same  sometimes
