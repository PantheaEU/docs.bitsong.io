# Evidence

Evidence is an implementation of a Cosmos SDK module, per [ADR 009](https://docs.cosmos.network/master/docs/architecture/adr-009-evidence-module.html), that allows for the submission and handling of arbitrary evidence of misbehavior such as equivocation and counterfactual signing.

The evidence module differs from standard evidence handling which typically expects the underlying consensus engine, e.g. Tendermint, to automatically submit evidence when it is discovered by allowing clients and foreign chains to submit more complex evidence directly.

All concrete evidence types must implement the `Evidence` interface contract. Submitted `Evidence` is first routed through the evidence module's `Router` in which it attempts to find a corresponding registered `Handler` for that specific `Evidence` type. Each `Evidence` type must have a `Handler` registered with the evidence module's keeper in order for it to be successfully routed and executed.

Each corresponding handler must also fulfill the `Handler` interface contract. The `Handler` for a given `Evidence` type can perform any arbitrary state transitions such as slashing, jailing, and tombstoning.
