# Technical

The goal of Dexoshi is to provide simple UX and gameplay without needing understand crypto jargon. On the surface, players can create a Twitter account, execute commands on the platform and automagically get tokens. But there is a a lot of meta transactions, on-chain interactions and keccak256 hashes. Lots of keccak256 hashes.

## Semi Custodial Tokens (Cards)

Tokens by default are owned by an admin. This allows players to not worry about setting up a wallet. Transaction fees are paid by the admin and tokens are sent to your "Twitter address".

Below are some admin functions

```solidity
function adminMint(address _to, uint256 _tokenId, uint256 _amount) public {
    require(msg.sender == ADMIN, "Only admin can mint");
    _mint(_to, _tokenId, _amount, "");
}
```

```solidity
function adminSafeTransferFrom(address _from, address _to, uint256 _tokenId, uint256 _amount) public {
    require(msg.sender == ADMIN, "Only admin can transfer");
    require(hasCustody[_from] == false, "Admin does not have custody");
    _safeTransferFrom(_from, _to, _tokenId, _amount, "");
}
```

Notice `adminSafeTransferFrom` has a `hasCustody` mapping. This variable enables certain address to toggle custody. For example, a player can send their tokens from a custodial address to a non-custodial (metamask) address and `setCustody` to `true`

```solidity
function setCustody(bool _bool) public {
    hasCustody[tx.origin] = _bool;
}
```

Dexoshi contract allows tokens to be non-custodial for better UX or have custody for true ownership.

## "Twitter Addresses"

If a player never has a wallet, how can they receive tokens? What address do you send the tokens to?

Great question! This can be done by mapping a user's twitter Id to an address. Each twitter account has a unique twitter id.

{% embed url="https://www.codeofaninja.com/tools/find-twitter-id/" %}

For example, `@elonmusk` has twitter ID 44196394.

![](https://user-images.githubusercontent.com/19412160/210456096-f5ffd607-bf93-4cc6-8861-fbe80de63904.png)

The contract can create an address by hashing the Twitter identifier

```solidity
function twitterIdToAddress(uint64 _twitterId) public pure returns(address) {
    return address(bytes20(sha256(abi.encodePacked(_twitterId))));
}
```

This means each Twitter Id has a unique 0x address :tada:

## Sell For Free

The contract also expands to enable meta-transactions on OpenSea.

What does this mean?

By default everytime a player wants to sell an NFT, they must pay a small fee to list on chain. Enabling meta-transactions allows players to sell for free!

In fact, Dexoshi does not require players to own any crypto!

### Steps

* Create a metamask account with a non-custodial `0xADDRESS`
* Tweet `@dexoshi transfer <0xADDRESS> <CARD_ID> <AMOUNT>`
* Visit OpenSea, connect to metamask and start selling.

On a technical level. The contract whitelists OpenSea's proxy contract to set approval for all.

```solidity
function isApprovedForAll(
    address _owner,
    address _operator
) public override view returns (bool isOperator) {
    if (_operator == address(0x1E0049783F008A0085193E00003D00cd54003c71)) {
        return true;
    }
    return ERC1155.isApprovedForAll(_owner, _operator);
}
```
