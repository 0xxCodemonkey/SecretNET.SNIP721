# Secret.NET NFT (SNIP721) / Secret NFT
**Secret.NET NFT** is a layer on top of the [**Secret.NET client**](https://github.com/0xxCodemonkey/SecretNET) which supports all methods of the reference implementation of the SNIP721 contract.

**The [Secret Network blockchain](https://scrt.network/) (L1 / Cosmos), is the first privacy smart contract blockchain that processes and stores data on-chain in encrypted form (via Intel SGX).** 
This allows [unique use cases](https://docs.scrt.network/secret-network-documentation/secret-network-overview/use-cases) like **Secret NFTs** where you can store public and private data e.g., Encryption Keys, passwords or other secrets.

<p align="center">
  <img src="./resources/Secret.NET_banner.png" type="image/png" width="100%" />
</p>

**SecretNET.NFT** provides typed and documented objects and methods that simplify interaction with a SNIP721 smart contract.

- Implementation => [GitHub - baedrik/snip721-reference-impl](https://github.com/baedrik/snip721-reference-impl) 
- Implementation of the [SNIP-721 specification](https://github.com/SecretFoundation/SNIPs/blob/master/SNIP-721.md) and [SNIP-722 specification](https://github.com/baedrik/snip-722-spec/blob/master/SNIP-722.md).
- See also the [SNIP721 documentation on Secret Network](https://docs.scrt.network/secret-network-documentation/development/snips/snip-721-private-non-fungible-tokens-nfts).

:white_check_mark: **This repository is explicitly intended to serve as a template for custom SNIP721 NFT contracts.**
This makes it easy to create your own customized clients for your own customized contracts.
Of course, the concept can be used for any kind of smart contracts in general.

## Full API-documentation
You can find the **full API-documentation** here => https://0xxcodemonkey.github.io/SecretNET.NFT

# Table of Contents
- [Implementation](#implementation)
  - [Instantiating a SNIP721 Client](#instantiating-a-snip721-client)
  - [Usage](#usage)
- [Implemented methods](#implemented-methods)
  - [Queries](#queries-snip721clientquery)
  - [Transactions](#transactions-snip721clienttx)

# Implementation
The structure of **SecretNET.NFT** is the same as the **SecretNET** client and transactions are accessible via `Tx` property and queries via `Query` property.

All transactions can also be simulated via `Tx.Simulate`.

**All types and methods are documented and eases programming:**

![](resources/VS_IntelliSense.png)
## Instantiating a SNIP721 Client
To instantiate a **SecretNET.SNIP721** client you just have to pass it a [SecretNET client instance](https://github.com/0xxCodemonkey/SecretNET#usage-examples):
```  csharp
var snip721Client =  new SecretNET.NFT.Snip721Client(secretNetworkClient);
```

## Usage
All Methods can be easily called with the payload message like this:
```  csharp
var payloadTransferMsg = new SecretNET.NFT.TransferNftRequest(
              recipientAddress,
              tokenId);
              
var transferMsg = new SecretNET.NFT.MsgTransferNft(
                payloadTransferMsg, 
                snip721ContractAddress, 
                snip721CodeHash);

var transferResult = await snip721Client.Tx.TransferNft(
                transferMsg, 
                txOptions: txOptionsExecute);
```

Many methods also have an overload to make them even easier to call, like this
```  csharp
var transferResult = await snip721Client.Tx.TransferNft(
                snip721ContractAddress, 
                recipientAddress, 
                tokenId, 
                codeHash: snip721CodeHash, 
                txOptions: txOptionsExecute);
```

# Implemented methods
- [Queries](#queries-snip721clientquery)
  - [GetAllNftInfo](#getallnftinfo)
  - [GetAllTokens](#getalltokens)
  - [GetApprovedForAll](#getapprovedforall)
  - [GetBatchNftDossier](#getbatchnftdossier)
  - [GetContractConfig](#getcontractconfig)
  - [GetContractInfo](#gettokeninfo)
  - [GetImplementsNonTransferableTokens](#getimplementsnontransferabletokens)
  - [GetImplementsTokenSubtype](#getimplementstokensubtype)
  - [GetInventoryApprovals](#getinventoryapprovals)
  - [GetIsTransferable](#getistransferable)
  - [GetIsUnwrapped](#getisunwrapped)
  - [GetMinters](#getminters)
  - [GetNftDossier](#getnftdossier)
  - [GetNftInfo](#getnftinfo)
  - [GetNumTokens](#getnumtokens)
  - [GetNumTokensOfOwner](#getnumtokensofowner)
  - [GetOwnerOf](#getownerof)
  - [GetPrivateMetadata](#getprivatemetadata)
  - [GetRegisteredCodeHash](#getregisteredcodehash)
  - [GetRoyaltyInfo](#getroyaltyinfo)
  - [GetTokenApprovals](#gettokenapprovals)
  - [GetTokens](#gettokens)
  - [GetTransactionHistory](#gettransactionhistory)
  - [GetVerifyTransferApproval](#getverifytransferapproval)
- [Transactions](#transactions-snip721clienttx)
  - [AddMinter](#addminter)
  - [Approve](#approve)
  - [ApproveAll](#approveall)
  - [BatchBurnNft](#batchburnnft)
  - [BatchMintNft](#batchmintnft)
  - [BatchSendNft](#batchsendnft)
  - [BatchTransferNft](#batchtransfernft)
  - [BurnNft](#burnnft)
  - [ChangeAdmin](#changeadmin)
  - [CreateViewingKey](#createviewingkey)
  - [Instantiate (new contract)](#instantiate-new-contract)
  - [MakeOwnershipPrivate](#makeownershipprivate)
  - [MintNft](#mintnft)
  - [MintNftClones](#mintnftclones)
  - [RegisterReceiveNft](#registerreceivenft)
  - [RemoveMinters](#removeminters)
  - [Reveal](#reveal)
  - [Revoke](#revoke)
  - [RevokeAll](#revokeall)
  - [RevokePermit](#revokepermit)
  - [SendNft](#sendnft)

## Queries (`Snip721Client.Query`)
### [GetAllNftInfo](https://0xxcodemonkey.github.io/SecretNET.NFT/html/M-SecretNET.NFT.Snip721Querier.GetAllNftInfo.htm)
AllNftInfo displays the result of both OwnerOf and NftInfo in a single query. This is provided for CW-721 compliance, but for more complete information about a token, use NftDossier, which will include private metadata and view_owner and view_private_metadata approvals if the querier is permitted to view this information.
``` csharp
GetAllNftInfo(
	string contractAddress,
	string tokenId,
	ViewerInfo viewerInfo,
	Nullable<Permit> permit,
	Nullable<bool> includeExpired,
	Nullable<string> codeHash
);
```
### [GetAllTokens](https://0xxcodemonkey.github.io/SecretNET.NFT/html/M-SecretNET.NFT.Snip721Querier.GetAllTokens.htm)
AllTokens returns an optionally paginated list of all the token IDs controlled by the contract. If the contract's token supply is private, only an authenticated minter's address will be allowed to perform this query. When paginating, supply the last token ID received in a response as the start_after token ID of the next query to continue listing where the previous query stopped.
``` csharp
GetAllTokens(
	string contractAddress,
	string address,
	string viewingKey,
	Nullable<Permit> permit,
	string startAfter,
	Nullable<int> limit,
	Nullable<string> codeHash
);
```
### [GetApprovedForAll](https://0xxcodemonkey.github.io/SecretNET.NFT/html/M-SecretNET.NFT.Snip721Querier.GetApprovedForAll.htm)
ApprovedForAll displays all the addresses that have approval to transfer all of the specified owner's tokens. This is provided to comply with CW-721 specification, but because approvals are private on Secret Network, if the owner's viewing key is not provided, no approvals will be displayed. For a more complete list of inventory-wide approvals, the owner should use InventoryApprovals which also includes view_owner and view_private_metadata approvals.
``` csharp
GetApprovedForAll(
	string contractAddress,
	string tokenId,
	string viewingKey,
	Nullable<Permit> permit,
	Nullable<bool> includeExpired,
	Nullable<string> codeHash
)
```
### [GetBatchNftDossier](https://0xxcodemonkey.github.io/SecretNET.NFT/html/M-SecretNET.NFT.Snip721Querier.GetBatchNftDossier.htm)
Displays all the information about multiple tokens that the viewer has permission to see. This may include the owner, the public metadata, the private metadata, royalty information, mint run information, whether the token is unwrapped, whether the token is transferable, and the token and inventory approvals.
``` csharp
GetBatchNftDossier(
	string contractAddress,
	string[] tokenIds,
	ViewerInfo viewerInfo,
	Nullable<Permit> permit,
	Nullable<bool> includeExpired,
	Nullable<string> codeHash
);
```
### [GetContractConfig](https://0xxcodemonkey.github.io/SecretNET.NFT/html/M-SecretNET.NFT.Snip721Querier.GetContractConfig.htm)
ContractConfig returns the configuration values that were selected when the contract was instantiated. See Config for an explanation of the configuration options. This query is not authenticated.
``` csharp
GetContractConfig(
	string contractAddress,
	Nullable<string> codeHash
);
```
### [GetContractInfo](https://0xxcodemonkey.github.io/SecretNET.NFT/html/M-SecretNET.NFT.Snip721Querier.GetContractInfo.htm)
ContractInfo returns the contract's name and symbol. This query is not authenticated.
``` csharp
GetContractInfo(
	string contractAddress,
	Nullable<string> codeHash
);
```
### [GetImplementsNonTransferableTokens](https://0xxcodemonkey.github.io/SecretNET.NFT/html/M-SecretNET.NFT.Snip721Querier.GetImplementsNonTransferableTokens.htm)
ImplementsNonTransferableTokens is a SNIP-722 query which indicates whether the contract implements non-transferable tokens. Because legacy SNIP-721 contracts do not implement this query and do not implement non-transferable tokens, any use of this query should always check for an error response, and if the response is an error, it can be considered that the contract does not implement non-transferable tokens. Because message parsing ignores input fields that a contract does not expect, this query should be used before attempting to mint a non-transferable token. If the message is sent to a SNIP-721 contract that does not implement non-transferable tokens, the transferable field will just be ignored and the resulting NFT will still be created, but will always be transferable.
``` csharp
GetImplementsNonTransferableTokens(
	string contractAddress,
	Nullable<string> codeHash
);
```
### [GetImplementsTokenSubtype](https://0xxcodemonkey.github.io/SecretNET.NFT/html/M-SecretNET.NFT.Snip721Querier.GetImplementsTokenSubtype.htm)
ImplementsTokenSubtype is a SNIP-722 query which indicates whether the contract implements the token_subtype Extension field. Because legacy SNIP-721 contracts do not implement this query and do not implement token subtypes, any use of this query should always check for an error response, and if the response is an error, it can be considered that the contract does not implement subtypes. Because message parsing ignores input fields that a contract does not expect, this query should be used before attempting a message that uses the token_subtype Extension field. If the message is sent to a SNIP-721 contract that does not implement token_subtype, that field will just be ignored and the resulting NFT will still be created/updated, but without a token_subtype.
``` csharp
GetImplementsTokenSubtype(
	string contractAddress,
	Nullable<string> codeHash
);
```
### [GetInventoryApprovals](https://0xxcodemonkey.github.io/SecretNET.NFT/html/M-SecretNET.NFT.Snip721Querier.GetInventoryApprovals.htm)
InventoryApprovals returns whether all the address' tokens have public ownership and/or public display of private metadata, and lists all the inventory-wide approvals the address has granted. Only the viewing key for this specified address will be accepted. (This query MUST be authenticated)
``` csharp
GetInventoryApprovals(
	string contractAddress,
	string tokenId,
	string viewingKey,
	Nullable<Permit> permit,
	Nullable<bool> includeExpired,
	Nullable<string> codeHash
);
```
### [GetIsTransferable](https://0xxcodemonkey.github.io/SecretNET.NFT/html/M-SecretNET.NFT.Snip721Querier.GetIsTransferable.htm)
IsTransferable is a SNIP-722 query that indicates whether the token is transferable. This query is not authenticated.
``` csharp
GetIsTransferable(
	string contractAddress,
	string tokenId,
	Nullable<string> codeHash
);
```
### [GetIsUnwrapped](https://0xxcodemonkey.github.io/SecretNET.NFT/html/M-SecretNET.NFT.Snip721Querier.GetIsUnwrapped.htm)
IsUnwrapped indicates whether the token has been unwrapped. If sealed metadata is not enabled, all tokens are considered to be unwrapped. This query is not authenticated.
``` csharp
GetIsUnwrapped(
	string contractAddress,
	string tokenId,
	Nullable<string> codeHash
);
```
### [GetMinters](https://0xxcodemonkey.github.io/SecretNET.NFT/html/M-SecretNET.NFT.Snip721Querier.GetMinters.htm)
Minters returns the list of addresses that are authorized to mint tokens. This query is not authenticated.
``` csharp
GetMinters(
	string contractAddress,
	Nullable<string> codeHash
);
```
### [GetNftDossier](https://0xxcodemonkey.github.io/SecretNET.NFT/html/M-SecretNET.NFT.Snip721Querier.GetNftDossier.htm)
NftDossier returns all the information about a token that the viewer is permitted to view. If no viewer is provided, NftDossier will only display the information that has been made public. The response may include the owner, the public metadata, the private metadata, the reason the private metadata is not viewable, the royalty information, the mint run information, whether the token is transferable, whether ownership is public, whether the private metadata is public, and (if the querier is the owner,) the approvals for this token as well as the inventory-wide approvals for the owner. This implementation will only display a token's royalty recipient addresses if the querier has permission to transfer the token. SNIP-722 adds a transferable field to the NftDossier response. SNIP-723 (specification to be written) adds an unwrapped field which is false if private metadata for this token is sealed.
``` csharp
GetNftDossier(
	string contractAddress,
	string tokenId,
	ViewerInfo viewerInfo,
	Nullable<Permit> permit,
	Nullable<bool> includeExpired,
	Nullable<string> codeHash
);
```
### [GetNftInfo](https://0xxcodemonkey.github.io/SecretNET.NFT/html/M-SecretNET.NFT.Snip721Querier.GetNftInfo.htm)
NftInfo returns the public metadata of a token. It follows CW-721 specification, which is based on ERC-721 Metadata JSON Schema. At most, one of the fields token_uri OR extension will be defined.
``` csharp
GetNftInfo(
	string contractAddress,
	string tokenId,
	Nullable<string> codeHash
);
```
### [GetNumTokens](https://0xxcodemonkey.github.io/SecretNET.NFT/html/M-SecretNET.NFT.Snip721Querier.GetNumTokens.htm)
NumTokens returns the number of tokens controlled by the contract. If the contract's token supply is private, only an authenticated minter's address will be allowed to perform this query.
``` csharp
GetNumTokens(
	string contractAddress,
	string address,
	string viewingKey,
	Nullable<Permit> permit,
	Nullable<string> codeHash
);
```
### [GetNumTokensOfOwner](https://0xxcodemonkey.github.io/SecretNET.NFT/html/M-SecretNET.NFT.Snip721Querier.GetNumTokensOfOwner.htm)
Displays the number of tokens that the querier has permission to see the owner and that belong to the specified address.
``` csharp
GetNumTokensOfOwner(
	string contractAddress,
	string owner,
	string viewer,
	string viewingKey,
	Nullable<Permit> permit,
	Nullable<string> codeHash
);
```
### [GetOwnerOf](https://0xxcodemonkey.github.io/SecretNET.NFT/html/M-SecretNET.NFT.Snip721Querier.GetOwnerOf.htm)
OwnerOf returns the owner of the specified token if the querier is the owner or has been granted permission to view the owner. If the querier is the owner, OwnerOf will also display all the addresses that have been given transfer permission. The transfer approval list is provided as part of CW-721 compliance; however, the token owner is advised to use NftDossier for a more complete list that includes view_owner and view_private_metadata approvals (which CW-721 is not capable of keeping private). If no viewer is provided, OwnerOf will only display the owner if ownership is public for this token.
``` csharp
GetOwnerOf(
	string contractAddress,
	string tokenId,
	ViewerInfo viewerInfo,
	Nullable<Permit> permit,
	Nullable<bool> includeExpired,
	Nullable<string> codeHash
);
```
### [GetPrivateMetadata](https://0xxcodemonkey.github.io/SecretNET.NFT/html/M-SecretNET.NFT.Snip721Querier.GetPrivateMetadata.htm)
PrivateMetadata returns the private metadata of a token if the querier is permitted to view it. It follows CW-721 metadata specification, which is based on ERC-721 Metadata JSON Schema. At most, one of the fields token_uri OR extension will be defined. If the metadata is sealed, no one is permitted to view it until it has been unwrapped with Reveal. If no viewer is provided, PrivateMetadata will only display the private metadata if the private metadata is public for this token.
``` csharp
GetPrivateMetadata(
	string contractAddress,
	string tokenId,
	ViewerInfo viewerInfo,
	Nullable<Permit> permit,
	Nullable<string> codeHash
);
```
### [GetRegisteredCodeHash](https://0xxcodemonkey.github.io/SecretNET.NFT/html/M-SecretNET.NFT.Snip721Querier.GetRegisteredCodeHash.htm)
RegisteredCodeHash will display the code hash of the specified contract if it has registered its receiver interface and will indicate whether the contract implements BatchReceiveNft.
``` csharp
GetRegisteredCodeHash(
	string contractAddress,
	Nullable<string> codeHash
);
```
### [GetRoyaltyInfo](https://0xxcodemonkey.github.io/SecretNET.NFT/html/M-SecretNET.NFT.Snip721Querier.GetRoyaltyInfo.htm)
If a token_id is provided in the request, RoyaltyInfo returns the royalty information for that token. This implementation will only display a token's royalty recipient addresses if the querier has permission to transfer the token. If no token_id is requested, RoyaltyInfo displays the default royalty information for the contract. This implementation will only display the contract's default royalty recipient addresses if the querier is an authorized minter.
``` csharp
GetRoyaltyInfo(
	string contractAddress,
	string tokenId,
	ViewerInfo viewerInfo,
	Nullable<Permit> permit,
	Nullable<string> codeHash
);
```
### [GetTokenApprovals](https://0xxcodemonkey.github.io/SecretNET.NFT/html/M-SecretNET.NFT.Snip721Querier.GetTokenApprovals.htm)
TokenApprovals returns whether the owner and private metadata of a token is public, and lists all the approvals specific to this token. Only the token's owner may perform TokenApprovals. (This query MUST be authenticated)
``` csharp
GetTokenApprovals(
	string contractAddress,
	string tokenId,
	string viewingKey,
	Nullable<Permit> permit,
	Nullable<bool> includeExpired,
	Nullable<string> codeHash
);
```
### [GetTokens](https://0xxcodemonkey.github.io/SecretNET.NFT/html/M-SecretNET.NFT.Snip721Querier.GetTokens.htm)
Tokens displays an optionally paginated list of all the token IDs that belong to the specified owner. It will only display the owner's tokens on which the querier has view_owner permission. If no viewing key is provided, it will only display the owner's tokens that have public ownership. When paginating, supply the last token ID received in a response as the start_after string of the next query to continue listing where the previous query stopped.
``` csharp
GetTokens(
	string contractAddress,
	string owner,
	string viewer,
	string viewingKey,
	Nullable<Permit> permit,
	string startAfter,
	Nullable<int> limit,
	Nullable<string> codeHash
);
```
### [GetTransactionHistory](https://0xxcodemonkey.github.io/SecretNET.NFT/html/M-SecretNET.NFT.Snip721Querier.GetTransactionHistory.htm)
TransactionHistory displays an optionally paginated list of transactions (mint, burn, and transfer) in reverse chronological order that involve the specified address. (This query MUST be authenticated)
``` csharp
GetTransactionHistory(
	string contractAddress,
	string address,
	string viewingKey,
	Nullable<Permit> permit,
	Nullable<int> page,
	Nullable<int> pageSize,
	Nullable<string> codeHash
);
```
### [GetVerifyTransferApproval](https://0xxcodemonkey.github.io/SecretNET.NFT/html/M-SecretNET.NFT.Snip721Querier.GetVerifyTransferApproval.htm)
VerifyTransferApproval will verify that the specified address has approval to transfer the entire provided list of tokens. As explained above, queries may experience a delay in revealing expired approvals, so it is possible that a transfer attempt will still fail even after being verified by VerifyTransferApproval. If the address does not have transfer approval on all the tokens, the response will indicate the first token encountered that can not be transferred by the address. Because the intent of VerifyTransferApproval is to provide contracts a way to know before-hand whether an attempt to transfer tokens will fail, this implementation will consider any SNIP-722 non-transferable token as unapproved for transfer. (This query MUST be authenticated)
``` csharp
GetVerifyTransferApproval(
	string contractAddress,
	string[] tokenIds,
	string address,
	string viewingKey,
	Nullable<Permit> permit,
	Nullable<string> codeHash
);
```

## Transactions (`Snip721Client.Tx`)
### AddMinter

``` csharp

```
### Approve

``` csharp

```
### ApproveAll

``` csharp

```
### BatchBurnNft

``` csharp

```
### BatchMintNft

``` csharp

```
### BatchSendNft

``` csharp

```
### BatchTransferNft

``` csharp

```
### BurnNft

``` csharp

```
### ChangeAdmin

``` csharp

```
### CreateViewingKey

``` csharp

```
### Instantiate (new contract)

``` csharp

```
### MakeOwnershipPrivate

``` csharp

```
### MintNft

``` csharp

```
### MintNftClones

``` csharp

```
### RegisterReceiveNft

``` csharp

```
### RemoveMinters

``` csharp

```
### Reveal

``` csharp

```
### Revoke

``` csharp

```
### RevokeAll

``` csharp

```
### RevokePermit

``` csharp

```
### SendNft

``` csharp

```
