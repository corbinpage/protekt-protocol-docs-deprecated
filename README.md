![Banner](/img/banner.jpg)

# Protekt Protocol
Protekt Protocol puts crypto to work insuring users against hacks, bugs, and exploits of any DeFi protocol. Just as [Uniswap](https://uniswap.org/) allows any token to have a spot market, Protekt allows any smart contract to be insured by stakers. The goal is to support and catalyze the growth of the DeFi ecosystem by protecting users from getting rekt.

Along with being a smart contract protocol, an allocation of protocol treasury will be used for grants to continually audit and secure other DeFi money legos, so the ecosystem can all grow safely together!

## DeFi Risk
Building on the work of awesome projects like [DeFi Score](https://defiscore.io/), [Nexus Mutual](https://nexusmutual.io/), [Aave's Safety Modules](https://docs.aave.com/aavenomics/safety-module), and others, we believe that large technical and financial vulnerabilities are the **biggest risk to a thriving DeFi community** over the next few years. Smart contracts that contain large amounts of value face the following risks:
1. Smart Contract Risk - Technical bugs that can expose funds to hackers
2. Financial Risk - Collateral falls below outstanding obligations, likely due to price movement, or low liquidity leads to locked funds
3. Centralization Risk - Centralized admin keys are stolen or used nefariously or oracles are manipulated to allow an exploit

Especially as new money legos are created, snapped together, and remixed weekly, the risks multiply and become a bottleneck to more capital flowing into the space. New entrants need signaling and assurance of the projects they can trust and commit capital as well as recapitalization if a [Shortfall Event](https://docs.aave.com/aavenomics/terminology#shortfall-event-se) occurs.

To fulfill this need, Protekt Protocol introduces a new insurance marketplace with several innovative features:
* 📜 ANYONE can back ANY capital pool with a composable insurance contract
* 💸 Insurees can mint wrapped tokens with built in coverage (never "buy cover")
* 🛡 Stakers deposit capital (shield mining) to assume liability and earn rewards
* 🔀 Configurable claims process via automated rules or a DAO
* 🏦 Payouts trigger a liquidation waterfall to spread risk through tranches

The protocol  was inspired and uses money legos from yearn, Aave, Compound, Balancer, Maker, rDAi, and others. The very best in DeFi.

## How it works
Similar to how Uniswap allows any token to be added, Protekt Protocol allows any smart contract to be backed by a Protekt contract, making a market on the risk of hacks, bugs, and exploits via configurable rules.

[Graphic showing different contracts](/)


### pTokens, like cTokens but with cover
Users can deposit Dai that gets forwarded into the Compound cDAI pool and get pTokens in return. The pToken represents your underlying cToken 1:1 plus 90% of the COMP farming rewards, while the other 10% goes to the Protekt pool stakers as rewards. This fee is the user's ongoing "premium" for purchasing cover. pTokens can be minted at any time and redeemed for your cTokens + adjusted COMP rewards at any time.

**In short, by holding a pToken, you pay 10% of your yield farming returns to be insured against hacks, bugs, and exploits of the underlying capital pool.**

![pToken Image](/img/pTokenDiagram.png)

### Protekt contracts
Protekt contracts are configurable insurance contracts that can be set up on top of ANY DeFi pool, whether it's a lending pool, market making pool, staking pool, etc. Users can point the contract at any Ethereum address, define the rules that trigger an incident, set the fees, and specify how the staking funds are managed and paid. Then anyone can mint pTokens by joining the pool and obtain coverage on their assets.

Stakers can add capital to the Protekt contract to cover the liability of the underlying pool from a Shortfall event and earn a portion of the yield farming rewards in return. Stakers should only stake on capital pools they are confident are secure and can ask for audits, reviews, timelocks, etc before depositing value.

![Protekt Pool Image](/img/ProtektPool.png)

### The PKT Mothership Pool
The PKT Mothership is the backstop that covers all Protekt pools, governs which underlying pools are added and when, and will eventually earn cashflow. New Protekt pools can only be added through the Mothership. She creates life and gives security.

![Full Protocol Image](/img/ProtektProtocolDiagram.png)

## Claims & Liquidations

### Claims
All these Shortfall Events result in collateral that falls below the protocol's obligations for a sustained period of time. Market making pools, staking pools, wallets, exchanges, and other accounts can be programmatically checked for incidents as well. So Protekt pool provides a common interface for submitting claims, investigation, resolution, and payouts, but the implementation is left up to the pool creator.

**In short, each insurance contract follows the same claims process but can be executed via programmatic rules, a DAO, or centralized party.**

### Liquidations
If a claim is successfully made, the payouts will be made by liquidating the Protekt pool and, if necessary, the PKT Mothership Pool. This structure was inspired by a [distribution waterfall ](https://en.wikipedia.org/wiki/Distribution_waterfall) so that multiple buckets of capital can be set up to assume different amounts of liability to the underlying pool. Payouts can be made via [payment-in-kind](https://www.investopedia.com/terms/p/paymentinkind.asp) or swapped and distributed in a monetary asset like ETH, DAI, or USDC.

## The PKT Token
The PKT token is the governance and rewards token of the Protekt Protocol. It will be used to stake for assuming protocol liability, make governance decisions, receive rewards from protocol fees, provided as protocol incentives, and used to fund grants and audit reports for DeFi protocols that are covered by Protekt.

### Protocol Incentives (Yield Farming)
Every Wednesday, new rounds of PKT will be claimable by those providing capital or work into the protocol. PKT can't be bought, only earned. Tasks that earn weekly PKT include:
* Staking in a Protekt pool
* Staking ETH or PKT in the Mothership Vault
* Rewards for fulfilling open grants
* Rewards for creating audit reports on other DeFi protocols

### Governance
Governance will start and end with the Protekt community. The community will not only be PKT holders but also the hackers, devs, auditors, analysts, and actuaries that contribute their blood, sweat, and tears to DeFi. They will be the ones to propose coverage of new DeFi pools, adjust and critique settings, and keep DeFi safe at night. The protocol will maintain some level of centralization at the beginning so it can iterate quickly but will pursue a pathway of [progressive decentralization](https://a16z.com/2020/01/09/progressive-decentralization-crypto-product-management/) over time.

### Community
Protekt protocol's ultimate mission is to provide a service that makes DeFi safer so that the ecosystem can grow its capital, participants, and impact. Along with the smart contract protocol, we hope to foster a robust and sustainable community of devs, auditors, analysts, hackers, mempool sleuths, and others to continually test, prod, poke the latest DeFi projects to ensure they are safe. A substantial allocation of the protocol treasury will go towards audit reports, battle testing, meetups, and other content and events to foster a safe financial system.

## References
* [Twitter](https://twitter.com/protektprotocol) for announcements
* [Discord (Coming Soon)](/) for discussions
* [Snapshot (Coming Soon)](/) for governance
* [Github](https://github.com/corbinpage/protekt-protocol) for code & docs