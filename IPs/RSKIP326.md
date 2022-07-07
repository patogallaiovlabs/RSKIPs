# Change btcDestinationAddress format in `release_request_received` event from hash160 to base58

|RSKIP          |326           |
| :------------ |:-------------|
|**Title**      |Change btcDestinationAddress format in `release_request_received` event from hash160 to base58 |
|**Created**    |21-JUNE-22 |
|**Author**     |KI |
|**Purpose**    |Usa |
|**Layer**      |Core |
|**Complexity** |1 |
|**Status**     |Draft |

## Abstract

As of now, the `btcDestinationAddress` field logged by the `release_request_received` event is a hash160 bytes format which is not user friendly. This RSKIP proposes updating the `btcDestinationAddress` field to the base58 string format.

## Motivation

These changes will improve the user experience of getting event information in a human readable/friendly format from the blockchain. 

## Specification

### Current signature:

```
release_request_received(address indexed sender, bytes btcDestinationAddress, uint256 amount)
```

The btcDestinationAddress field is currently in the hash160 bytes format.

### Proposed signature:

```
release_request_received(address indexed sender, string btcDestinationAddress, uint256 amount)
```

The btcDestinationAddress field will be in the base58 string format.

#### Data

- sender: the RSK address of the peg-out requester.
- btcDestinationAddress: the derived BTC address of said RSK address, where the BTC will be transferred to.
- amount: amount in weis the user sent to the Bridge (this doesn't reflect how many BTC will be received since transfer fees will be deducted from that amount).

If `RSKIP326` is activated, the event will log the `btcDestinationAddress` field in the base58 string format.

## Backwards Compatibility

This change is a hard-fork and therefore all full nodes, block explorers must be updated. SPV light-clients do not need to be updated. 

## References

[1] [RSKIP-185](https://github.com/rsksmart/RSKIPs/blob/master/IPs/RSKIP185.md) 

### Copyright

Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
