pragma solidity ^0.8.26;

contract MyContract {
    mapping(address => uint256) public balances;
    
    event Deposited(address indexed sender, uint256 amount);
    event Withdrawn(address indexed sender, uint256 amount);

function deposit() public payable { 
        require(msg.value > 0);  
        
        if (balances[msg.sender] == 0) {
            balances[msg.sender] = msg.value;   
           emit Deposited(msg.sender,msg.value);// Changed here
        } else {
            balances[msg.sender] += msg.value;    
       }
    }

function getBalance() public view returns(uint256){
   return balances[msg.sender];
}
 function withdraw(uint256 amount) public { 
     require(amount > 0);
      require(balances[msg.sender] >= amount);

balances[msg.sender]=balances[msg.sender]-amount;
 emit Withdrawn(msg.sender, amount); }

}
