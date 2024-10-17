intento 2 tarea de vottun, ojala este bien
 contratos inteligentes

- VulnerableContract.sol: Un contrato con una vulnerabilidad en el uso de modificadores internal/external/public.
- ExploitContract.sol: Un contrato que explota la vulnerabilidad del contrato anterior.

*Repositorio:* (link unavailable)

*VulnerableContract.sol:*
solidity
pragma solidity ^0.8.0;

contract VulnerableContract {
    address public owner;
    uint public balance;

    constructor() public {
        owner = msg.sender;
        balance = 1000 ether;
    }

    // Vulnerable function, should be internal or private
    function transferBalance(address recipient) external {
        balance -= 100 ether;
        payable(recipient).transfer(100 ether);
    }

    // Vulnerable function, should be internal or private
    function updateOwner(address newOwner) external {
        owner = newOwner;
    }
}
*ExploitContract.sol:*
solidity
pragma solidity ^0.8.0;

import "./VulnerableContract.sol";

contract ExploitContract {
    address public attacker;
    VulnerableContract public vulnerableContract;

    constructor(address _vulnerableContract) public {
        attacker = msg.sender;
        vulnerableContract = VulnerableContract(_vulnerableContract);
    }
