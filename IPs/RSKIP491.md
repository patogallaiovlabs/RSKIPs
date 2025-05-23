---
rskip: 491
title: Reduce target difficulty to lower average block time to 10s
description: This RSKIP proposes a 30% reduction in target difficulty to lower the average block time from 14 seconds to 10 seconds, improving transaction finality while maintaining network security.
status: Draft
purpose: Usa
author: PDG (@patogallaiovlabs)
layer: Core
complexity: 1
created: 2025-02-27
---

# Reduce target difficulty to lower average block time to 10s

|RSKIP          | 491        |
| :------------ |:-------------|
|**Title**      |Reduce target difficulty to lower average block time to 10s |
|**Created**    |27-FEB-2025 |
|**Author**     |Patricio Gallardo|
|**Purpose**    |Usa|
|**Layer**      |Core |
|**Complexity** |1 |
|**Status**     |Draft |

## Abstract

This RSKIP proposes reducing the target difficulty by 30% to achieve an average block time of 10 seconds instead of the current 14 seconds. By adjusting the difficulty calculation, Rootstock can improve transaction finality while maintaining network security and stability.

## Motivation  
Currently, Rootstock maintains a 14-second block time, balancing security and efficiency.  

Recent analysis of block template refresh intervals (as explored in [this research](https://blog.rootstock.io/noticia/leveraging-bitcoins-security-exploring-the-dynamics-of-merged-mining/)) showed that several mining pools have improved their block template refresh policies, reducing the time it takes to update new templates. These improvements have led to:  
- a **decrease in the sibling-to-main block ratio**,  
- and **faster effective block times**, previously averaging 30 seconds and now around [24 seconds](https://stats.rootstock.io/)(at the time of writing).  

With these optimizations in place, reducing the block time to **10 seconds** is now feasible, as the network can sustain faster block production without compromising stability.  

By leveraging these mining pool improvements, this proposal aims to:  
- **Reduce block time to 10 seconds** with minimal impact on network congestion while maintaining stability.  
- **Enhance transaction finality**, improving efficiency without compromising security.  
- **Encourage continued improvements in mining pool behavior**, reinforcing the benefits of optimized template refresh strategies.  


## Specification  
To achieve a 10-second block time, the target block time reference must be changed from **14s to 10s** in the difficulty adjustment calculation.  

In RSKj, this value is configured in the **`Constants`** class, which defines the target block time for mainnet and testnet. The relevant code can be found [here](https://github.com/rsksmart/rskj/blob/master/rskj-core/src/main/java/org/ethereum/config/Constants.java#L250) for mainnet and [here](https://github.com/rsksmart/rskj/blob/master/rskj-core/src/main/java/org/ethereum/config/Constants.java#L280) for testnet.

## Implementation
A lower difficulty target may lead to an increase in sibling blocks, which could impact network performance. While monitoring can help assess these effects, it cannot entirely prevent potential performance degradation.  

## Backwards Compatibility

This change is a hard-fork and therefore all full nodes must be updated. SPV light-clients do not need to be updated.
Additionally, protocols or applications that rely on block time assumptions should be notified prior to activation to allow for any necessary adjustments.  

### Copyright

Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
