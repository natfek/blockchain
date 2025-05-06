# Chapter 1

Solidity is a high-level programming language used to write smart contracts that run on the Ethereum blockchain, enabling decentralized applications and automated, trustless transactions.

<a name="Value Types"></a>
## Value Types

- **uint** - unsigned integer, it doesn't have a sign for positive or negative numbers. This form is a alias(shorthand) form of unint255, the maximum number of digits in binary form for a uint.

- **int** - signed integer, holds a range of positive and negative numbers. An alias for int255, the max digit in binary form for a int
- **bool** - boolean, either true or false, on default is false.
- **enum** - enumerate, a set of pre-defined choices. The chosen value use the datatype of the enum variable name; for example:
```sol
     enum Choice {
        Up,
        Down,
        Left,
        Right
    }

    Choice choice = Choice.Up;
```
- enum choices defined in other programs can be called separately like this: "Example.Choice.Right"
- To print strings in a solidity contract we use the **string** or **bytes** for messages larger than 32 bytes and **bytes32** for messages with less. Bytes and strings are dynamically allocated while bytes32 are pre-emptively allocated

- constructors in a contract can be used to test contracts
 
- To run a code in a solidity contract without any testing, we use an "unchecked" method and add the inner statement.
- To display a unint/int in hex mode, use "console.logBytes32();"

<a name="Storage Variables"></a>
## Storage Variables

Solidity store variables of a contract scope in a 32 byte(256 bits) contiguous storage(state) slots. This is important to reduce the amount of money(Gas) needed to read/writing the storage slot of a contract in the Ethereum network.

Functions in Solidity are designed to be memory efficient. To implement this efficiency, most contract programmers implement low leveling programming in their solidity code. One of the following is using Etherium Virtual Machine(EVM) Opcodes.
Most undeclared variables are assumed to contain 0 in their storage except variables with the "constant" modifier where they shift the start of the storage variable with the size required to store the constant variable.

In Solidity, declaring a storage variable is as simple as declaring the variable inside of the contract:

contract Contract {
	bool myVariable;
}

<a name="Functions"></a>
## Functions

Functions are blocks of code in a Etherium contract designed to perform a certain action. This action can either have one of four visibility keywords:
- **private:** this function is called from within the contract
- **internal:** this function is called within the contract, any other functions inheriting this function can call said function
- **public:** this function can be called from either inside or outside the contract
- **external:** this function can only be called from outside the contract's EVM. This is used as an entry point for the contract.

and one of three state mutability(changeability) keywords:
- **pure:** this is similar to "void" modifier in C++, it doesn't read/store anything in the storage variables.
- **view:** this function can only read storage slots.
- **payable:** this function can store Ether in the contract.

A solidity function is written as follows:
```
function functionName(variable1, variable2,...) visibilityModifier stateModifier returns(variable/datatype){
    return variable/finalResult;
}
```
One of the main functions in a solidity contract is the **constructor**. This function is called once during the contract's deployment and is used for setting up inital contract values.

In general,In Solidity, functions are blocks of code with specified visibility (private, internal, public, external) and mutability (pure, view, payable), used to define contract behavior, with the constructor serving as a special function that initializes the contract upon deployment
Solidity is a high-level, statically-typed programming language designed for writing smart contracts on the Ethereum blockchain. It enables decentralized applications (dApps), trustless transactions, and immutable logic.

🔹 Value Types in Solidity
1. uint / int
uint: Unsigned integer (only positive values). Alias for uint256.

int: Signed integer (positive and negative values). Alias for int256.


uint age = 30;       // uint256
int balance = -100;  // int256
2. bool
Stores either true or false. Default value is false.


bool isVerified = true;
3. enum
Used to define a set of named constants (choices).


enum Direction { Up, Down, Left, Right }

Direction myDirection = Direction.Up;
Access from another contract:


Example.Direction choice = Example.Direction.Right;
4. string / bytes / bytes32
string: Used for UTF-8 encoded text.

bytes: Dynamic array of bytes.

bytes32: Fixed-size (32 bytes) byte array — more gas efficient for short messages.


string name = "Alice";
bytes data = "Dynamic message";
bytes32 fixedMsg = "ShortMsg";
🔹 Constructors in Solidity
A constructor is a special function that runs only once, at contract deployment. Used to initialize state variables.


contract MyContract {
    uint public age;

    constructor(uint _age) {
        age = _age;
    }
}
🔹 Unchecked Blocks
Use unchecked {} to skip overflow checks and save gas (used for optimization, not testing):


function addUnchecked(uint x, uint y) public pure returns (uint) {
    unchecked {
        return x + y;
    }
}
