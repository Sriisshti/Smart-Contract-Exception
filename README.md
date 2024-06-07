# DrivingLicense Smart Contract

This Solidity program is a simple contract that demonstrates the use of require(), assert(), and revert() statements in Solidity.The purpose of the contract is to demonstrate the error handling while creation and updation of  driving license and vehicle ownership using require(), assert() and revert().

## Description

This contract simulates a driving license eligibility system. Users can set their age and vehicle ownership status, and then check if they are eligible for a driving license based on these details. The contract uses Solidity's require(), assert(), and revert() statements to enforce rules and validate conditions.

## Getting Started

### Executing Program

To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at [Remix Ethereum IDE](https://remix.ethereum.org/).

Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., DrivingLicense.sol). Copy and paste the following code into the file:

solidity
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.0;

contract DrivingLicense {
    // Mapping to store the age of each user
    mapping(address => uint) public age;

    // Mapping to store whether a user owns a vehicle
    mapping(address => bool) public ownsVehicle;

    // Function to set the age of a user
    function setAge(uint _age) public {
        // Using require to ensure the age is a reasonable value
        require(_age > 0 && _age < 150, "Invalid age provided.");

        // Setting the age for the sender's address
        age[msg.sender] = _age;
    }

    // Function to set vehicle ownership status of a user
    function setVehicleOwnership(bool _ownsVehicle) public {
        // Setting the vehicle ownership status for the sender's address
        ownsVehicle[msg.sender] = _ownsVehicle;
    }

    // Function to check eligibility for a driving license
    function checkEligibility() public view returns (bool) {
        uint userAge = age[msg.sender];
        bool vehicleOwnership = ownsVehicle[msg.sender];

        // Using require to ensure the age is set
        require(userAge > 0, "Age is not set. Please set your age first.");

        // Check if the user is eligible for a driving license
        if (userAge < 18) {
            // Using revert to indicate the user is not eligible
            revert("You are not eligible for a driving license.");
        }

        // Using assert to ensure the user's age is indeed 18 or greater
        assert(vehicleOwnership == true);

        // Returning the eligibility status in boolean form
        return true;
    }
}


To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.0" (or another compatible version), and then click on the "Compile DrivingLicense.sol" button.

Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar. Select the "DrivingLicense" contract from the dropdown menu, and then click on the "Deploy" button.

Once the contract is deployed, you can interact with it by calling the setAge(), setVehicleOwnership(), and checkEligibility() functions. Set your age and vehicle ownership status first, and then check your eligibility for a driving license.

## Authors

Srishti
@Srishti

## License

This project is licensed under the MIT License - see the LICENSE.md file for details.
