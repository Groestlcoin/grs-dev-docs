# Difficulty Adjustment

Groestlcoin's block difficulty adjustment is more involved than Bitcoin's. Groestlcoin uses the Dark Gravity Wave algorithm, and used a previous version of it before block height one hundred thousand.

For blocks before block height one hundred thousand, DGW version 1 is used. Blocks at height one hundred thousand and above use DGW version 3.

## Implementations

The Groestlcoin reference implementation's block difficulty adjustment can be found on [GitHub](https://github.com/Groestlcoin/groestlcoin/blob/2.16.3/src/groestlcoin.cpp#L128-L279).
