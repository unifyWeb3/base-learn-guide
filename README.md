# base-learn-guide

There are three major ways I know we can gain exposure to base, they are: 
- Guild 
- Social
- Onchain activities

In order to reduce the bulkiness of this article, I would split this series into three parts. Then, we would begin by covering each and every one of the tasks on the base guild page. (This might not amount to anything, and this might amount to something, but you never know till you really try.)

GUILD
To access the guild, go to https://guild.xyz/base/home then connect your discord, X and Farcaster to continue. 
The guild page is split into 6 various categories, namely: 
Home
Stay Connected 
Onchain 
Builders and Founders 
Creators and Voices 
Base Programs

HOME 
This part has 6 sub parts in em and they are very simple tasks: 
Become Based (follow base and visit the base website)
Based (claim your base name) 
Onchain ( Hold a min of 0.001 ETH on Base and have at least one txn as well) 
Builders and Founders ( Have a github acc registered before July 1, 2025, have 1 commit on github, follow the link on the page too.)
Creators and Voices (Follow Base on X)
Coinbase onchain verified (Connect your active base wallet to your coinbase acc..)

STAY CONNECTED
This is quite simple, just follow base on reddit via https://www.reddit.com/r/BASE/

ONCHAIN 
There are five roles here. It requires 1 to 1000 transactions. The moment you score a thousand txns on Base, you get all 5 roles. So far, I have gotten a total sum of 6k txns, all organic... we’re going to add the number of people who have gotten each badge on the guild.

To check your stats as well, go to https://basescan.org, input your address then go to analytics.. 

be based!
BASE DEVELOPER
This part involves following buildonbase and it involves the base team or Jesse Polak following you. 

CREATOR'S AND VOICES 
This part is bit tricky and at the same time, it is not. 
This part focuses more on influencers with a lot of audience on X and Farcaster (between 10k- 100k followers on both apps) and it also focuses on users with a distinct Base social score. 
The Base social score was split into three categories: 
Base social score <20. 
Base social score between 21-60. 
Base social score above 61.

The only way to increase our social score is by interacting with and being followed by top key members on the base ecosystem..
Examples of such are: Jesse Polak, Connor Holliman (just anyone with a base badge, I believe) 

BASE PROGRAMS 
This part is a bit bulky so kindly stay close to me and pay attention
We have about 13 different roles to be collected in this segment and to get those roles, we have to learn how to deploy contracts onchain..

Before we get started here, we would need gas on base sepolia. To get gas on Base sepolia, we would go to https://testnet.brid.gg/base-sepolia?amount=&originChainId=11155111&token=ETH then we would connect our wallet and bridge from sepolia to base sepolia


The 13 contracts goes thus: 
basic contract NFT 
array contract NFT 
control structure NFT
strorage pin NFT 
mapping pin NFT
inheritance NFT
struct pin NFT
error triage pin NFT 
new keyword pin NFT
import pin NFT
scd erc721 pin NFT
minimal token pin NFT 
erc20 token pin NFT
We have covered the basic contract NFT, control structure NFT, array contract NFT, and storage pin NFT so far, so we would continue by covering mapping pin NFT to the ERC20 token pin NFT...
Today, we would continue our deployments by starting with the mapping pin NFT.
Mapping Pin NFT
go to https://remix.ethereum.org/#lang=en&optimize&runs=200&evmVersion&version=soljson-v0.8.30+commit.73712a01.js then connect your github 
after github connection, we would continue by creating the "mapping.sol" file under the contracts folder 
afterwards, we would paste the code below then compile it. 
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;

/**
 * @title FavoriteRecords
 * @dev Contract to manage a list of approved music records and allow users to add them to their favorites
 */
contract FavoriteRecords {
    // Mapping to store whether a record is approved
    mapping(string => bool) private approvedRecords;
    // Array to store the index of approved records
    string[] private approvedRecordsIndex;

    // Mapping to store user's favorite records
    mapping(address => mapping(string => bool)) public userFavorites;
    // Mapping to store the index of user's favorite records
    mapping(address => string[]) private userFavoritesIndex;

    // Custom error to handle unapproved records
    error NotApproved(string albumName);

    /**
     * @dev Constructor that initializes the approved records list
     */
    constructor() {
        // Predefined list of approved records
        approvedRecordsIndex = [
            "Thriller", 
            "Back in Black", 
            "The Bodyguard", 
            "The Dark Side of the Moon", 
            "Their Greatest Hits (1971-1975)", 
            "Hotel California", 
            "Come On Over", 
            "Rumours", 
            "Saturday Night Fever"
        ];
        // Initialize the approved records mapping
        for (uint i = 0; i < approvedRecordsIndex.length; i++) {
            approvedRecords[approvedRecordsIndex[i]] = true;
        }
    }

    /**
     * @dev Returns the list of approved records
     * @return An array of approved record names
     */
    function getApprovedRecords() public view returns (string[] memory) {
        return approvedRecordsIndex;
    }

    /**
     * @dev Adds an approved record to the user's favorites
     * @param _albumName The name of the album to be added
     */
    function addRecord(string memory _albumName) public {
        // Check if the record is approved
        if (!approvedRecords[_albumName]) {
            revert NotApproved({albumName: _albumName});
        }
        // Check if the record is not already in the user's favorites
        if (!userFavorites[msg.sender][_albumName]) {
            // Add the record to the user's favorites
            userFavorites[msg.sender][_albumName] = true;
            // Add the record to the user's favorites index
            userFavoritesIndex[msg.sender].push(_albumName);
        }
    }

    /**
     * @dev Returns the list of a user's favorite records
     * @param _address The address of the user
     * @return An array of user's favorite record names
     */
    function getUserFavorites(address _address) public view returns (string[] memory) {
        return userFavoritesIndex[_address];
    }

    /**
     * @dev Resets the caller's list of favorite records
     */
    function resetUserFavorites() public {
        // Iterate through the user's favorite records
        for (uint i = 0; i < userFavoritesIndex[msg.sender].length; i++) {
            // Delete each record from the user's favorites mapping
            delete userFavorites[msg.sender][userFavoritesIndex[msg.sender][i]];
        }
        // Delete the user's favorites index
        delete userFavoritesIndex[msg.sender];
    }
}
after compiling, we would press the deploy button to deploy the contract. 
lastly, we would copy the contract address and we would paste it in https://docs.base.org/learn/mappings/mappings-exercise to get the NFT..  
mapping.sol contract NFT 

Inheritance NFT
go to Remix 
under the contract folder, we would create a new file called "inheritance.sol" then we would copy and paste the code below into the file. 
// SPDX-License-Identifier: MIT

pragma solidity 0.8.17;

/**
 * @title Employee
 * @dev Abstract contract defining common properties and behavior for employees.
 */
abstract contract Employee {
    uint public idNumber; // Unique identifier for the employee
    uint public managerId; // Identifier of the manager overseeing the employee

    /**
     * @dev Constructor to initialize idNumber and managerId.
     * @param _idNumber The unique identifier for the employee.
     * @param _managerId The identifier of the manager overseeing the employee.
     */
    constructor(uint _idNumber, uint _managerId) {
        idNumber = _idNumber;
        managerId = _managerId;
    }

    /**
     * @dev Abstract function to be implemented by derived contracts to get the annual cost of the employee.
     * @return The annual cost of the employee.
     */
    function getAnnualCost() public virtual returns (uint);
}

/**
 * @title Salaried
 * @dev Contract representing employees who are paid an annual salary.
 */
contract Salaried is Employee {
    uint public annualSalary; // The annual salary of the employee

    /**
     * @dev Constructor to initialize the Salaried contract.
     * @param _idNumber The unique identifier for the employee.
     * @param _managerId The identifier of the manager overseeing the employee.
     * @param _annualSalary The annual salary of the employee.
     */
    constructor(uint _idNumber, uint _managerId, uint _annualSalary) Employee(_idNumber, _managerId) {
        annualSalary = _annualSalary;
    }

    /**
     * @dev Overrides the getAnnualCost function to return the annual salary of the employee.
     * @return The annual salary of the employee.
     */
    function getAnnualCost() public override view returns (uint) {
        return annualSalary;
    }
}

/**
 * @title Hourly
 * @dev Contract representing employees who are paid an hourly rate.
 */
contract Hourly is Employee {
    uint public hourlyRate; // The hourly rate of the employee

    /**
     * @dev Constructor to initialize the Hourly contract.
     * @param _idNumber The unique identifier for the employee.
     * @param _managerId The identifier of the manager overseeing the employee.
     * @param _hourlyRate The hourly rate of the employee.
     */
    constructor(uint _idNumber, uint _managerId, uint _hourlyRate) Employee(_idNumber, _managerId) {
        hourlyRate = _hourlyRate;
    }

    /**
     * @dev Overrides the getAnnualCost function to calculate the annual cost based on the hourly rate.
     * Assuming a full-time workload of 2080 hours per year.
     * @return The annual cost of the employee.
     */
    function getAnnualCost() public override view returns (uint) {
        return hourlyRate * 2080;
    }
}

/**
 * @title Manager
 * @dev Contract managing a list of employee IDs.
 */
contract Manager {
    uint[] public employeeIds; // List of employee IDs

    /**
     * @dev Function to add a new employee ID to the list.
     * @param _reportId The ID of the employee to be added.
     */
    function addReport(uint _reportId) public {
        employeeIds.push(_reportId);
    }

    /**
     * @dev Function to reset the list of employee IDs.
     */
    function resetReports() public {
        delete employeeIds;
    }
}

/**
 * @title Salesperson
 * @dev Contract representing salespeople who are paid hourly.
 */
contract Salesperson is Hourly {
    /**
     * @dev Constructor to initialize the Salesperson contract.
     * @param _idNumber The unique identifier for the employee.
     * @param _managerId The identifier of the manager overseeing the employee.
     * @param _hourlyRate The hourly rate of the employee.
     */
    constructor(uint _idNumber, uint _managerId, uint _hourlyRate) 
        Hourly(_idNumber, _managerId, _hourlyRate) {}
}

/**
 * @title EngineeringManager
 * @dev Contract representing engineering managers who are paid an annual salary and have managerial responsibilities.
 */
contract EngineeringManager is Salaried, Manager {
    /**
     * @dev Constructor to initialize the EngineeringManager contract.
     * @param _idNumber The unique identifier for the employee.
     * @param _managerId The identifier of the manager overseeing the employee.
     * @param _annualSalary The annual salary of the employee.
     */
    constructor(uint _idNumber, uint _managerId, uint _annualSalary) 
        Salaried(_idNumber, _managerId, _annualSalary) {}
}

/**
 * @title InheritanceSubmission
 * @dev Contract for deploying instances of Salesperson and EngineeringManager.
 */
contract InheritanceSubmission {
    address public salesPerson; // Address of the deployed Salesperson instance
    address public engineeringManager; // Address of the deployed EngineeringManager instance

    /**
     * @dev Constructor to initialize the InheritanceSubmission contract.
     * @param _salesPerson Address of the deployed Salesperson instance.
     * @param _engineeringManager Address of the deployed EngineeringManager instance.
     */
    constructor(address _salesPerson, address _engineeringManager) {
        salesPerson = _salesPerson;
        engineeringManager = _engineeringManager;
    }
}
After pasting the code, we would compile it then go to the deployment tab on remix. 
This place is a bit tricky, as we are running 4 deployments, so please pay attention.
Input the below parameters for "sales person" then press the transact button to deploy the contract: This is the first contract, make sure you save the contract address as we would need it in the fourth contract deployment. 
Hourly rate is 20 dollars an hour
Id number is 55555
Manager Id number is 12345
2.     Deploy the manager contract by selecting the manager contract and pressing the transact button ( 0 parameters needed) and this is our second contract. 
3.      Input the following parameters for  "engineering manager"  then press the transact button button to deploy the contract: This is the third contract, make sure you save the contract address as we would need it in the fourth contract deployment.
Annual salary is 200000
Id number is 54321
Manager Id is 11111
4.     Select the inheritance submission contract and input the CA for sales person and Engineering manager then press transact to deploy the fourth contract. 
Lastly, we would go to https://docs.base.org/learn/inheritance/inheritance-exercise to submit the contract address for the inheritance submission so as to collect the NFT. 


Struct Pin NFT
go to Remix 
Under the contract folder, we would create a "struct.sol" file then we would input the code below into the file. 
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;

/**
 * @title GarageManager
 * @dev Contract to manage a garage of cars for each user
 */
contract GarageManager {
    // Mapping to store the garage of cars for each user
    mapping(address => Car[]) private garages;

    // Struct to represent a car
    struct Car {
        string make; // Make of the car
        string model; // Model of the car
        string color; // Color of the car
        uint numberOfDoors; // Number of doors of the car
    }

    // Custom error for handling invalid car index
    error BadCarIndex(uint256 index);

    /**
     * @dev Adds a new car to the caller's garage
     * @param _make The make of the car
     * @param _model The model of the car
     * @param _color The color of the car
     * @param _numberOfDoors The number of doors of the car
     */
    function addCar(string memory _make, string memory _model, string memory _color, uint _numberOfDoors) external {
        // Push a new car struct with the provided details to the caller's garage
        garages[msg.sender].push(Car(_make, _model, _color, _numberOfDoors));
    }

    /**
     * @dev Retrieves the caller's array of cars
     * @return An array of `Car` structs
     */
    function getMyCars() external view returns (Car[] memory) {
        // Return the array of cars stored in the caller's garage
        return garages[msg.sender];
    }

    /**
     * @dev Retrieves a specific user's array of cars
     * @param _user The address of the user
     * @return An array of `Car` structs
     */
    function getUserCars(address _user) external view returns (Car[] memory) {
        // Return the array of cars stored in the garage of the specified user
        return garages[_user];
    }

    /**
     * @dev Updates a specific car in the caller's garage
     * @param _index The index of the car in the garage array
     * @param _make The new make of the car
     * @param _model The new model of the car
     * @param _color The new color of the car
     * @param _numberOfDoors The new number of doors of the car
     */
    function updateCar(uint256 _index, string memory _make, string memory _model, string memory _color, uint _numberOfDoors) external {
        // Check if the provided index is valid
        if (_index >= garages[msg.sender].length) {
            revert BadCarIndex({index: _index}); // Revert with custom error if the index is invalid
        }
        // Update the specified car with the new details
        garages[msg.sender][_index] = Car(_make, _model, _color, _numberOfDoors);
    }

    /**
     * @dev Deletes all cars in the caller's garage
     */
    function resetMyGarage() external {
        // Delete all cars from the caller's garage
        delete garages[msg.sender];
    }
}
afterwards, we would compile the codes then we would deploy the contract. 
Lastly, we would go to https://docs.base.org/learn/structs/structs-exercise to claim the NFT for structs. 

Error Triage Pin NFT 
go to remix 
create a "error.sol" file under the contract folder then paste the code below.. 
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.17;

contract ErrorTriageExercise {
    /**
     * @dev Finds the difference between each uint with its neighbor (a to b, b to c, etc.)
     * and returns a uint array with the absolute integer difference of each pairing.
     * 
     * @param _a The first unsigned integer.
     * @param _b The second unsigned integer.
     * @param _c The third unsigned integer.
     * @param _d The fourth unsigned integer.
     * 
     * @return results An array containing the absolute differences between each pair of integers.
     */
    function diffWithNeighbor(
        uint _a,
        uint _b,
        uint _c,
        uint _d
    ) public pure returns (uint[] memory) {
        // Initialize an array to store the differences
        uint[] memory results = new uint[](3);

        // Calculate the absolute difference between each pair of integers and store it in the results array
        results[0] = _a > _b ? _a - _b : _b - _a;
        results[1] = _b > _c ? _b - _c : _c - _b;
        results[2] = _c > _d ? _c - _d : _d - _c;

        // Return the array of differences
        return results;
    }

    /**
     * @dev Changes the base by the value of the modifier. Base is always >= 1000. Modifiers can be
     * between positive and negative 100.
     * 
     * @param _base The base value to be modified.
     * @param _modifier The value by which the base should be modified.
     * 
     * @return returnValue The modified value of the base.
     */
    function applyModifier(
        uint _base,
        int _modifier
    ) public pure returns (uint returnValue) {
        // Apply the modifier to the base value
        if(_modifier > 0) {
            return _base + uint(_modifier);
        }
        return _base - uint(-_modifier);
    }


    uint[] arr;

    function popWithReturn() public returns (uint returnNum) {
        if(arr.length > 0) {
            uint result = arr[arr.length - 1];
            arr.pop();
            return result;
        }
    }

    // The utility functions below are working as expected
    function addToArr(uint _num) public {
        arr.push(_num);
    }

    function getArr() public view returns (uint[] memory) {
        return arr;
    }

    function resetArr() public {
        delete arr;
    }
}
afterwards, compile the "error.sol" file then proceed to deploy the contract 
Lastly, go to https://docs.base.org/learn/error-triage/error-triage-exercise then paste the contract address to claim the NFT..


New Keyword NFT 
go to remix 
Here, we are creating two new files under the contract folder..
The first file is   "AddressBook.sol" file and here is the code below:  (Please make sure you use the above file name so as to escape errors) (If compiling returns an OPENZEPPELIN error, change the compiler version and redeploy.)
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.8;

import "@openzeppelin/contracts/access/Ownable.sol";

contract AddressBook is Ownable(msg.sender) {
    // Define a private salt value for internal use
    string private salt = "value"; 

    // Define a struct to represent a contact
    struct Contact {
        uint id; // Unique identifier for the contact
        string firstName; // First name of the contact
        string lastName; // Last name of the contact
        uint[] phoneNumbers; // Array to store multiple phone numbers for the contact
    }

    // Array to store all contacts
    Contact[] private contacts;

    // Mapping to store the index of each contact in the contacts array using its ID
    mapping(uint => uint) private idToIndex;

    // Variable to keep track of the ID for the next contact
    uint private nextId = 1;

    // Custom error for when a contact is not found
    error ContactNotFound(uint id);

    // Function to add a new contact
    function addContact(string calldata firstName, string calldata lastName, uint[] calldata phoneNumbers) external onlyOwner {
        // Create a new contact with the provided details and add it to the contacts array
        contacts.push(Contact(nextId, firstName, lastName, phoneNumbers));
        // Map the ID of the new contact to its index in the array
        idToIndex[nextId] = contacts.length - 1;
        // Increment the nextId for the next contact
        nextId++;
    }

    // Function to delete a contact by its ID
    function deleteContact(uint id) external onlyOwner {
        // Get the index of the contact to be deleted
        uint index = idToIndex[id];
        // Check if the index is valid and if the contact with the provided ID exists
        if (index >= contacts.length || contacts[index].id != id) revert ContactNotFound(id);

        // Replace the contact to be deleted with the last contact in the array
        contacts[index] = contacts[contacts.length - 1];
        // Update the index mapping for the moved contact
        idToIndex[contacts[index].id] = index;
        // Remove the last contact from the array
        contacts.pop();
        // Delete the mapping entry for the deleted contact ID
        delete idToIndex[id];
    }

    // Function to retrieve a contact by its ID
    function getContact(uint id) external view returns (Contact memory) {
        // Get the index of the contact
        uint index = idToIndex[id];
        // Check if the index is valid and if the contact with the provided ID exists
        if (index >= contacts.length || contacts[index].id != id) revert ContactNotFound(id);
        // Return the contact details
        return contacts[index];
    }

    // Function to retrieve all contacts
    function getAllContacts() external view returns (Contact[] memory) {
        // Return the array of all contacts
        return contacts;
    }
}
the second file is "othercontract.sol" and here is the code for it: 
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.8;

// Import the AddressBook contract to interact with it
import "./AddressBook.sol";

// Contract for creating new instances of AddressBook
contract AddressBookFactory {
    // Define a private salt value for internal use
    string private salt = "value";

    // Function to deploy a new instance of AddressBook
    function deploy() external returns (AddressBook) {
        // Create a new instance of AddressBook
        AddressBook newAddressBook = new AddressBook();

        // Transfer ownership of the new AddressBook contract to the caller of this function
        newAddressBook.transferOwnership(msg.sender);

        // Return the newly created AddressBook contract
        return newAddressBook;
    }
}
after creating both files, we would proceed by compiling them one after the other.. 
after compiling, we would proceed by deploying the contract.
lastly, we would paste our contract address in https://docs.base.org/learn/new-keyword/new-keyword-exercise then we would sign the txn. 



Import Pin NFT 
go to remix 
we are creating two new files under the contract folder here. 
Name file 1 "SillyStringUtils.sol" then input the below code and compile it. (Please make sure you use the above file name so as to escape errors)
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.17;

library SillyStringUtils {

    struct Haiku {
        string line1;
        string line2;
        string line3;
    }

    function shruggie(string memory _input) internal pure returns (string memory) {
        return string.concat(_input, unicode" 🤷");
    }
}
Name file 2 "imports.sol" then input the below code and compile it. 
f you run into a compiler error here, change the compiler version then re-compile. 
// SPDX-License-Identifier: MIT

// Importing the SillyStringUtils library
import "./SillyStringUtils.sol";

pragma solidity 0.8.17;

contract ImportsExercise {
    // Using the SillyStringUtils library for string manipulation
    using SillyStringUtils for string;

    // Declaring a public variable to store a Haiku
    SillyStringUtils.Haiku public haiku;

    // Function to save a Haiku
    function saveHaiku(string memory _line1, string memory _line2, string memory _line3) public {
        haiku.line1 = _line1;
        haiku.line2 = _line2;
        haiku.line3 = _line3;
    }

    // Function to retrieve the saved Haiku
    function getHaiku() public view returns (SillyStringUtils.Haiku memory) {
        return haiku;
    }

    // Function to append a shrugging emoji to the third line of the Haiku
    function shruggieHaiku() public view returns (SillyStringUtils.Haiku memory) {
        // Creating a copy of the Haiku
        SillyStringUtils.Haiku memory newHaiku = haiku;
        // Appending the shrugging emoji to the third line using the shruggie function from the SillyStringUtils library
        newHaiku.line3 = newHaiku.line3.shruggie();
        return newHaiku;
    }
}
After compiling, deploy the contract then go to https://docs.base.org/learn/imports/imports-exercise to paste the contract address and claim the NFT.. 



SCD ERC721 pin NFT
go to remix 
create a new file and name it "ERC721.sol" under the contract folder
after creating the file, we would input the code below into the file then we would proceed by compiling the contract before deploying the contract. 
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

// Importing OpenZeppelin ERC721 contract
import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC721/ERC721.sol";

// Interface for interacting with a submission contract
interface ISubmission {
    // Struct representing a haiku
    struct Haiku {
        address author; // Address of the haiku author
        string line1; // First line of the haiku
        string line2; // Second line of the haiku
        string line3; // Third line of the haiku
    }

    // Function to mint a new haiku
    function mintHaiku(
        string memory _line1,
        string memory _line2,
        string memory _line3
    ) external;

    // Function to get the total number of haikus
    function counter() external view returns (uint256);

    // Function to share a haiku with another address
    function shareHaiku(uint256 _id, address _to) external;

    // Function to get haikus shared with the caller
    function getMySharedHaikus() external view returns (Haiku[] memory);
}

// Contract for managing Haiku NFTs
contract HaikuNFT is ERC721, ISubmission {
    Haiku[] public haikus; // Array to store haikus
    mapping(address => mapping(uint256 => bool)) public sharedHaikus; // Mapping to track shared haikus
    uint256 public haikuCounter; // Counter for total haikus minted

    // Constructor to initialize the ERC721 contract
    constructor() ERC721("HaikuNFT", "HAIKU") {
        haikuCounter = 1; // Initialize haiku counter
    }

    string salt = "value"; // A private string variable

    // Function to get the total number of haikus
    function counter() external view override returns (uint256) {
        return haikuCounter;
    }

    // Function to mint a new haiku
    function mintHaiku(
        string memory _line1,
        string memory _line2,
        string memory _line3
    ) external override {
        // Check if the haiku is unique
        string[3] memory haikusStrings = [_line1, _line2, _line3];
        for (uint256 li = 0; li < haikusStrings.length; li++) {
            string memory newLine = haikusStrings[li];
            for (uint256 i = 0; i < haikus.length; i++) {
                Haiku memory existingHaiku = haikus[i];
                string[3] memory existingHaikuStrings = [
                    existingHaiku.line1,
                    existingHaiku.line2,
                    existingHaiku.line3
                ];
                for (uint256 eHsi = 0; eHsi < 3; eHsi++) {
                    string memory existingHaikuString = existingHaikuStrings[
                        eHsi
                    ];
                    if (
                        keccak256(abi.encodePacked(existingHaikuString)) ==
                        keccak256(abi.encodePacked(newLine))
                    ) {
                        revert HaikuNotUnique();
                    }
                }
            }
        }

        // Mint the haiku NFT
        _safeMint(msg.sender, haikuCounter);
        haikus.push(Haiku(msg.sender, _line1, _line2, _line3));
        haikuCounter++;
    }

    // Function to share a haiku with another address
    function shareHaiku(uint256 _id, address _to) external override {
        require(_id > 0 && _id <= haikuCounter, "Invalid haiku ID");

        Haiku memory haikuToShare = haikus[_id - 1];
        require(haikuToShare.author == msg.sender, "NotYourHaiku");

        sharedHaikus[_to][_id] = true;
    }

    // Function to get haikus shared with the caller
    function getMySharedHaikus()
        external
        view
        override
        returns (Haiku[] memory)
    {
        uint256 sharedHaikuCount;
        for (uint256 i = 0; i < haikus.length; i++) {
            if (sharedHaikus[msg.sender][i + 1]) {
                sharedHaikuCount++;
            }
        }

        Haiku[] memory result = new Haiku[](sharedHaikuCount);
        uint256 currentIndex;
        for (uint256 i = 0; i < haikus.length; i++) {
            if (sharedHaikus[msg.sender][i + 1]) {
                result[currentIndex] = haikus[i];
                currentIndex++;
            }
        }

        if (sharedHaikuCount == 0) {
            revert NoHaikusShared();
        }

        return result;
    }

    // Custom errors
    error HaikuNotUnique(); // Error for attempting to mint a non-unique haiku
    error NotYourHaiku(); // Error for attempting to share a haiku not owned by the caller
    error NoHaikusShared(); // Error for no haikus shared with the caller
}
Lastly, we would copy our deployed contract then we would go to https://docs.base.org/learn/token-development/erc-721-token/erc-721-exercise then we would paste the contract address and claim the NFT. 


ERC721.sol Pin NFT
Minimal Token Pin NFT 
go to remix 
create a new file named "minimal.sol" under the contracts folder then input the code below into the file. 
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

// Contract for an unburnable token
contract UnburnableToken {
    string private salt = "value"; // A private string variable

    // Mapping to track token balances of addresses
    mapping(address => uint256) public balances;

    uint256 public totalSupply; // Total supply of tokens
    uint256 public totalClaimed; // Total number of tokens claimed
    mapping(address => bool) private claimed; // Mapping to track whether an address has claimed tokens

    // Custom errors
    error TokensClaimed(); // Error for attempting to claim tokens again
    error AllTokensClaimed(); // Error for attempting to claim tokens when all are already claimed
    error UnsafeTransfer(address _to); // Error for unsafe token transfer

    // Constructor to set the total supply of tokens
    constructor() {
        totalSupply = 100000000; // Set the total supply of tokens
    }

    // Public function to claim tokens
    function claim() public {
        // Check if all tokens have been claimed
        if (totalClaimed >= totalSupply) revert AllTokensClaimed();
        
        // Check if the caller has already claimed tokens
        if (claimed[msg.sender]) revert TokensClaimed();

        // Update balances and claimed status
        balances[msg.sender] += 1000;
        totalClaimed += 1000;
        claimed[msg.sender] = true;
    }

    // Public function for safe token transfer
    function safeTransfer(address _to, uint256 _amount) public {
        // Check for unsafe transfer conditions, including if the target address has a non-zero ether balance
        if (_to == address(0) || _to.balance == 0) revert UnsafeTransfer(_to);

        // Ensure the sender has enough balance to transfer
        require(balances[msg.sender] >= _amount, "Insufficient balance");

        // Perform the transfer
        balances[msg.sender] -= _amount;
        balances[_to] += _amount;
    }
}
after inputing the code, we would proceed by compiling the contract then deploying the contract..
lastly, we would go to https://docs.base.org/learn/token-development/minimal-tokens/minimal-tokens-exercise then we would submit the contract and claim the NFT. 



* ERC20 Token Pin NFT
go to remix
create a new file named "ERC20.sol" under the contracts folder then input the code below into the file.
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.17;

// Importing OpenZeppelin contracts for ERC20 and EnumerableSet functionalities
import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/utils/structs/EnumerableSet.sol";

// Contract for weighted voting using ERC20 token
contract WeightedVoting is ERC20 {
    string private salt = "value"; // A private string variable
    using EnumerableSet for EnumerableSet.AddressSet; // Importing EnumerableSet for address set functionality

    // Custom errors
    error TokensClaimed(); // Error for attempting to claim tokens again
    error AllTokensClaimed(); // Error for attempting to claim tokens when all are already claimed
    error NoTokensHeld(); // Error for attempting to perform an action without holding tokens
    error QuorumTooHigh(); // Error for setting a quorum higher than total supply
    error AlreadyVoted(); // Error for attempting to vote more than once
    error VotingClosed(); // Error for attempting to vote on a closed issue

    // Struct to represent an issue
    struct Issue {
        EnumerableSet.AddressSet voters; // Set of voters
        string issueDesc; // Description of the issue
        uint256 quorum; // Quorum required to close the issue
        uint256 totalVotes; // Total number of votes casted
        uint256 votesFor; // Total number of votes in favor
        uint256 votesAgainst; // Total number of votes against
        uint256 votesAbstain; // Total number of abstained votes
        bool passed; // Flag indicating if the issue passed
        bool closed; // Flag indicating if the issue is closed
    }

    // Struct to represent a serialized issue
    struct SerializedIssue {
        address[] voters; // Array of voters
        string issueDesc; // Description of the issue
        uint256 quorum; // Quorum required to close the issue
        uint256 totalVotes; // Total number of votes casted
        uint256 votesFor; // Total number of votes in favor
        uint256 votesAgainst; // Total number of votes against
        uint256 votesAbstain; // Total number of abstained votes
        bool passed; // Flag indicating if the issue passed
        bool closed; // Flag indicating if the issue is closed
    }

    // Enum to represent different vote options
    enum Vote {
        AGAINST,
        FOR,
        ABSTAIN
    }

    // Array to store all issues
    Issue[] internal issues;

    // Mapping to track if tokens are claimed by an address
    mapping(address => bool) public tokensClaimed;

    uint256 public maxSupply = 1000000; // Maximum supply of tokens
    uint256 public claimAmount = 100; // Amount of tokens to be claimed

    string saltt = "any"; // Another string variable

    // Constructor to initialize ERC20 token with a name and symbol
    constructor(string memory _name, string memory _symbol)
        ERC20(_name, _symbol)
    {
        issues.push(); // Pushing an empty issue to start from index 1
    }

    // Function to claim tokens
    function claim() public {
        // Check if all tokens have been claimed
        if (totalSupply() + claimAmount > maxSupply) {
            revert AllTokensClaimed();
        }
        // Check if the caller has already claimed tokens
        if (tokensClaimed[msg.sender]) {
            revert TokensClaimed();
        }
        // Mint tokens to the caller
        _mint(msg.sender, claimAmount);
        tokensClaimed[msg.sender] = true; // Mark tokens as claimed
    }

    // Function to create a new voting issue
    function createIssue(string calldata _issueDesc, uint256 _quorum)
        external
        returns (uint256)
    {
        // Check if the caller holds any tokens
        if (balanceOf(msg.sender) == 0) {
            revert NoTokensHeld();
        }
        // Check if the specified quorum is higher than total supply
        if (_quorum > totalSupply()) {
            revert QuorumTooHigh();
        }
        // Create a new issue and return its index
        Issue storage _issue = issues.push();
        _issue.issueDesc = _issueDesc;
        _issue.quorum = _quorum;
        return issues.length - 1;
    }

    // Function to get details of a voting issue
    function getIssue(uint256 _issueId)
        external
        view
        returns (SerializedIssue memory)
    {
        Issue storage _issue = issues[_issueId];
        return
            SerializedIssue({
                voters: _issue.voters.values(),
                issueDesc: _issue.issueDesc,
                quorum: _issue.quorum,
                totalVotes: _issue.totalVotes,
                votesFor: _issue.votesFor,
                votesAgainst: _issue.votesAgainst,
                votesAbstain: _issue.votesAbstain,
                passed: _issue.passed,
                closed: _issue.closed
            });
    }

    // Function to cast a vote on a voting issue
    function vote(uint256 _issueId, Vote _vote) public {
        Issue storage _issue = issues[_issueId];

        // Check if the issue is closed
        if (_issue.closed) {
            revert VotingClosed();
        }
        // Check if the caller has already voted
        if (_issue.voters.contains(msg.sender)) {
            revert AlreadyVoted();
        }

        uint256 nTokens = balanceOf(msg.sender);
        // Check if the caller holds any tokens
        if (nTokens == 0) {
            revert NoTokensHeld();
        }

        // Update vote counts based on the vote option
        if (_vote == Vote.AGAINST) {
            _issue.votesAgainst += nTokens;
        } else if (_vote == Vote.FOR) {
            _issue.votesFor += nTokens;
        } else {
            _issue.votesAbstain += nTokens;
        }

        // Add the caller to the list of voters and update total votes count
        _issue.voters.add(msg.sender);
        _issue.totalVotes += nTokens;

        // Close the issue if quorum is reached and determine if it passed
        if (_issue.totalVotes >= _issue.quorum) {
            _issue.closed = true;
            if (_issue.votesFor > _issue.votesAgainst) {
                _issue.passed = true;
            }
        }
    }
}
after inputing the code, we would proceed by compiling the contract then deploying the contract.. (deploying the contract here requires us to enter the name and symbol of the token we would like to deploy.) e.g- token name: flynn, token symbol: FLY
lastly, we would go to https://docs.base.org/learn/token-development/erc-20-token/erc-20-exercise to claim the NFT by submitting the deployed contract. 


ERC20.sol Pin NFT. 
After claiming all 13 NFTs, we would proceed to https://guild.xyz/base/base-programs then we would continue by connecting our EVM wallet and our coinbase wallet to guild. 
After connecting em, we would proceed by verifying each quest so as to get the:
Base Learn Newcomer 
Base Learn Acolyte
Base Learn Consul
Base Learn Perfect 
Base Learn Supreme roles. 
We should have all the roles since we have gotten all 13 NFTs by deploying the contracts. 

thats all for now. thank you. probably nothing
