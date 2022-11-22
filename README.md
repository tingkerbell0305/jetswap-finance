# PancakeSwap v2 Subgraph

[PancakeSwap](https://pancakeswap.finance/) is a decentralized protocol for automated token exchange on Binance Smart Chain.

This subgraph dynamically tracks any pair created by the uniswap factory. It tracks of the current state of PancakeSwap contracts, and contains derived stats for things like historical data and USD prices.

- aggregated data across pairs and tokens,
- data on individual pairs and tokens,
- data on transactions
- data on liquidity providers

#### UniswapFactory

Contains data across all of PancakeSwap v2. This entity tracks important things like total liquidity (in ETH and USD, see below), all time volume, transaction count, number of pairs and more.

#### Token

Contains data on a specific token. This token specific data is aggregated across all pairs, and is updated whenever there is a transaction involving that token.

#### Pair

Contains data on a specific pair.

#### Transaction

Every transaction on PancakeSwap is stored. Each transaction contains an array of mints, burns, and swaps that occured within it.

#### Mint, Burn, Swap

These contain specifc information about a transaction. Things like which pair triggered the transaction, amounts, sender, recipient, and more. Each is linked to a parent Transaction entity.

## Example Queries

### Querying Aggregated PancakeSwap Data

This query fetches aggregated data from all Pancakeswap pairs and tokens, to capture activity throughout the entire protocol.

```graphql
{
  uniswapFactories(first: 1) {
    pairCount
    totalVolumeUSD
    totalLiquidityUSD
  }
}
```
