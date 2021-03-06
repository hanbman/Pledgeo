## Avoiding common attacks

#### Use of audited contracts and libraries

All of the contracts imported (Pausable and Ownable libraries) come from safe sources (OpenZeppelin) where the contract have been audited for vulnerabilities by the community. 

#### Avoiding tx.origin

'msg.origin' was used throughout the contract rather than 'tx.origin' which may cause points of failure. 

#### Withdrawal pattern and reentrancy

The withdrawal method recommended in the Solidity documentation was implemented throughout the Pledgeo contract for transfering funds after an effect to a user.

In the withdrawalBalance function, the balance is set to 0 before the transfer is executed to prevent reentrancy as shown below.

```solidity
function withdrawalance() public {
    uint amount = pendingWithdrawals[msg.sender];
    pendingWithdrawals[msg.sender] = 0;
    msg.sender.transfer(amount);
}
```

#### Poison data

The functions are restricted (through 'Require' statements) from being called unless a certain state condition is met (state machines), the input parameters are valid, and the calling addresses are the ones permissioned.