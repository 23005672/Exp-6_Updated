# Experiment 6: Blockchain-Based Passwordless Authentication (Using Public-Private Key Cryptography)
# DATE : 23.04.2025
# Aim:
To implement a secure passwordless authentication system using public-private key cryptography on Ethereum. This prevents phishing and password leaks.

# Algorithm:
### step 1:
User opens the DApp interface.

### step 2:
User connects MetaMask to share their public Ethereum address.

### step 3:
User clicks “Register” to store their address on the blockchain.

### step 4:
Smart contract registers the user and emits a confirmation event.

### step 5:
User attempts to log in and receives a random challenge message.

### step 6:
User signs the message using their private key via MetaMask.

### step 7:
DApp sends the signed message and signature (v, r, s) to the smart contract.

### step 8:
Smart contract verifies the signature and confirms if the user is authenticated.

# Program:
```
NAME : RIYA P L
REG NO : 212223240141

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PasswordlessAuth {
    mapping(address => bool) public registeredUsers;

    event UserRegistered(address user);
    event UserAuthenticated(address user);

    // Register the user
    function registerUser() public {
        require(!registeredUsers[msg.sender], "Already registered");
        registeredUsers[msg.sender] = true;
        emit UserRegistered(msg.sender);
    }

    // Authenticate function that checks if the signed message is from the registered user
    function authenticate(string memory message, uint8 v, bytes32 r, bytes32 s) public view returns (bool) {
        require(registeredUsers[msg.sender], "User not registered");

        // Hash the message with the Ethereum prefix
        bytes32 messageHash = keccak256(abi.encodePacked("\x19Ethereum Signed Message:\n", uint2str(bytes(message).length), message));

        // Recover the signer from the signature (v, r, s)
        address signer = ecrecover(messageHash, v, r, s);

        // Check if the signer is the same as the msg.sender (who's trying to authenticate)
        return signer == msg.sender;
    }

    // Helper function to convert uint to string
    function uint2str(uint _i) internal pure returns (string memory _uintAsString) {
        if (_i == 0) {
            return "0";
        }
        uint j = _i;
        uint len;
        while (j != 0) {
            len++;
            j /= 10;
        }
        bytes memory bstr = new bytes(len);
        uint k = len - 1;
        while (_i != 0) {
            bstr[k--] = bytes1(uint8(48 + _i % 10)); // Use bytes1 instead of byte
            _i /= 10;
        }
        return string(bstr);
    }
}

```

# Output:
![6 1](https://github.com/user-attachments/assets/95ec2fab-23ff-4bfd-bf2a-d67d7b7a26ad)

![6 2](https://github.com/user-attachments/assets/171c86f3-0661-4066-8a22-64e898b1e125)

![6 3](https://github.com/user-attachments/assets/d1829017-9053-4218-b7d3-1ed28e040be7)

![6 4](https://github.com/user-attachments/assets/f105ec8d-4cd4-4dd0-a626-06d9eca99bfc)

# High-Level Overview:
Eliminates password hacks & phishing attacks.


Uses Ethereum's built-in cryptographic functions.


Inspired by Web3 login solutions like MetaMask authentication.

# RESULT: 
Thus the Blockchain-Based Passwordless Authentication (Using Public-Private Key Cryptography) is implemented successfully.
