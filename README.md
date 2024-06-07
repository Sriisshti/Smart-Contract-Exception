# DrivingLicense Smart Contract

## Overview

This project contains a Solidity smart contract that simulates a simple driving license eligibility system. The contract demonstrates the use of Solidity's require(), assert(), and revert() statements to enforce rules and validate conditions.

## Smart Contract Details

The smart contract DrivingLicense allows users to set their age and vehicle ownership status, and check if they are eligible for a driving license based on these details.

### Key Features

- Set User Age: Users can set their age using the setAge() function.
- Set Vehicle Ownership Status: Users can set their vehicle ownership status using the setVehicleOwnership() function.
- Check Eligibility: Users can check if they are eligible for a driving license using the checkEligibility() function.

### Usage of require(), assert(), and revert()

- *require()* is used to:
  - Ensure the provided age is a reasonable value (greater than 0 and less than 150).
  - Ensure the age is set before checking eligibility.

- *revert()* is used to:
  - Indicate the user is not eligible for a driving license if their age is less than 18.

- *assert()* is used to:
  - Ensure the user's vehicle ownership status is set to true when they are checking their eligibility for a driving license.

## Smart Contract Code

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


## How to Use

1. Deploy the Contract: Deploy the DrivingLicense contract on an Ethereum test network (such as Ropsten or Rinkeby) using Remix or any other Ethereum development framework.
2. Set Age: Call the setAge() function with a valid age value.
3. Set Vehicle Ownership: Call the setVehicleOwnership() function with the boolean value true.
4. Check Eligibility: Call the checkEligibility() function to check if you are eligible for a driving license.

## License

This project is licensed under the MIT License.
