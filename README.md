# 7-sem

- Bt
- 3
   https://www.buybitcoinbank.com/cryptocurrency/add-polygon-mumbai-to-metamask
  
  - Network name: Mumbai 
  - Network URL: https://rpc-mumbai.maticvigil.com 
  - Chain ID: 80001 
  - Currency symbol: MATIC 
  - Block explorer URL: https://mumbai.polygonscan.com

   - https://faucet.quicknode.com/polygon/mumbai
     
   - Bank.sol
     
   - // SPDX-License-Identifier: UNLICENSED
pragma solidity >=0.8.0;



contract bank_account {
    mapping(address => uint256) public user_balance;
    mapping(address => bool) public is_user;
    
    function create_account() public {
        require(is_user[msg.sender] == false, "Account already exist");
        is_user[msg.sender] = true;
    }

    function deposit() public payable {
        require(is_user[msg.sender], "User Account Not Found");
        user_balance[msg.sender] += msg.value;
    }

    function withdraw(uint256 amount) public {
        require(is_user[msg.sender], "User Account Not Found");
        require(user_balance[msg.sender] >= amount, "You don't have enough balance to withdraw");
        require(payable(msg.sender).send(amount));
        user_balance[msg.sender] -= amount;
    }

    function show_balance(address user) public view returns (uint256) {
        require(is_user[user], "User Account Not Found");
        return (user_balance[user]);
    }
}

