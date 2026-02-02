,45 PDX-License-Identifier: MIT
pragma solidity ^0.8.20contract BaseLoveNotes {
    struct LoveNote {
        address sender;
        string message;
        uint256 timestamp;
        uint256 tip;
    } 1

    LoveNote[] public allNotes;
    event NewLoveNote(address indexed from, string message, uint256 tip);

    // Function to send love to the blockchain
    function sendLove(string memory _message) public payable {
        require(bytes(_message).length > 0, "Love cannot be empty!");
        
        LoveNote memory newNote = LoveNote({
            sender: msg.sender,
            message: _message,
            timestamp: block.timestamp,
            tip: msg.value
        });

        allNotes.push(newNote);

        emit NewLoveNote(msg.sender, _message, msg.value);
    }

    // Function to see how much love has been shared
    function getTotalNotes() public view returns (uint256) {
        return allNotes.length;
    }
}
