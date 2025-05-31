- 👋 Hi, I’m @Matin72328
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
Matin72328/Matin72328 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract TrumpSup {
    string public name = "TrumpSup";
    string public symbol = "TRUMPSUP";
    uint8 public decimals = 18;
    uint256 public totalSupply = 1000000000 * 10 ** uint256(decimals);
    address public owner = 0x33736051D1A675683e06add8Ce5eE02f99418cCd;

    mapping(address => uint256) public balanceOf;
    mapping(address => mapping(address => uint256)) public allowance;

    constructor() {
        balanceOf[owner] = totalSupply;
    }

    function transfer(address to, uint256 value) public returns (bool) {
        require(balanceOf[msg.sender] >= value, "Insufficient Balance");
        balanceOf[msg.sender] -= value;
        balanceOf[to] += value;
        return true;
    }

    function approve(address spender, uint256 value) public returns (bool) {
        allowance[msg.sender][spender] = value;
        return true;
    }

    function transferFrom(address from, address to, uint256 value) public returns (bool) {
        require(balanceOf[from] >= value, "Insufficient Balance");
        require(allowance[from][msg.sender] >= value, "Allowance Exceeded");
        balanceOf[from] -= value;
        balanceOf[to] += value;
        allowance[from][msg.sender] -= value;
        return true;
    }
}
