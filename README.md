![Banner](/img/banner.jpg)

# Protekt Protocol
Protekt Protocol puts crypto to work insuring users against hacks, bugs, and other exploits of any DeFi protocol. Just as [Uniswap](https://uniswap.org/) allows any token to have a spot market, Protekt allows any smart contract to be insured by stakers. The goal is to support and catalyze the growth of the DeFi ecosystem by protecting users from getting rekt.

Along with being a smart contract protocol, an allocation of protocol treasury will be used for grants to continually audit and secure other DeFi money legos, so the ecosystem can all grow safely together!

**Repos**
* [Smart Contracts](https://github.com/corbinpage/protekt-protocol-contracts)
* [Frontend](https://github.com/corbinpage/protekt-fe)

## DeFi Risk
Building on the work of awesome projects like [DeFi Score](https://defiscore.io/), [Nexus Mutual](https://nexusmutual.io/), [Aave's Safety Modules](https://docs.aave.com/aavenomics/safety-module), and others, we believe that large technical vulnerabilities are the **biggest risk to a thriving DeFi community** over the next few years. Smart contracts that contain large amounts of value face the following risks:
1. Smart Contract Risk - Technical bugs that can expose funds to hackers
2. Centralization Risk - Centralized admin keys are stolen or used nefariously or oracles are manipulated to allow an exploit
3. Financial Risk - Collateral falls below outstanding obligations, likely due to price movement, or low liquidity leads to locked funds

Especially as new money legos are created, snapped together, and remixed weekly, the risks multiply and become a bottleneck to more capital flowing into the space. New entrants need signaling and assurance of the projects they can trust and commit capital as well as recapitalization if a [Shortfall Event](https://docs.aave.com/aavenomics/terminology#shortfall-event-se) occurs.

To fulfill this need, Protekt Protocol introduces a new insurance marketplace with several innovative features:
* 📜 ANYONE can back ANY capital pool with a composable insurance contract
* 💸 Insurees can mint wrapped tokens with built in coverage (never "buy cover")
* 🛡 Stakers (shield miners) deposit capital to assume liability and earn rewards
* 🔀 Configurable claims process via automated rules or a DAO
* 🏦 Payouts trigger a liquidation waterfall to spread risk through tranches

The protocol  was inspired and uses money legos from yearn, Aave, Compound, Balancer, Maker, rDAi, Nexus, and others. The very best in DeFi.

## How it works
Similar to how [Uniswap](https://uniswap.org/) allows any token to have a spot market, Protekt Protocol allows any smart contract to be backed by a **Protekt contract**, which creates a market for the risk of lost assets held by the smart contract.

When setting up the [Protekt contract](/docs/protektContracts.md), the user specifies an asset (DAI, ETH, USDC, etc.) and an underlying pool, which can be a lending pool, market making pool, staking pool, multi-sig wallet, etc. They also specify the fee model and rules for triggering and evaluating a claim. Once launched, insurees get coverage by minting **pTokens** and shield miners stake assets and earn rewards for assuming the risk of getting liquidated.

**Protekt Protocol is a generalized and open version of the risk management systems built into Maker and Aave but can back any capital pool by anyone.**

![Protocol Comparison Diagram](/img/ProtocolComparisonDiagram.png)

### pTokens, like cTokens but with cover
pTokens wrap shares in a DeFi pool (lending pool, AMM LP shares, etc.) and cover the deposits in return for an extracted fee to reward the shield miners. Let's look at an example:

Users can deposit Dai that gets forwarded into the Compound cDAI pool and get pTokens (pcDAI) in return. pcDAI represents your underlying cDAI 1:1 plus 80% of the COMP farming rewards, while the other 20% goes to the shield miners as rewards. This fee is the user's ongoing "premium" for purchasing cover. pTokens can be minted at any time and redeemed for your cTokens + adjusted COMP rewards at any time.

**In short, by holding a pToken, you pay 20% of your yield farming returns to be insured against hacks and smart contract bugs in the underlying capital pool.**

![pToken Image](/img/pTokenDiagram.png)

### Protekt Contracts
[Protekt contracts](/docs/protektContracts.md) are configurable insurance markets that can be set up on top of any smart contract. Upon launching the contract, the creator specifies:
* Underlying asset and capital pool
* Fee model
* Shield mining asset and investment strategy
* Claims Manager (a programmatic smart contract or a DAO)

Fee models, investment strategy, and the claims process are each configurable but must conform to the same interface. Users can search for the best contract to meet their goals, and stakers can stake capital on the capital pools they are confident in. If a payout event occurs, any insuree can `submitClaim()` and kick off the claims process, which can be managed by programmatic rules, a DAO, or a centralized party.

![Protekt Pool Image](/img/ProtektPool.png)

### The PKT Mothership Pool
The PKT Mothership is the backstop that covers all Protekt pools up to certain thresholds, governs which underlying pools are added and when, and will eventually earn cashflow. New Protekt pools can only be added through the Mothership. She creates life and gives security.

![Full Protocol Image](/img/ProtektProtocolDiagram.png)

## The PKT Token
The PKT token is the governance and rewards token of the Protekt Protocol. It will be used to stake for assuming protocol liability, make governance decisions, receive rewards from protocol fees, provided as protocol incentives, and used to fund grants and audit reports for DeFi protocols that are covered by Protekt.

### Protocol Incentives (Yield Farming)
Every Wednesday, new rounds of PKT will be claimable by those providing capital or work into the protocol. Tasks that earn weekly PKT include:
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
* [Telegram](https://t.me/protektdefi) for discussions
* [Snapshot (Coming Soon)](/) for governance
* [Github](https://github.com/corbinpage/protekt-protocol-docs) for code & docs