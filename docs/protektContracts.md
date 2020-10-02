# Protekt Contracts
Protekt contracts are configurable insurance contracts that create a P2P market for cover and liability on top of ANY smart contract, whether it's a lending pool, market making pool, staking pool, etc. Similar to how Uniswap allows anyone to create a spot market for any token, Protekt contracts allows anyone to create an insurance market for any smart contract.

## Contract structure
Each Protekt contract is a two-sided market for insurees to cover their position in a DeFi protocol, and insurers to take on that liability in tokenized form. Each contract conforms to the same generalizable interface so that entering/exiting the market, receiving rewards, and submitting claims is consistent and can be snapped together with other money lego blocks.

However, the parameters of the underlying market can be specifying when the market is created, including:
* Fees - Amount and how fees are paid
* Coverage - Amount of coverage
* Strategy - How the staked capital is invested
* Payout Event - What constitutes a payout event
* Claims process - Whether the claims process is automated or manual

### Fees
Each contract will implement a `claimRewards()` function which any insuree can call. The function will collect any new rewards, take out the fees payable to the protocol, and return any excess to the user.

### Coverage
The coverage amount of the underlying pool. In most cases, this will be 100% of the underlying value but can vary based on the pricing algorithm.

### Strategy
Similar to yearn, the staked capital can be invested via a configurable strategy. The simplest strategy is just to hold the underlying token, but the capital pool could be actively or passively managed as well.

### Payout Events
Payout events explicitly outline what executes the insurance contract. For instance, if a hack or financial exploit takes place on a protocol, obligations are greater than available collateral in the market. This condition can be measured with a smart contract query, so a Protekt contract could define that as a payout event. Alternatively, a DAO could govern what is considered a payout event if human dependencies are desirable.

### Claims Process
The claims process follows the same process steps for each Protekt contract. However, the process can be run via automated smart contract rules, a DAO, or a centralized party.
1. `submitClaim()` - Called to check for a `payoutEvent` and, if true, start the claims investigation period.
2. Claims investigation period - Payout events need to be true to begin the period and still true at the end of the period. The default period is 1 week.
3. `initiatePayout()` - Called after the claims investigation period and, if the payout event is still true, initiate liquidation of the staked capital for payouts.

![Claims Process](/img/claimsProcess.png)

## Examples
Let's look at some examples to see what can be built:
1. [Protekt cDai](./protektcDai.md) - Protect DAI deposits in Compound
2. DAO treasury coverage - Protect the treasury of a project from being drained
3. Simple Uniswap LP coverage - Protect LP shares from being drained or wild swings
4. Audit Firm coverage (centralized) - Audit firm stakes that a project is secure technically and is paid ongoing fees

| Name | For Insurees | For Insurers | Payout Events | Payouts |
|---------|----------|---------|---------|---------|
|[Protekt cDai](./protektcDai.md)|Users can deposit cDAI and get 1:1 pcDAI back. The only difference is that pcDAI only earned 80% of COMP rewards.|Stakers deposit ETH and receive an obligation to the equivalent portion of the pool. They earn rewards on their stake but get liquidated if a payout event occurs.|Anyone can call `submitClaim()` which does a smart contract query whether a payout scenario can occur. If it has, then the pool enters the investigation period where coverage and staking withdrawals are frozen.|After the claim investigation period, anyone can call `claimPayout()` function, which checks if the payment scenario is still true, and liquidates the pool and potentially part of the Mothership Vault. pcDAI holders can redeem their tokens for the equivalent cDAI (which may be discounted) plus the proceeds from the liquidations, paid out in ETH.|
|DAO treasury coverage|||||
|Simple Uniswap LP coverage|||||
|Audit Firm coverage (centralized)|||||