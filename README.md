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

        // Using require to ensure the vehicle ownership status is set
    

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
