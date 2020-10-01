# Protekt cDai
## Covered Risk
This protekt contract provides coverage on the DAI pooled in Compound's cDAI smart contract, insuring it against technical bugs that drain the contract, financial manipulation, and centralization risk.

With a [DeFi Score](https://app.defiscore.io/assets/dai) of 8.1 on Sep 28, 2020, the Compound DAI lending market is one of the least risky applications in DeFi.

See the [Risk Analysis section](#risk-analysis) below for more details.

### Not Covered
The following risks are still present and NOT covered by this contract:
* DAI price risk - If DAI were to lose its peg for an extended period of time, Compound's cDAI market could sustain loss in value. This event is not covered by this protekt contract.
* Maker Protocol Risk - If the Maker protocol sustains a massive shortfall event, DAI could lose its peg or experience other adverse events. This event is not covered by this protekt contract.

## For Insurees
Users can deposit cDai and get pTokens in return, and those pcDAI tokens can be redeemed for underlying cDai 1:1.

![pToken Image](/img/pTokenDiagram.png)

### Fees
Each pcDAI is the same as cDAI except up to 20% of the COMP rewards go to Shield Miners instead of being collected by the pcDAI holder. The exact fee will be set by the market, depending on the ratio of the Coverage pool to the Staking pool, but is capped at 20%.

### Payout Events
Payout events are calculated entirely programmatically based on the following query:
`ZZZ`

The query must be true for the entirety of the claims investigation period which is **1 week** (ZZZ blocks).

### Claims Process
If a payout event occurs, the following process leads to a payout of the insurees:
1. Payout event (technical hack, financial exploit, admin keys compromised)
2. Any user submits `submitClaim(payoutAmount)` and, if true, the protekt contract entered an investigation period of 1 week.
3. After the investigation period, any user submits `initiatePayout()` and, if the event is still true, the protekt contract liquidates up until the `payoutAmount`.
4. pcDAI holders can redeem their tokens for the full payout amount in ETH and their original cDAI tokens (which may have lost value).

## For Shield Miners
Shield mining is the act of Stakers depositing capital signaling their conviction that the underlying smart contracts are safe from technical, financial, and centralization exploits and, in return, earn rewards. This bucket of capital is called the Staking pool.

### Staking pool
The Staking pool for this Protekt contract has the following parameters:
* Reserve Token: **ETH**
* Withdraw delay: **0 blocks**
* Investment Strategy: **HODL, not Invested**
* Cash Pool: **No Cash pool**

### Rewards
* For all the covered cDAI, shield miners will receive up to 20% of the COMP rewards that are issued over those blocks. The exact % of COMP will be calculated by the ratio of coveraged `cDAI / Amount Staked`.

#### Additional rewards
Additional rewards may be offered to shield miners but are not guaranteed. These additional rewards include:
* Native PKT token rewards
* Native rewards from projects that want to encourage more stakers to enter the contract

## [Risk Analysis](#risk-analysis)
With a [DeFi Score](https://app.defiscore.io/assets/dai) of 8.1 on Sep 28, 2020, the Compound DAI lending market is one of the least risky applications in DeFi.

Compound maintains a prominent [Security page](https://compound.finance/docs/security) on their site, which includes:
* Audit history from [Trail of Bits](https://www.trailofbits.com/) and [OpenZeppelin](https://openzeppelin.com/).
* The smart contracts have been formally verified by Certora using Certora ASA (Accurate Static Analysis)
* A market stress test has been simulated by [Gauntlet](https://gauntlet.network/).
* A Bug Bounty program to incentivize white hat hackers to identify vulnerabilities
* Centralization risk tracked by [Codefi Inspect](https://inspect.codefi.network/).
