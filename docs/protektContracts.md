# Protekt Pools
Protekt pools are configurable insurance contracts that can be set up on top of ANY DeFi pool, whether it's a lending pool, market making pool, staking pool, etc. They consist of 3 modules:
1. Coverage Pool
2. Protekt Contract
3. Staking Pool

![Protekt Pool Image](/img/ProtektPool.png)

## Modules

### Coverage Pool
As an example, users can deposit Dai that gets forwarded into the Compound cDAI pool and get pTokens in return. The cDai tokens are held by the Coverage pool. pcDai tokens can be redeemed for underlying cDai 1:1.

Parameters
* Underlying token

### Staking Pool
As an example, users can stake ETH and take on the liability of the cDAI pool. In return for the risk of potentially getting liquidated, stakers earn fees from the Coverage pool. Furthermore, the deposits can be invested to build up cash

Parameters
* Reserve token
* Withdraw delay (if any)
* Investment Strategy

### Protekt Contract
Protekt contracts are configurable insurance contracts that define the terms of the market including:
* What fees are takens and how
* Underlying pool appraisal and coverage percentage
* What rules define an incident on that pool?
    * A smart contract query
    * DAO vote
    * Central actor
* Claims process
	* Who can submit a claim?
	* How long is the claim investigated?
	* Are payouts payment-in-kind or in ETH/DAI/USDC?

## Examples
Let's look at examples to see what can be built:
1. [Protekt cDai](./protektcDai.md) - Protect DAI deposits in Compound
2. DAO treasury coverage - Protect the treasury of a project from being drained
3. Simple Uniswap LP coverage - Protect LP shares from being drained or wild swings
4. Audit Firm coverage (centralized) - Audit firm stakes that a project is secure technically and is paid ongoing fees


| Name | For Insurees | For Stakers | Payout Events | Payouts |
|---------|----------|---------|---------|---------|
|[Protekt cDai](./protektcDai.md)|Users can deposit cDAI and get 1:1 pcDAI back. The only difference is that pcDAI only earned 90% of COMP rewards.|Stakers deposit COMP and recieve an obligation to the equivalent portion of the pool. They earn rewards on their stake but get liquidated if a payout event occurs.|Anyone can call `submitClaim()` which does a smart contract query whether a payout scenario can occurred. If it has, then the pool enters the investigation period where coverage and staking withdrawals are frozen.|After the claim investigation period, anyone can call `claimPayout()` function, which checks if the payment scenario is still true, and liquidates the pool and potentially part of the Mothership Vault. pcDAI holders can redeem their tokens for the equivalent cDAI (which may be worthless or discounted) plus the proceeds from the liquidations, paid out in COMP.|
|DAO treasury coverage|||||
|Simple Uniswap LP coverage|||||
|Audit Firm coverage (centralized)|||||