# Protekt Contracts
Protekt contracts are configurable insurance contracts that create a P2P market for cover and liability on top of ANY smart contract, whether it's a lending pool, market making pool, staking pool, etc. Each contract conforms to the same generalizable interface so that entering/exiting the market, fee pricing, and submitting claims is consistent and can be snapped together with other money legos.

For more on Protekt Contracts, [check out the explainer page](/aboutProtektContracts.md).

## Current Protekt Contracts
| Name | Status |
|---------|----------|
|[Comp-DAI Manual Liability](/compound-DAI-manual-market.md)|⌛In Progress|

## Modules

### Fee Models
| Multi-sig wallet | FeeModelAutoCompoundDAI |
|---------|----------|
|✅Done|📆Planned|

### Investment Strategy
| StrategyHodl | StrategyCompoundDAI | StrategyMakerDSR | StrategyUniswapWETH |
|---------|---------|---------|---------|
|✅Done|📆Planned|📆Planned|📆Planned|

### Claims Manager
| ClaimsManagerSingleAccount | ClaimsManagerAutoCompoundDAI | ClaimsManagerNexusClaimsAssessor |
|---------|---------|---------|
|✅Done|📆Planned|📆Planned|

### ShieldToken Withdrawals
| PausableWithdrawals | LockUpWindowWithdrawals | ThrottledWithdrawals | FeeWithdrawals |
|---------|---------|---------|---------|
|⌛In Progress|📆Planned|📆Planned|📆Planned|

## Architecture
![Smart](/img/smartContractArchitecture.png)