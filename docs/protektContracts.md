# Protekt Contracts
Protekt contracts are configurable insurance contracts that create a P2P market for cover and liability on top of ANY smart contract, whether it's a lending pool, market making pool, staking pool, etc. Similar to how Uniswap allows anyone to create a spot market for any token, Protekt contracts allows anyone to create an insurance market for any smart contract.

Each Protekt contract is a two-sided market for insurees to cover their position in a DeFi protocol, and insurers to take on that liability in tokenized form. Each contract conforms to the same generalizable interface so that entering/exiting the market, receiving rewards, and submitting claims is consistent and can be snapped together with other money legos.

## Creating a Protekt Contract
The parameters for creating a Protekt contract are:
* `underlyingToken` - Address of the insured token (i.e. cDAI on Compound)
* `feeModel` - Contract address that specifies the fee model for the contract
* `depositToken` - The token that's staked by shield miners (normally ETH, DAI, or USDC)
* `investmentStrategy` - Contract address for the strategy for the `depositToken`
* `claimsManager` - Contract address for the claims process (conforming to `ClaimsManagerInterface.sol`)

### Underlying Token
The address of the underlying token that should be insured. For instance, it'd be the cDAI contract `0x5d3a536E4D6DbD6114cc1Ead35777bAB948E3643` to insure DAI in Compound or the DAI<>ETH LP Token (`0x1f9840a85d5af5bf1d1762f925bdaddc4201f984`) on Uniswap.

### Fee Model
Each Protekt contract will point to a `feeModel` contract, which specifies the premiums that insurees pay for coverage. Encapsulating the logic in a separate smart contract allows the model to be adjusted over time and even switched out if needed.

### Deposit Token
The reserve token for the market, which shield miners stake. Typically, this token is a reserve asset like ETH, DAI, or USDC. This token is invested for returns according to the `investmentStrategy` contract.

### Investment Strategy
Borrowed from [yearn](https://yearn.finance/), the staked deposit token can be invested via a configurable strategy. The simplest strategy is just to hold the token, but the capital could be actively or passively managed as well, for instance, used to collect trading fees on Balancer.

### Claims Manager
Each Protekt contract will point to a `claimsManager` contract, which defines what constitutes a payout event, a claims investigation period, and the liquidation waterfall if a payout event occurs. Encapsulating the logic in a separate smart contract allows the process to be run by an programmable smart contract, a DAO, or a centralized party.
1. `submitClaim()` - Called to check for a `payoutEvent` and, if true, start the claims investigation period.
2. Claims investigation period - Payout events need to be true from begin the period and still true at the end of the period. The default period is 1 week (43,200 Blocks).
3. `payoutClaim()` - Called after the claims investigation period and, if the payout event is still true, initiate liquidation of the staked capital for payouts.

**In short, each insurance contract follows the same claims process but can be executed via programmatic rules, a DAO, or centralized party.**

![Claims Process](/img/claimsProcess.png)

#### Payout Events
Payout events explicitly outline what executes the insurance contract. For instance, if a hack or financial exploit takes place on a protocol, obligations are greater than available collateral in the market. This condition can be measured with a smart contract query, so a Protekt contract could define that as a payout event. Alternatively, a DAO or centralized party could govern what is considered a payout event if human dependencies are desirable.

#### Liquidations
If a claim is successfully made, the payouts will be made by liquidating the Protekt pool and, if necessary, the PKT Mothership Pool. This structure was inspired by a [distribution waterfall ](https://en.wikipedia.org/wiki/Distribution_waterfall) so that multiple buckets of capital can be set up to assume different amounts of liability to the underlying pool. Payouts can be made via [payment-in-kind](https://www.investopedia.com/terms/p/paymentinkind.asp) or swapped and distributed in any token.

## Architecture
![Claims Process](/img/smartContractArchitecture.png)

## Examples
Let's look at some examples to see what can be built:
1. Protekt cDai - Protect DAI deposits in Compound
2. DAO treasury coverage - Protect the treasury of a project from being drained
3. Simple Uniswap LP coverage - Protect LP shares from being drained or wild swings
4. Audit Firm coverage (centralized) - Audit firm stakes that a project is secure technically and is paid ongoing fees

| Name | For Insurees | For Insurers | Payout Events | Payouts |
|---------|----------|---------|---------|---------|
|[Protekt cDai](./protektcDai.md)|Users can deposit cDAI and get 1:1 pcDAI back. The only difference is that pcDAI only earned 80% of COMP rewards.|Stakers deposit ETH and receive an obligation to the equivalent portion of the pool. They earn rewards on their stake but get liquidated if a payout event occurs.|Anyone can call `submitClaim()` which does a smart contract query whether a payout scenario can occur. If it has, then the pool enters the investigation period where coverage and staking withdrawals are frozen.|After the claim investigation period, anyone can call `payoutClaim()` function, which checks if the payment scenario is still true, and liquidates the pool and potentially part of the Mothership Vault. pcDAI holders can redeem their tokens for the equivalent cDAI (which may be discounted) plus the proceeds from the liquidations, paid out in ETH.|
|DAO treasury coverage|Users can deposit their pooled token (xtoken) and get 1:1 pxtoken back. The protocol DAO pays a percentage of protocol rewards to the Protekt contract per block.|Stakers deposit ETH and receive an obligation to the equivalent portion of the pool. The DAO can take a large position here signalling confidence in their protocol. The stakers earn rewards on their stake but get liquidated if a payout event occurs.|Anyone can call `submitClaim()` which prompts the DAO to specify whether a payout scenario has occurred. If it has, then the pool enters the investigation period where coverage and staking withdrawals are frozen.|After the claim investigation period, the DAO can call `claimPayout()` function which liquidates the pool and potentially part of the Mothership Vault. pxtoken holders can redeem their tokens for the equivalent xtoken plus the proceeds from the liquidations, paid out in ETH.|
|Simple Uniswap LP coverage|Users can deposit Uniswap LP tokens and get 1:1 pLPtokens back. The only difference is that pLPtokens only earned 80% of UNI rewards.|Stakers deposit ETH and receive an obligation to the equivalent portion of the pool. They earn rewards on their stake but get liquidated if a payout event occurs.|Anyone can call `submitClaim()` which does a smart contract query whether the Uniswap pool is grossly out of line with the asset prices. If it has, then the pool enters the investigation period where coverage and staking withdrawals are frozen.|After the claim investigation period, anyone can call `payoutClaim()` function, which checks if the payment scenario is still true, and liquidates the pool and potentially part of the Mothership Vault. pLPtokens holders can redeem their tokens for the equivalent LPtoken (which may be discounted) plus the proceeds from the liquidations, paid out in ETH.|
|Audit Firm coverage (centralized)|Users can deposit their pooled token (xtoken) and get 1:1 pxtoken back. Rewards accumulate to xtokens with a small fee that goes to the stakers.|Stakers deposit ETH and receive an obligation to the equivalent portion of the pool. The audit firm can take a large position here signalling confidence in their protocol and earn rewards from those that take cover.|Anyone can call `submitClaim()` which prompts the DAO to specify whether a payout scenario has occurred. If it has, then the pool enters the investigation period where coverage and staking withdrawals are frozen.|
After the claim investigation period, the anyone can call `claimPayout()` function which liquidates the pool and potentially part of the Mothership Vault. pxtoken holders can redeem their tokens for the equivalent xtoken plus the proceeds from the liquidations, paid out in ETH. The audit firm likely loses their stake.|