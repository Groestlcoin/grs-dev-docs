# Subsidy

Groestlcoin's block rewards (subsidy) follow a schedule and depend on block height. Like Bitcoin, block height is the only determinant of block subsidy. Unlike Bitcoin, Groestlcoin's block subsidy is not a single geometric progression.

## Units

The following units are relevant to Groestlcoin's block subsidy:

- **gro**: Groestlcoin's equivalent of a satoshi. A gro is one hundred-millionth of a groestlcoin.
- **groestlcoin**: A unit corresponding to a bitcoin. A groestlcoin is one hundred million gro.

Like Bitcoin, Groestlcoin implements fractional amounts using integer arithmetic on units of gro.

*Localization note*: In this document, amounts use a comma as the thousands separator and a period as the decimal separator. For example, one thousand and two tenths is expressed as `1,000.2`.

## Schedule

### Genesis Block and Premine

The first two blocks in the Groestlcoin blockchain have subsidies that do not adhere to a schedule. The genesis block (height 0) has a subsidy of 1 groestlcoin, and the next block (height 1) has a subsidy of 240,640 groestlcoins.

### Block Heights 2 - 119,999

Block subsidies are 512 groestlcoins beginning at block height 2. For every 10,080 blocks (roughly one week) that precede a block, excluding the genesis block (height 0), block subsidies decrease by 6%. The minimum block subsidy is 5 groestlcoins.

### Block Heights 120,000 - 149,999

Block subsidies are 250 groestlcoins beginning at block height 120,000. For every 1,440 blocks (roughly one day) that precede a block in this interval, block subsidies decrease by 10%.

### Block Heights 150,000+

Block subsidies are 25 groestlcoins beginning at block height 150,000. For every 10,080 blocks (roughly one week) that precede a block in this interval, block subsidies decrease by 1%. The minimum block subsidy is 5 groestlcoins.

## Implementations

The Groestlcoin reference implementation's subsidy schedule can be found on [GitHub](https://github.com/Groestlcoin/groestlcoin/blob/2.16.3/src/groestlcoin.cpp#L54-L126).
