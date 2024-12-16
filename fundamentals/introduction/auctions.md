# Auctions

Auction is the process of finding a solver for user intents. The selected user will then go on to implement the user's intent, ie swap. Garden's auction system ensure that user intents are fulfilled with efficient and competitive pricing.

Garden balances both competition and fairness by leveraging **solver scores** to create a system where solvers are incentivized to optimize their performance while maintaining accountability to their stakers.

## Solver score

&#x20; The solver score combines performance efficiency and vote power to determine a solver's priority in the auction process. It is calculated as:

**Settlement score for a specific chain C:**

$$
\text{Settlement Score}_{C} = \frac{\text{Average Settlement Time}_{C} - \text{Solver's Settlement Time}_{C}}{\text{Standard Deviation}_{C}}
$$

**Weighted settlement score across all chains:**

$$
\text{Weight}_{C} = \frac{\text{Solver Settlements}_{C}}{\text{Total Solver Settlements}}
$$

$$
\text{Settlement Score} = e^{\left(\sum_{C} \left(\text{Weight}_{C} \times \text{Settlement Score}_{C}\right)\right)}
$$

**Final solver score:**

$$
\text{Solver Score} = \left(\frac{\text{Total Volume on Garden} \times \text{Stake Against Solver}}{\text{Volume Filled by Solver} \times \text{Total Staked Amount}}\right) \times \text{Settlement Score}
$$

Solvers with a score great than 1 get priority in the auction. Solver scores are calculated before every auction.

## How does a typical auction work?

1. All solvers submit their quotes for a given intent to the Auction House. Each quote specifies the solver’s proposed execution price for fulfilling the intent.
2. The Auction House identifies the solver with the best price (i.e., the lowest quote).
3. Solvers with a **staker score** higher than the solver with the best quote have a 5-second window to accept the best quote. This mechanism ensures that solvers with higher backing from stakers have the opportunity to get first dibs on intents.
4. The outcome depends on the participation during the acceptance period:

**No one accepts:** The solver with the best quote wins the auction and fills the order.

**One solver accepts:** The solver who accepts the quote gets the order.

<figure><img src="../../.gitbook/assets/solver_one_select.png" alt=""><figcaption></figcaption></figure>

**Multiple sovlers accept:** Among the solvers who accept the best quote, the one with the highest **staker score** wins the auction and fills the order.

<figure><img src="../../.gitbook/assets/solver_multiple_select.png" alt=""><figcaption></figcaption></figure>

