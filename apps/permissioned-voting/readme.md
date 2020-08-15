# Permissioned Voting

Permissioned Voting is an Aragon app offering a checkpointed ERC20 token interface that is usable in Aragon Voting applications. Its purpose is to restrict voting to holders of a Membership Token, while using the balance of a transferable token as the voting weight. This is usefull when you want to restrict governance to members of a Guild who also have a publicly tradable share token.

Accounts that have stake in any of the underlying sources will be represented by this app, allowing them to forward actions or vote in an attached Voting instance.

<br>

## 🚨 Security review status: audited

The `PermissionedVoting` contract is a fork of [VotingAggregator](https://github.com/aragonone/voting-connectors/blob/master/apps/voting-aggregator/contracts/VotingAggregator.sol#L311) contract. 

`VotingAggregator` was [last professionally audited in 2020-01](../../AUDIT.md).

Permissioned Voting changes [line 311](https://github.com/aragonone/voting-connectors/blob/master/apps/voting-aggregator/contracts/VotingAggregator.sol#L311) from

```
311| aggregate = aggregate.add(weight.mul(value));
```
to
```
311| aggregate = aggregate.mul(weight.mul(value));
```


This version was published to aragonPM as `permissioned-voting.open.aragonpm.eth`.

## Caveats

The same checkpointing caveats from the [Token Wrapper](../token-wrapper/) apply to the Permissioned Voting. Aggregated token amounts are limited to `uint192`.

## Installation instructions

The installation instructions are fairly similar to the [Token Wrapper](../token-wrapper) as well, and you can generally substitute any instructions for the Token Wrapper for the Permissioned Voting.

The main changes are the initialization parameters and permissions.

The Permissioned Voting's initialization parameters:

- Permissioned Voting's "token" name
- Permissioned Voting's "token" symbol
- Permissioned Voting's "token" display decimals

And the role you should use when assigning a permission is:

- `ADD_POWER_SOURCE_ROLE`
