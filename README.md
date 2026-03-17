# Zoro-contract
Zoro Protocol Issues fixing 

## Known Issues

### Timestamp Overflow Risk
The protocol uses `block.timestamp` instead of `block.number` for time-based calculations. Several functions cast timestamps to `uint32`, which will overflow when `block.timestamp` exceeds 2^32 - 1 (4,294,967,295) around the year 2106.

**Affected Functions:**
- `Comptroller._initializeMarket()`: Will prevent new markets from being initialized
- `Comptroller.updateCompSupplyIndex()`: Will halt COMP supply rewards distribution
- `Comptroller.updateCompBorrowIndex()`: Will halt COMP borrow rewards distribution

**Mitigation:** Upgrade `CompMarketState.block` from `uint32` to `uint64` or `uint256` before 2106.
