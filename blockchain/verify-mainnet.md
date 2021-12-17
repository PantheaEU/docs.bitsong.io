# Verify Mainnet

Help to prevent a catastrophe by running invariants on each block on your full node. In essence, by running invariants you ensure that the state of mainnet is the correct expected state. One vital invariant check is that no atoms are being created or destroyed outside of expected protocol, however there are many other invariant checks each unique to their respective module. Because invariant checks are computationally expensive, they are not enabled by default. To run a node with these checks start your node with the assert-invariants-blockly flag:

```
bitsongd start --assert-invariants-blockly
```

If an invariant is broken on your node, your node will panic and prompt you to send a transaction which will halt mainnet. For example the provided message may look like:

```
invariant broken:
    loose token invariance:
        pool.NotBondedTokens: 100
        sum of account tokens: 101
    CRITICAL please submit the following transaction:
        bitsongd tx crisis invariant-broken staking supply

```

When submitting a invariant-broken transaction, transaction fee tokens are not deducted as the blockchain will halt (invariant-broken transactions are free transactions).
