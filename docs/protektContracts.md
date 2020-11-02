---
id: protekt-contracts
title: Protekt Contracts
---

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
![Smart](/img/smartContractArchitecture.png)

## Examples
Let's look at some examples to see what can be built:
1. Protekt cDai - Protect DAI deposits in Compound
2. DAO treasury coverage - Protect the treasury of a project from being drained
3. Simple Uniswap LP coverage - Protect LP shares from being drained or wild swings
4. Audit Firm coverage (centralized) - Audit firm stakes that a project is secure technically and is paid ongoing fees

| Name | Coverage Cost | Shield Mining | Claims & Payout |
|---------|----------|---------|---------|
|Protekt cDai|Users can deposit cDAI from Compound and get 1:1 pcDAI back. The only difference is that pcDAI only earned 80-90% of COMP rewards. The other 10-20% goes to the shield miners.|Shield miners deposit ETH and can withdraw at any time. They earn 10-20% COMP rewards on their stake but get liquidated if a payout event occurs.|Anyone can submit a claim and if a payout event has occurred, then the pool enters the investigation period where coverage and staking withdrawals are frozen. After the claim investigation period, if the payout event is still true, the Shield Mining contract is liquidated and ETH is claimable by pcDAI holders.|
|Protekt aUSDC|Users can deposit aUSDC from Aave and get 1:1 paUSDC back. There’s a 0.1% fee when deposited and withdrawn.|Shield miners deposit USDC and can withdraw at any time. They earn all deposit and withdrawal fees on their stake but get liquidated if a payout event occurs.|Anyone can submit a claim and if a payout event has occurred, then the pool enters the investigation period where coverage and staking withdrawals are frozen. After the claim investigation period, if the payout event is still true, the Shield Mining contract is liquidated and ETH is claimable by paUSD holders.|
|Simple Uniswap LP coverage|Users can deposit Uniswap LP tokens and get 1:1 pLPtokens back. The only difference is that pLPtokens only earned 80% of UNI rewards.|Shield miners deposit ETH and can withdraw at any time. They earn 20% UNI rewards on their stake but get liquidated if a payout event occurs.|Anyone can submit a claim and if a payout event has occurred, then the pool enters the investigation period where coverage and staking withdrawals are frozen. After the claim investigation period, if the payout event is still true, the Shield Mining contract is liquidated and ETH is claimable by pLPtokens holders.|
|DAO treasury coverage|Users can deposit their pooled token (xtoken) and get 1:1 pxtoken back. The protocol DAO pays a percentage of protocol rewards to the Protekt contract per block.|Shield miners deposit ETH and can withdraw at any time. They earn a portion of the protocol rewards for assuming the liability of the treasury.|Anyone can submit a claim and if a payout event has occurred, then the pool enters the investigation period where coverage and staking withdrawals are frozen. After the claim investigation period, if the payout event is still true, the Shield Mining contract is liquidated and ETH is claimable by pxtoken holders.|