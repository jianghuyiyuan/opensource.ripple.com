# AMMClawback

{% partial file="/docs/_snippets/_ammclawback-disclaimer.md" /%}

The `AMMClawback` amendment enables token issuers to claw back tokens from wallets that have deposited into AMM pools, ensuring regulatory compliance. This amendment also changes the behavior of the `AMMCreate` and `AMMDeposit` transactions.


## AMMCreate Changes

Currently, the `AMMCreate` transaction is prohibited if either of the AMM pool's token issuers have enabled the `lsfAllowTrustLineClawback` flag.

XLS-73d permits you to create new AMMs with clawback-enabled tokens.


## AMMDeposit Changes

### Frozen Assets

Currently, if an asset in the AMM pool is frozen (either global or individual) and the paired asset isn't, you can still deposit the unfrozen asset into the AMM pool with `AMMDeposit`.

XLS-73d prohibits a wallet from depositing any tokens (single-sided and double-sided) into an AMM pool if at least one of the pooled assets has been frozen (either individually or globally) by the token issuer.

### Unauthorized Assets

Currently, if an account isn't authorized to hold a token in the AMM pool, it can still make a single-sided deposit of the other token as long as it's authorized for that token.

XLS-73d prevents a wallet from depositing any tokens (single-sided or double-sided) into an AMM pool if the wallet isn't authorized to hold at least one of the assets in the AMM.
