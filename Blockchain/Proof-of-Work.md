Mining & Proof of Work
===

Blockchain networks, like Ethereum, are essentially distributed and decentralized databases consisting of many nodes (fancy name for computers!).

![blockchain-nodes](https://i.imgur.com/O7jloYu.jpg)

In a decentralized environment, common issues are:

- How do all nodes agree on what the current and future state of user account balances and contract interactions is?
- Who gets to add new blocks/transactions to a chain? How do we know any blocks added are "valid"?
- How the heck are all of these things coordinated without any central actor in place?

The answer is **consensus mechanisms**.

## Consensus Mechanisms

_Consensus_ means coming to a general agreement. **_Blockchain consensus_ typically means at least 51% of nodes are in agreement over the current global state of the network**. Consensus mechanisms end up simply being rules that a distributed + decentralized blockchain network follows in order to stay in agreement over what is considered valid. Remember that consensus mechanisms are inter-changeable and there are many out there that we have yet to cover, like proof-of-stake.

The main consensus rules for proof-of-work typically look like religious commandments:

- You cannot double spend.
- The "longest" chain will be the one the rest of the nodes accept as the one "true" chain, determined by a chain's cumulative work. Also known as **Nakamoto Consensus**.

Bitcoin being a blockchain network, use a consensus mechanism called **proof-of-work**. Ethereum was previously using proof of work but has since moved to **proof-of-stake**. We will not be covering proof of stake here (for now), but in the meantime you can learn more about this transition [here](https://www.alchemy.com/overviews/ethereum-2-0-your-guide-for-2022#transitioning-to-proof-of-stake-2)

## Proof of Work

Proof-of-work is the consensus mechanism that allows decentralized networks like Bitcoin and (previously) Ethereum to come to consensus, or agree on things like account balances and the order of transactions. This prevents users from "double spending" their coins and ensures that everyone is following the rules, making proof-of-work-based networks resistant to attack. The consensus mechanism ends up providing security to a blockchain network just because it demands that everyone follow the consensus rules if they want to participate!

In proof-of-work, **mining** is the "work" itself.

## Mining

**Mining** is process of creating a block of transactions to be added to a blockchain.

But how does that tie in to proof-of-work? Well, proof-of-work could just as well be called proof-of-mining!

> "Mining" can be considered an industry misnomer. The term gained popularity as it has a close tie in to gold mining, where miners expend energy and resources in the pursuit of valuable rewards.

In proof-of-work consensus, nodes in the network continuously attempt to extend the chain with new blocks - these are the **miners**, nodes that contain mining software. Miners are in charge of extending a blockchain by adding blocks that contain "valid" transactions. In order to add a block, the network will ask miners for their 'proof-of-work'.

A proof-of-work-based system will typically require miners produce an output in a very difficult-to-get target range. A valid proof-of-work would currently look like this in the Bitcoin network:

> 000000000000000000043f43161dc56a08ffd0727df1516c987f7b187f5194c6

How the heck does a miner get an output like this right!? Well, the automated mining software has one job: take a piece of data (ie. the prev block header + new transactions to add to a chain) and [hash](https://emn178.github.io/online-tools/sha256.html) it. If the hash output is below a target difficulty, then the miner has found the answer to the puzzle: a valid proof of work.

The proof of work shown above has 19 leading zeroes - that's a ton! :scream: Since the range of each possible character per space is in hexadecimal, this means we have 1/16 character possibilities per space.

The hash outputs for SHA-256 are in hexadecimal which means we have 1/16 possible characters per space - `a-f` in letters and `0-9` in decimals = 16 total possibilities. This means finding one 32-byte SHA-256 output that has just ONE leading zero will take _on average_ 16 tries. [Try it now](https://emn178.github.io/online-tools/sha256.html) with any random input! How many tries did it take you to find an output with one leading zero?

The thing is, once we start adding more difficulty, things start to get more difficult. Finding an output with 2 leading zeroes increases the average attempts to 256 - 16 possible characters in the first spot * 16 possible characters in the second spot. Finding 19 leading zeroes will take, on average, `75557863725914323419136000000000000000000000` attempts.

Proof-of-work networks will typically have some sort of `target_difficulty`. In order for a miner to add a new block, they must find a proof-of-work lower than the network target difficulty. It's basically the network saying: "If you want to add a new block, you must provide a proof-of-work with 12 leading zeroes." The way the math works, finding such a difficult-to-find output is proof enough that a miner expended considerable resources to secure the network. There is no way to cheat the system, you either have a valid proof of work or you don't.

Here's what the proof-of-work mining algorithm looks like:

1. Take current block’s block header, add mempool transactions
2. Append a nonce, starting at nonce = 0
3. Hash data from #1 and #2
4. Check hash versus target difficulty (provided by protocol)
5. If hash < target, puzzle is solved! Get rewarded.
6. Else, restart process from step #2, but increment nonce![](https://cdn.dribbble.com/users/1498581/screenshots/4127416/cryptocurrency_mining_mov.gif)

The miner nodes in a proof-of-work network will perform this algorithm regularly. This gives the network a way to recognize the true state and validity of proposed transactions via following of the consensus rules. As long as a majority of nodes on the network follow the consensus rules, the blockchain remains secure and resistant to attacks, ensuring that only valid and verified transactions are added to the distributed ledger, thus maintaining its integrity and trustworthiness.

Why do miners expend resources to secure a proof-of-work blockchain network like Ethereum or Bitcoin? In exchange for the large amounts of energy and hardware upkeep required to run mining software, miners receive currency as a reward. If the consensus rules are followed, making a secure network, miners get paid.

## Conclusion

In proof-of-work, miners must present a proof (in the form of a hash output on valid input data) that they expended energy in order to successfully "mine" a block and have it extend a blockchain.
