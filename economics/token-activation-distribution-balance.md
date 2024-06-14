
### Designing Token

[Work tokens](https://x.com/ViktorBunin/status/1785000852375109848) are created with objective faults in mind. They are typically provided to those that offer some specialized service to a network and also grant the ability to punish adversarial members. Currently, one primary model for work tokens is specialized objective work tokens. These tokens can only be used for a limited scope of tasks, and the completion or neglect of the task above must be [attributable](https://x.com/ViktorBunin/status/1785000852375109848) onchain. For example, ETH is allotted to those who validate or delegate to secure the network. It also grants the ability to punish adversarial members via slashing if they submit invalid transactions.

### Liquidity

* Maximum supply: the maximum number of tokens that can ever exist
* Total supply: the total number of tokens that have been created
* Circulating supply: the tokens currently available for trading

---
### Distribution

#### Airdrop Mechanism
Designing an effective airdrop mechanism is challenging and almost an art form. Key considerations should include: 
• Who to reward 
• The value attributed to their efforts 
• When and how to distribute rewards

Analysis around token strength
* Consistently increase new holders count
* More new buyers than recurring ones
* Minimal presence of whales

Balancing incentivization
* Metcalfe's Law
* Understand quasi hyperbolic discounting model
* Beat Initial Selloff with time-delay mechanism

#### Prevent Sybil Farming

Preventing sybil attacks to ensure
- Unfair Distribution of Tokens: Sybil attackers amass a large portion of the airdropped tokens, leaving less for genuine users who might be more interested in using and supporting the project long-term.
- Reduced Project Legitimacy: Airdrops affected by Sybil attacks can damage the project’s reputation and make it look like they’re just trying to inflate the token supply.
- Price Manipulation: If Sybil attackers dump a large amount of airdropped tokens on the market, it can cause the token price to plummet, hurting legitimate investors and users.

It will be impossible to weed out sybil attackers completely, there will always be edge cases but the main goal should be to **incentivise ‘strong on-chain’ profile over one or small number of addresses, vs ‘weak on-chain’ profile over many.**

* Multiple round of airdrops
* Reward proportionate to wallet age
* Reward proportionate to gas usage
* More liquidity/volume per address