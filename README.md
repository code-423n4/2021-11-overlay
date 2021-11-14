# ✨ So you want to sponsor a contest

This `README.md` contains a set of checklists for our contest collaboration.

Your contest will use two repos:
- **a _contest_ repo** (this one), which is used for scoping your contest and for providing information to contestants (wardens)
- **a _findings_ repo**, where issues are submitted.

Ultimately, when we launch the contest, this contest repo will be made public and will contain the smart contracts to be reviewed and all the information needed for contest participants. The findings repo will be made public after the contest is over and your team has mitigated the identified issues.

Some of the checklists in this doc are for **C4 (🐺)** and some of them are for **you as the contest sponsor (⭐️)**.

---

# Contest setup

## 🐺 C4: Set up repos
- [X] Create a new private repo named `YYYY-MM-sponsorname` using this repo as a template.
- [ ] Get GitHub handles from sponsor.
- [ ] Add sponsor to this private repo with 'maintain' level access.
- [X] Send the sponsor contact the url for this repo to follow the instructions below and add contracts here.
- [ ] Delete this checklist and wait for sponsor to complete their checklist.

## ⭐️ Sponsor: Provide contest details

Under "SPONSORS ADD INFO HERE" heading below, include the following:

- [X] Name of each contract and:
  - [X] lines of code in each
  - [X] external contracts called in each
  - [X] libraries used in each
- [X] Describe any novel or unique curve logic or mathematical models implemented in the contracts
- [ ] Does the token conform to the ERC-20 standard? In what specific ways does it differ?
- [ ] Describe anything else that adds any special logic that makes your approach unique
- [X] Identify any areas of specific concern in reviewing the code
- [ ] Add all of the code to this repo that you want reviewed
- [ ] Create a PR to this repo with the above changes.

---

# ⭐️ Sponsor: Provide marketing details

- [ ] Your logo (URL or add file to this repo - SVG or other vector format preferred)
- [ ] Your primary Twitter handle
- [ ] Any other Twitter handles we can/should tag in (e.g. organizers' personal accounts, etc.)
- [ ] Your Discord URI
- [ ] Your website
- [ ] Optional: Do you have any quirks, recurring themes, iconic tweets, community "secret handshake" stuff we could work in? How do your people recognize each other, for example?
- [ ] Optional: your logo in Discord emoji format

---

# Contest prep

## 🐺 C4: Contest prep
- [X] Rename this repo to reflect contest date (if applicable)
- [X] Rename contest H1 below
- [X] Add link to report form in contest details below
- [X] Update pot sizes
- [X] Fill in start and end times in contest bullets below.
- [X] Move any relevant information in "contest scope information" above to the bottom of this readme.
- [ ] Add matching info to the [code423n4.com public contest data here](https://github.com/code-423n4/code423n4.com/blob/main/_data/contests/contests.csv))
- [ ] Delete this checklist.

## ⭐️ Sponsor: Contest prep
- [ ] Make sure your code is thoroughly commented using the [NatSpec format](https://docs.soliditylang.org/en/v0.5.10/natspec-format.html#natspec-format).
- [ ] Modify the bottom of this `README.md` file to describe how your code is supposed to work with links to any relevent documentation and any other criteria/details that the C4 Wardens should keep in mind when reviewing. ([Here's a well-constructed example.](https://github.com/code-423n4/2021-06-gro/blob/main/README.md))
- [ ] Please have final versions of contracts and documentation added/updated in this repo **no less than 8 hours prior to contest start time.**
- [ ] Ensure that you have access to the _findings_ repo where issues will be submitted.
- [ ] Promote the contest on Twitter (optional: tag in relevant protocols, etc.)
- [ ] Share it with your own communities (blog, Discord, Telegram, email newsletters, etc.)
- [ ] Optional: pre-record a high-level overview of your protocol (not just specific smart contract functions). This saves wardens a lot of time wading through documentation.
- [ ] Designate someone (or a team of people) to monitor DMs & questions in the C4 Discord (**#questions** channel) daily (Note: please *don't* discuss issues submitted by wardens in an open channel, as this could give hints to other wardens.)
- [ ] Delete this checklist and all text above the line below when you're ready.

---

# Overlay Protocol contest details
- $47,500 worth of ETH main award pot
- $2,500 worth of ETH gas optimization award pot
- Join [C4 Discord](https://discord.gg/code4rena) to register
- Submit findings [using the C4 form](https://code423n4.com/2021-11-overlay-protocol-contest/submit)
- [Read our guidelines for more details](https://docs.code4rena.com/roles/wardens)
- Starts November 16, 2021 00:00 UTC
- Ends November 22, 2021 23:59 UTC

This repo will be made public before the start of the contest. (C4 delete this line when made public)

[ ⭐️ SPONSORS ADD INFO HERE ]

# Contest Scope

This contest is open for two weeks to give wardens time to understand the protocol properly. Submissions can only be made in the second week of the contest. Representatives from Overlay will be available in the Code Arena Discord to answer any questions during the contest period. The focus for the contest is to try and find any logic errors or ways to drain funds from the protocol in a way that is advantageous for an attacker at the expense of users with funds invested in the protocol. Wardens should assume that governance variables are set sensibly (unless they can find a way to change the value of a governance variable, and not counting social engineering approaches for this).


# Protocol Overview

Overlay is a protocol that allows users to trade nearly any data stream without the need for traditional counterparties.

The Overlay mechanism allows traders to enter positions by staking Overlay's native token (OVL) as collateral in long or short positions on various data streams offered by the protocol. Data streams are obtained via manipulation-resistant oracles. When a trader exits that same position later, the protocol dynamically mints/burns OVL based on their net profit/loss for the trade to compensate them.

An example: Bob thinks the floor price on PUNK NFTs is not sustainable and will likely go down in ETH terms. He wishes to short the floor. As a trader, Bob enters a short position on the associated Overlay market for the PUNK/ETH floor price feed:

- Bob stakes 100 OVL short at an entry price of 80 ETH for the PUNK/ETH floor

- The PUNK/ETH floor then drops 10 ETH (-12.5%) to 70 ETH over the next week

- Bob unwinds the position to take profit: Overlay mints 12.5 OVL for the PnL and returns a total of 112.5 OVL to Bob for the trade.

If the PUNK floor had gone up 12.5% to 90 ETH, Overlay would burn 12.5 OVL from Bob's stake and return 87.5 OVL back to him.

Overlay V1 Core has three different economic mechanisms to manage the risk associated with excessive inflation of the OVL token supply:

1. Open interest caps: limit the amount of position size a market can take on at any given time

2. Payoff caps: limit the maximum change in price the protocol is willing to honor for any one trade on a market

3. Funding rates: overweight open interest side on a market pays the underweight open interest side to incentivize a drawdown in imbalance over time

To deter front-running the oracle, the protocol adds:

- Bid/ask spread to the price fetched from the oracle feed

- Market impact fee charged on the size of the position entered into

Initial data streams to be offered as markets on Overlay will be Uniswap V3 price feeds and Balancer V2 price feeds (TWAPs).


# Contracts

Contracts under audit are listed below. Any contracts not in this list are to be ignored for this contest.

**overlay-v1-core**

| Contract  | sloc | External Calls | Libraries |
| ------------- | ------------- | ------------- | ------------- |
| OverlayV1Token.sol  | 29  |  | [OpenZeppelin/token/ERC20](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC20/ERC20.sol), [OpenZeppelin/access](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/access/AccessControlEnumerable.sol)  |
| OverlayV1UniswapV3Market.sol  | 307  | UniswapV3Pool  | [BalancerV2/utils/math/FixedPoint](https://github.com/balancer-labs/balancer-v2-monorepo/blob/master/pkg/solidity-utils/contracts/math/FixedPoint.sol), [UniswapV3-periphery/libraries/OracleLibrary](https://github.com/Uniswap/v3-periphery/blob/main/contracts/libraries/OracleLibrary.sol) |
| collateral/OverlayV1OVLCollateral.sol  | 337  |  OverlayV1Mothership, OverlayV1Token  | [OpenZeppelin/token/ERC1155](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC1155/extensions/ERC1155Supply.sol)  |
| market/OverlayV1Comptroller.sol  | 371  |  | [OpenZeppelin/utils/math](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/math/Math.sol) |
| market/OverlayV1Governance.sol  | 96  | OverlayV1Mothership  |  |
| market/OverlayV1Market.sol  | 106  | OverlayV1Mothership  | [BalancerV2/utils/math/FixedPoint](https://github.com/balancer-labs/balancer-v2-monorepo/blob/master/pkg/solidity-utils/contracts/math/FixedPoint.sol) |
| market/OverlayV1OI.sol  | 107  |  | [BalancerV2/utils/math/FixedPoint](https://github.com/balancer-labs/balancer-v2-monorepo/blob/master/pkg/solidity-utils/contracts/math/FixedPoint.sol) |
| market/OverlayV1PricePoint.sol  | 88  |  | [BalancerV2/utils/math/FixedPoint](https://github.com/balancer-labs/balancer-v2-monorepo/blob/master/pkg/solidity-utils/contracts/math/FixedPoint.sol), [OpenZeppelin/utils/math](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/math/Math.sol) |
| mothership/OverlayV1Mothership.sol  | 124  |  | [OpenZeppelin/access](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/access/AccessControlEnumerable.sol)  |
| libraries/Position.sol  | 292  |  | [BalancerV2/utils/math/FixedPoint](https://github.com/balancer-labs/balancer-v2-monorepo/blob/master/pkg/solidity-utils/contracts/math/FixedPoint.sol), [OpenZeppelin/utils/math](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/math/Math.sol) |


## Modules

See [docs/module-system.md](https://github.com/overlay-market/overlay-v1-core/blob/main/docs/module-system.md) in the `overlay-market/overlay-v1-core` repo for a detailed explanation of module interactions. Module system diagram in [docs/module-system.pdf](https://github.com/overlay-market/overlay-v1-core/blob/main/docs/module-system.pdf).

V1 Core relies on four modules:

- Collaterals Module
- Markets Module
- OVL Module
- Mothership Module


### Collaterals Module

Collaterals module consists of collateral managers specializing in different types of collateral. Trader interactions with the system occur through collateral managers.

Traders deposit collateral to the specific collateral manager supporting their collateral type. The collateral manager subsequently enters open interest on the market the trader wishes to enter a position on. On exit, collateral managers remove open interest from the market and return collateral to the trader, adjusting for PnL associated with the position. Positions are issued as shares of an ERC1155 by the collateral manager.

Collateral managers are given mint and burn permissions on the OVL token and the ability to enter/exit open interest on markets by the mothership contract.


### Markets Module

Markets module consists of markets on different data streams. Traders do not interact directly with the market contract. Only collateral managers are permitted to interact with market contracts, in order to enter or exit open interest on a market.

Each market inherits from `OverlayV1Market.sol` and tracks:

- Total open interest outstanding on long and short sides. In `OverlayV1OI.sol`:
```
uint256 internal __oiLong__; // total long open interest
uint256 internal __oiShort__; // total short open interest
```
- Accumulator snapshots for how much of the open interest cap has been entered into in the past. In `OverlayV1Comptroller.sol`:
```
Roller[60] public impactRollers;
```
- Accumulator snapshots for how much OVL has been printed in the past. In `OverlayV1Comptroller.sol`:
```
Roller[60] public brrrrdRollers;
```
- Historical prices fetched from the oracle. In `OverlayV1PricePoint.sol`:
```
// mapping from price point index to realized historical prices
PricePoint[] internal _pricePoints;
```
- Collateral managers approved by governance to add/remove open interest. In `OverlayV1Governance.sol`:
```
mapping (address => bool) public isCollateral;
```


### OVL Module

OVL module consists of an ERC20 token with permissioned mint and burn functions. Upon initialization, collateral managers are given permission to mint and burn OVL to compensate traders for their PnL on market positions.


### Mothership Module

Mothership module consists of a mothership contract through which governance can add or remove markets and collateral managers. Access control roles for governance to tune per-market risk parameters are also defined on the mothership contract.


# Mathematical Models

Updated whitepaper with underlying math can found [here](https://drive.google.com/file/d/1I8uGHwMBg8bPJ4eYrG-5U_WNIDN73TyN/view?usp=sharing).

It is most concerned with addressing the question of how to set risk parameters for each market. In particular, setting governance variables in the general `OverlayMarket.sol` contract for:

- `k`: funding constant
- `pbnj`: bid/ask static spread
- `lmbda`: market impact
- `staticCap`: open interest cap
- `priceFrameCap`: payoff cap
- `brrrrdExpected`: expected worst-case inflation rate

Original whitepaper outlining the vision for the protocol is [here](https://drive.google.com/file/d/1Jhpah-KPvX1C9bxPKxiorxsXmgT8LuMd/view?usp=sharing).


## Profit and Loss

The value of a position that the collateral manager needs to return at unwind is

```
V = OI - D +/- OI * ( priceFrame - 1 )
```

where

- `OI` is the current open interest associated with the position. This can change in time due to funding payments.
- `D` is the debt associated with the position. This is static.
- `priceFrame` is the ratio of the exit price divided by the entry price

The PnL for a position that the collateral manager needs to either mint or burn at unwind is

```
PnL = V - C
```

where `C` is the initial collateral deposited, adjusted for trading fees and market impact.

If `pos.isLong = true`:

```
priceFrame = min(exitPrice / entryPrice, priceFrameCap)
```

- `+/- = +`
- `exitPrice = pricePoint.bid`
- `entryPrice = pricePoint.ask`

and if `pos.isLong = false`:

```
priceFrame = exitPrice / entryPrice
```

- `+/- = -`
- `exitPrice = pricePoint.ask`
- `entryPrice = pricePoint.bid`


### Fees

Market impact and trading fees are charged on the notional amount of the position.

#### build

On `build()`, notional amount on which fees are charged is `collateral * leverage`. Market impact and trading fees adjust the collateral amount backing a position

```
collateralAdjusted = collateral - impactFee - tradeFee
```

Open interest and debt associated with the position then use the adjusted collateral amount

```
oiAdjusted = collateralAdjusted * leverage;
debtAdjusted = oiAdjusted - collateralAdjusted;
```

for position attributes.

#### unwind

On `unwind()`, notional amount on which trading fees are charged is

```
NO = V + D
```

where
- `V` is the value of the position
- `D` is the debt

Value returned on unwind is adjusted only for trading fees (no impact on unwind):

```
valueAdjusted = V - NO * feeRate
```


## Funding Payments

```
OI_imb(m) = OI_imb(0) * (1 - 2*k) ** (m)
```

## Pricing


### Bid-Ask Spread

pbnj

### Market Impact

lmbda

## Open Interest Caps

Q



# Tokens

There are two token contracts used. Both inherit from the OpenZeppelin library.

`OverlayToken.sol` (ERC-20)
- Extends OpenZeppelin ERC-20 implementation for permissioned mint and burn functionality
- Defines `MINTER_ROLE` and `BURNER_ROLE` access permissions, with associated modifiers on `mint()` and `burn()` external functions

`OverlayV1OVLCollateral.sol` (ERC-1155)
- Extends OpenZeppelin ERC-1155 implementation


# Areas of Concern

- Oracle attacks: front-running, manipulation
- Robustness of economic mechanisms: whether our risk framework will work in practice
- Gas optimizations: the most important flows are `build()` and `unwind()` on the collateral manager
- General failure of our mechanisms and constructs in Solidity — price fetching, rolling oi cap accounting, composure of our smart contract system (governance contracts, market contract integration with collateral manager)
- Collateral managers and the logic within, as all collateral will be held in there while users have an active position

If wardens are unclear on which areas to look at or which areas are important please feel free to ask in the contest Discord channel.


# Tests

Existing tests are provided in the repo. Tests use a Uniswap mock loaded in `conftest.py` with historical observations from Uniswap V3 `AXS/WETH` and `DAI/WETH` pools.


## Requirements

To run the project you need:

- Python >=3.7.2 local development environment
- [Brownie](https://github.com/eth-brownie/brownie) local environment setup
- Set env variables for [Etherscan API](https://etherscan.io/apis) and [Infura](https://eth-brownie.readthedocs.io/en/stable/network-management.html?highlight=infura%20environment#using-infura): `ETHERSCAN_TOKEN` and `WEB3_INFURA_PROJECT_ID`
- Local Ganache environment installed


## Compile

```
brownie compile
```


## Test

```
brownie test
```
