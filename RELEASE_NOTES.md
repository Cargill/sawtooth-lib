# Release Notes

## Changes in libsawtooth 0.6.0

### Highlights
- Replace the `sawtooth::signing` module with the `cylinder` library, which
  provides a similar interface and implementations.
- Replace the execution platform with Transact.

### Experimental Changes
- Create a Sawtooth client to handle communications with the REST API.
  Implements a function which lists all existing batches returned from the REST
  API and get a specific batch. This feature is currently behind an experimental
  feature `client`.

### Other Changes
- Rework ChainController so it does not require `light_clone`. The
  `BlockValidator` has also been updated to return a `ChainControllerRequest` on
  block validation instead of the `BlockValidationResult` directly.
- Rewrite `validation rule enforcement` into a struct. This struct allows the
  block to be validated as it's constructed.
- Implement the "block info" batch injector in Rust.
- Update `PendingBatchPool` to use `BatchPair`s and change the update method to
  take a set of published batch IDs; while this implementation is potentially
  less efficient, it is more correct.
- Update `PermissionVerifier` to use `BatchPair`s.
- Add `CborMerkleState` for reading/writting cbor encoded state. This is
  required for backwards compatibility with Sawtooth state.
- Update `BlockValidator` to use Transact's execution transaction platform.
- Move the `BlockValidator` start/stop into the ChainController. This removes
  the requirement to need to clone the `BlockValidator`.
- Implement the GenesisController in Rust. The GenesisController now uses
  Transact's execution platform.
- Implement the `BlockPublisher` in Rust
- Remove the `TransactionCommitCache`, which is no longer be used by the block
  publisher.
- Remove the `CandidateBlock` trait, which has been replaced by an internal
  struct in the block publisher.
- Update the `ChainController::build_fork` method to return `BatchPair`s instead
  of `Batch`es.
- Move the `ChainHeadLock` to the publisher module since it's specific to the
  block publisher.
- Remove the `ExecutionPlatform` and `Scheduler` traits, since they are no
  longer used due to the Transact integration.


## Changes in libsawtooth 0.5.0

* Add the `protocol::block` module that provides the block protocol for
  Sawtooth, including protobuf conversions and a builder
* Remove the batch and transaction structs from Sawtooth and use the
  corresponding structs from Transact's protocols


## Changes in libsawtooth 0.4.0

* Add the `protocol` module with native setting and identity protocol structs
  and update code to use these structs instead of the corresponding protobufs
* Replace internal state and database implementations with implementations
  provided by Transact and remove the `database` module
* Add a permission verifier implementation that replaces the trait in the
  `gossip` module, use it for block validation, and remove the `gossip` module
  since it is now empty
* Make minor corrections and updates to Jenkins files


## Changes in libsawtooth 0.3.0

* Update transact dependency to 0.2, which enables storing the results of
  invalid transactions as transaction receipts
