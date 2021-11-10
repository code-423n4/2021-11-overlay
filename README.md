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

- [ ] Name of each contract and:
  - [ ] lines of code in each
  - [ ] external contracts called in each
  - [ ] libraries used in each
- [ ] Describe any novel or unique curve logic or mathematical models implemented in the contracts
- [ ] Does the token conform to the ERC-20 standard? In what specific ways does it differ?
- [ ] Describe anything else that adds any special logic that makes your approach unique
- [ ] Identify any areas of specific concern in reviewing the code
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
- Starts November 11, 2021 00:00 UTC
- Ends November 17, 2021 23:59 UTC

This repo will be made public before the start of the contest. (C4 delete this line when made public)

[ ⭐️ SPONSORS ADD INFO HERE ]

# Contest Scope
This contest is open for two weeks to give wardens time to understand the protocol properly. Submissions can only be made in the second week of the contest. Representatives from gro will be available in the Code Arena Discord to answer any questions during the contest period. The focus for the contest is to try and find any logic errors or ways to drain funds from the protocol in a way that is advantageous for an attacker at the expense of users with funds invested in the protocol. Wardens should assume that governance variables are set sensibly (unless they can find a way to change the value of a governance variable, and not counting social engineering approaches for this).

# Novel Maths
Updated Whitepaper with underlying math can found here[https://drive.google.com/file/d/1Jhpah-KPvX1C9bxPKxiorxsXmgT8LuMd/view?usp=sharing](url)

# Protocol Overview
Overlay is a protocol for trading nearly any data stream, long or short, with leverage, using price oracles and a native token (OVL). All PnL is denominated in OVL and the OVL token also serves as the native governance token of the protocol, it gives successful traders even more skin in the game. OVL enables holders to propose new markets on Overlay and determine per-market risk parameters such as trading fees and maximum leverage levels.

# Security Assumptions & Concerns
- Oracle attacks: front-running, manipulation
- Robustness of economic mechanisms: whether our risk framework will work in practice
- General failure of our mechanisms and constructs in solidity — multi leg and historic price fetching, rolling oi cap accounting, composure of our smart contract system (governance contracts, market contract integration with collateral manager), etc)

# Smart Contracts
Solidity: core contracts repo has ~ 1511 lines of code
- OverlayV1Comptroller.sol **(371 sloc)**
- OverlayV1Governance.sol **(96 sloc)**
- OverlayV1OVLCollateral.sol **(337 sloc)**
- OverlayV1Market.sol **(106 sloc)**
- OverlayV1Mothership.sol **(124 sloc)**
- OverlayV1OI.sol **(107 sloc)**
- OverlayV1PricePoint.sol **(88 sloc)**

# Library Contracts
- OpenZeppelin contracts
- Slightly [modified UniswapV3 Oracle library](https://github.com/overlay-market/overlay-v1-core/tree/main/contracts/libraries/UniswapV3OracleLibrary)
- Some particular math library, maybe [FixedPoint library](https://github.com/overlay-market/overlay-v1-core/blob/main/contracts/libraries/FixedPoint.sol) (forked from sushiswap/mirin; which was forked from Uniswap/uniswap-lib), or Balancer's library

# System Diagrams
 - Detailed System Diagrams found [here](https://miro.com/app/board/o9J_l5DRg6A=/?invite_link_id=632214936825)
 - - OVL Collateral Manager contract 
    - Overview
        - Users interact with the collateral manager contract to trade on different Overlay markets
        - Collateral manager contracts have special auth permissions to interact with the market contracts — they are the only ones that can interact w market contracts
        - Inherits from OpenZeppelin's ERC-1155 implementation
    - Interface
        - Build
            - Users deposit collateral to the collateral manager to take out a position on a specified market. Parameters include market, leverage, side (long or short), and collateral amount (of type manager supports)
            - Collateral manager updates open interest (OI) on the specified market contract given side, leverage, and collateral amount
            - Collateral manager issues shares of an ERC-1155 position token to track user's share of open interest on the market
        - Unwind
            - Users supply a position and number of shares to unwind. The protocol figures out the PnL of the position they are unwinding and mints or burns OVL to compensate user for their PnL.
            - Collateral manager returns associated value of the shares (collateral + PnL). Collateral manager burns associated number of shares of the position.
        - Liquidate
            - When a position is liquidatable, meaning the value of the position is beneath the margin maintenance percent, users can liquidate the position, which sets the value of the position to zero, rewards the liquidator a portion of the collateral and sends the rest to the DAO or burns it.
        - Update
            - Calls the update function on a market contract
- Market contract (Uni V3 Price Feed)
    - Overview
        - The Market contracts are responsible for keeping track of open interest, funding and prices. The collateral managers call this contract when they are building or unwinding positions to register/deregister their OI.
    - Interface
        - entryData
            - This provides the data needed to build a position - when a user enters a position. It returns the freeOi (for OI caps), the maximum leverage, the current price point index, and the next compounding epoch. Performs historic updates of prices.
        - enterOI
            - This function queues up the OI determined by the Collateral Manager contract. It remains queued until a compounding period has passed, at which point it is exposed to funding payments.
        - exitData
            - This function provides data needed to unwind and liquidate positions. Right now it returns the total OI, total OI shares, the price frame (ratio of exit/entry price), and the last epoch that was compounded (necessary to discern whether to take OI off of queued OI or fully exposed OI. Performs historic updates of prices.
        - exitOI
            - Exits OI determined by the Collateral Manager contract.
        - Price update functions
            - Internal functions
                - entryUpdate()
                    - Called on entryData(), this function settles any position that needs to be settled and queues an update for the next update epoch.
                - exitUpdate()
                    - Called on exitData(), this function settles any position that needs to have been settled as well as retrieves the price for the current position being exited. Open question if we save that price or not.
            - **External**
                - staticUpdate()
                    - Looks back in time to see if there is a position that needs to be settled and settles it.
