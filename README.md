# king-fallback
created a fallback to stop so that whenever the instance resets, nothing happens

Code to break:

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.6.0;

contract King {

  address payable king;
  uint public prize;
  address payable public owner;

  constructor() public payable {
    owner = msg.sender;  
    king = msg.sender;
    prize = msg.value;
  }

  receive() external payable {
    require(msg.value >= prize || msg.sender == owner);
    king.transfer(msg.value);
    king = msg.sender;
    prize = msg.value;
  }

  function _king() public view returns (address payable) {
    return king;
  }
}
```
Created another contract on remix ide and to send 1eth to the contract since that was the current kings balance and we need to become king first
then used  
```
king.transfer(msg.value);
    king = msg.sender;
    prize = msg.value;
    ```
    
   to my advantage to create a fallback for msg.value and set the string to null so that it does not send anything when it resets and we get to keep our spot
