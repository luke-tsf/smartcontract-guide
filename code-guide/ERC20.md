# ERC20 Token

## Initialize Smart Contract

Using Truffle to initialize sample smart contract.

`mkdir metacoin | cd metacoin`

`truffle unbox metacoin`

Initialize node package module

`npm init`

Install zepplin-solidity contract

`npm install zeppelin-solidity --save`
## Ownable contract
Location: `zeppelin-solidity/contracts/ownership/Ownable.sol`

This is a very famous smart contract to restrict access. Whenever a contract inherited this contract, it can set the owner variable and restrict access to some function via onlyOwner modifier.

## Pausable contract
Location: `zeppelin-solidity/contracts/lifecycle/Pausable.sol`

Pausable.sol is a contract provided by zepplin-solidity package. Pausable contract help to pause important function a token (Ex: transfer,...) whenever something is happen.

## Simple Detail Token with Pausable
```
pragma solidity ^0.4.8;

import "zeppelin-solidity/contracts/token/ERC20/DetailedERC20.sol";
import "zeppelin-solidity/contracts/lifecycle/Pausable.sol";

contract SimpleToken{
    constructor()
        //name, symbol, division 
        DetailedERC20 ("NAME","SYMBOL",0)
    {
        owner = msg.sender;
        emit OwnershipTransferred(address(0x0), owner);
        
        totalSupply_ = 0;        
        balances[owner] = totalSupply_;
        emit Transfer(address(0x0), owner, 0);
    }

    function transfer(address _to, uint256 _value) 
        whenNotPaused
        public 
        returns (bool success) 
    {
        return super.transfer(_to, _value);
    }
}
```

## Mintable Token

Mintable token can be reached in: `zeppelin-solidity/contracts/token/ERC20/MintableToken.sol`. A contract inherit this contract will have ability to be minted.

## Mintable Token

Mintable token can be reached in: `zeppelin-solidity/contracts/token/ERC20/BurnableToken.sol`. A contract inherit this contract will have ability to be burned (transfer into `address(0x0)`).

### Note: A Token can inherit many contract
