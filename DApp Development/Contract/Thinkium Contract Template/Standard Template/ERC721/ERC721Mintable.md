# Contract template

## ERC721 tokens can be minted
> The ERC721 token is a non-homogeneous token. The fully functional ERC721 token contains the metadata and enumerability of ERC721.
> The mineable ERC721 token has a public casting method that only the casting manager can call.

[Contract Document: ERC721Mintable.sol](https://github.com/TxCodeGroup/ContractTemplate/blob/master/contracts/ERC721/ERC721Mintable.sol)

[test scripts: ERC721Mintable.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/test/ERC721/ERC721Mintable.js)

[Deployment script: 22_deploy_ERC721Mintable.js](https://github.com/TxCodeGroup/ContractTemplate/blob/master/migrations/22_deploy_ERC721Mintable.js)

### Define the following variables when deploying the contract
```javascript
string memory name,     //Token name
string memory symbol,   //tokens for
string memory baseURI,   //Token base link
```
### Calling methods
```javascript
// Return the token name
name() public view returns (string memory)
// Return token abbreviation
symbol() public view returns (string memory)
// Token base link address
BaseURI external View returns (String Memory)
// Return the data connection address according to tokenID
tokenURI(uint256 tokenId) external view returns (string memory)
// Returns the number of tokens owned by the specified account
balanceOf(address owner) public view returns (uint256)
// Returns the owner according to tokenID
ownerOf(uint256 tokenId) public view returns (address)
// Approve tokens
approve(address to, uint256 tokenId) public
// Get the approved address of the token ID; If no address is set or tokenID does not exist, zero is returned; .
getApproved(uint256 tokenId) public view returns (address)
// Approve all the owner's tokens to the specified address
setApprovalForAll(address to, bool approved) public
// Get whether the operator approves all tokens to the specified address
isApprovedForAll(address owner, address operator) public view returns (bool)
// Send approval
transferFrom(address from, address to, uint256 tokenId) public
// Securely send the approval
safeTransferFrom(address from, address to, uint256 tokenId) public
// Gets the token ID at the given index of the token list for the owner of the request
tokenOfOwnerByIndex(address owner, uint256 index) public view returns (uint256)
// Get the total amount of tokens for the contract
totalSupply() public view returns (uint256)
// Get tokens by indexing
tokenByIndex(uint256 index) public view returns (uint256)
// Coinage method
mint(address to, uint256 tokenId) public onlyMinter returns (bool)
// Safe coinage method
safeMint(address to, uint256 tokenId) public onlyMinter returns (bool)
// Minting method with URI
mintWithTokenURI(address to, uint256 tokenId, string memory tokenURI) public onlyMinter returns (bool)
// Query whether the specified address has the right to mint coins
IsMinter (Address Account) Public View returns (bool)
// Add the coinage to the specified address. Only the address with the coinage can be added
Public onlyMinter addMinter (the address of the account)
// Revoke the coinage of the currently sent account
renounceMinter() public       
```
