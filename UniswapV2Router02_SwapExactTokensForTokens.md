## Introduction

**Protocol Name**: Uniswap  
**Category**: DeFi  
**Smart Contract**: [UniswapV2Router02](https://etherscan.io/address/0x7a250d5630b4cf539739df2c5dacf5a442f4c34a#code)  

## Function Analysis

**Function Name**: `swapExactTokensForTokens`  
**Block Explorer Link**: [UniswapV2Router02 on Etherscan](https://etherscan.io/address/0x7a250d5630b4cf539739df2c5dacf5a442f4c34a#code)  
**Function Code**:
```solidity
function swapExactTokensForTokens(
    uint amountIn,
    uint amountOutMin,
    address[] calldata path,
    address to,
    uint deadline
) external ensure(deadline) returns (uint[] memory amounts) {
    amounts = UniswapV2Library.getAmountsOut(factory, amountIn, path);
    require(amounts[amounts.length - 1] >= amountOutMin, 'UniswapV2Router: INSUFFICIENT_OUTPUT_AMOUNT');
    TransferHelper.safeTransferFrom(
        path[0], msg.sender, UniswapV2Library.pairFor(factory, path[0], path[1]), amounts[0]
    );
    _swap(amounts, path, to);
}
