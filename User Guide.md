**Io.vault user guide**

# Technology Background 
 
 The unique aspect of the io.vault product is the underlying technology we have used which is based on MPC-TSS cryptography (multi-party computation and threshold signature schemes).  *What this technology does is remove the single point of failure inherent to the traditional way of holding any blockchain based digital asset: the private key.*
 
## **Public private key pairs**

Normally, when holding digital assets directly (i.e. not via an exchange or 3rd party custodian) the blockchain doesn’t know your name - just a “public address” (*e.g. 1Jc7vYQHCnmdyhbpcv5o3pYtUbH6Sk139z*) and your balance of assets is “owned” by this address. 

In order to move your assets anywhere else you need the public address’ corresponding “private key” to sign any transaction, which is then verified by the blockchain network before the transaction is processed.

This private key is simply a string of characters (*e.g. 310fe2e677a3ad28acb91d2645bb33882f015ab11e59dce9d2a72905979e3cb6*) that is used to cryptographically prove ownership of its corresponding public address through cryptographic functions (i.e. “signing”).  

The issue arises when you think about ownership - since there is no name attached to your public address and it is only controlled by the private key.  Anyone who manages to gain access to this private key can take complete control of any assets associated with your public address and send them anywhere they like!  

There are many examples of this, where both individuals and companies have had their private key compromised, resulting in a total loss of their assets.  

## MPC-TSS
TSS (threshold signature schemes)  technology eliminates the use of a single private key and instead uses a customizable number of “secret shares” to accomplish the same feat of signing a transaction for a corresponding public address.  In addition to being able to customize the number of secret shares you can also set a “threshold” which determines how many secret shares are required in order to generate a signature.  
This means that you could have many different secret shares held in different locations, with different people, and if one of them was stolen no assets could be stolen.  

However, an issue arises when you want to actually sign a transaction, because you still need to combine the necessary number of shares in the same place in order to do so.  How do we solve this problem?
This is where multi-party computation (MPC) comes into play.  The MPC technology allows devices that contain their own secret shares to communicate with one another and produce a signature trustlessly, without ever disclosing to the other devices their own secret share. In doing so, the single point of failure that would normally occur when combining secret shares to generate a signature is eliminated.

The end result is that we now have a technology which allows us to eliminate the single point of failure normally associated with holding self-custody of digital assets.  In addition, it allows users of our product to determine for themselves the level of security for each vault (number of shares, and required threshold) and distribute that signing power across multiple employees instead of relying upon one trusted person to show up to work the next day.

# Introduction to the Io.Vault product

## Concepts

**Vault** - A grouping of wallets for any supported asset(s), which are all controlled by the same underlying secret shares.
		
**Signing Party** - 
A collection of users and their specified devices that contain the secret shares which control a particular vault.
		
**Signing Power** - 
The number of secret shares a user controls on their specified device as part of that particular vault signing party.

**Threshold** - the number of secret shares required to create a valid transaction signature or vault re-share for a particular vault.  

**Reshare Request** - Users may submit a request defining a new vault threshold and signing party, including the creation of a new vault.  This request must then be approved, by reaching the existing vault threshold and “signed” by the existing signing party.  
		
**Asset Card** - an asset card displays the balance, ($) value and the equivalent value in bitcoin, as well as the wallet address of a particular asset within a given vault.  Displayed or hidden asset cards for a given vault can be managed in the “vault settings” tab.

**Deposit Address** - A deposit address is the specific public address on the relevant blockchain/network that is cryptographically controlled by the underlying secret shares of the given vault

**Transaction Request** - A transaction request may be submitted via the dashboard by any user within an organization and is transmitted to the signing party of the vault for which the transaction is to be sent from.  The request defines the network, asset, destination address, and the quantity to be sent.  The request must be approved and signed by members of the signing party for the given vault that have sufficient signing power to meet or exceed the vault threshold.

**Transaction Status**:
	
**Received** - the transaction has been received by a vault

**Pending** - the transaction request is pending approval and signature

**Expired** - the transaction request has expired
	
**Signing** - the transaction request has met the threshold for approval and is pending completion of the signature process

**Failed** - the transaction was either rejected, determined to be invalid by the blockchain node/network, or the MPC signature process failed during signing

**Broadcast** - the transaction has been signed and broadcast successfully to the relevant network.  Broadcast transactions may still remain unconfirmed on the blockchain for some time. Broadcast transactions may still result in an incomplete transaction in certain circumstances, such as interacting incorrectly with a smart contract.

## Application model 

There are two primary components users of Io.Vault interact with: the web-application dashboard and the mobile application.  

The web dashboard is used to view and manage an organization's vaults and transactional activity whereas the mobile application is used by each member of a vault signing party to review transaction or re-share requests and participate in the signing process.

# Getting started
	
## **Accessing the web-dashboard**

The Io.Vault Dashboard can be accessed by visiting vault.iofinnet.com 

Credentials - Initial credentials are provided by your organizations Io.Vault admins, you will be required to reset your password upon logging in for the first time.

## Registering a device

As a user, to register a new device simply login to the mobile application on the device.  Upon logging in on a new device you will be prompted to save a randomly generated, device specific 24 word secret phrase.  This is a required step to enable device recovery (disaster recovery section link here). It is highly recommended to record and store this phrase physically in a safe and secure location.

## **Creating or resharing a vault**
		
### **Creating the request**
				
A re-share request can be made for an existing vault by visiting the “vault settings” section within a specific vault or for a new vault by selecting the “vaults” dropdown and selecting “create new vault”.  

For a new vault you must specify a unique name for the vault, existing vault names cannot be changed.  A user must also specify the vault threshold and define the signing party members, including signing power for each users device.  Defining a signing party is device specific so a user will not appear as an available option until they have successfully registered a device.

## **Approving the request**

All users that are designated as part of the new signing party will receive a request on the device listed in the signing party and must approve the request and participate in the re-share process simultaneously.  
For existing vaults members of the existing signing party must meet the existing threshold by approving and participating in the re-share process as well.

If the current vault threshold can be met with a given user's secret shares, and they are not a part of the new signing party, then it is not required for them to participate in the new re-share process.  

### **Signing the request**

Signing a re-share request for the creation of a new vault requires all members of the signing party to approve and participate in the re-share signing process.  All devices must be unlocked with the io.vault mobile application open and the user signed-in simultaneously for the process to be successful.

## **Depositing into a vault**

The only requirement to deposit into an existing vault is to obtain the appropriate deposit address for the desired asset.  This deposit address can be found by selecting the intended vault in the dashboard and the complete address can be copied directly from the corresponding asset card.  Note that only the initial and trailing 5 characters are displayed for easier visual identification but the copy button will copy the entire address to your device clipboard.

## **Withdrawing from a vault**
		
Creating the requestA transaction request is created on the dashboard by selecting the “new transaction” button.  A user must specify from which vault they are creating the request for as well as the network, asset, public address, and quantity to be sent.  A transaction request expires if it is not completed within two hours by default. 

### **Approving the request**


Upon submission of a transaction request all members of the vault signing party will receive the request on their device to review.  Any user in the organization is capable of creating a transaction request for any vault within the organization so it is important to review the information carefully each time before approving a request.
After reviewing the details users may either elect to approve or reject the transaction.  Users with devices having sufficient signing power to reach the vault threshold must all approve the request before a signature is possible.
Rejecting a transaction request simply notifies the other members of the signing party that you have rejected the transaction and prevents your device from participating in the signing process.  If other members of the signing party are still able to reach the vault threshold they may still complete the transaction.

### **Signing the request**

After a transaction request has the approval of enough signing power to meet the required vault threshold the transaction is ready for signature.  In order for the signature process to begin all devices which approved the transaction must be unlocked with the mobile application open simultaneously.  Users will be required to FaceID to authenticate with their device in order to initiate signing.  All devices must stay unlocked with the application open for the duration of the signing process, which should not be longer than 10 seconds, or the transaction will fail.

# Disaster Recovery Process

When initially creating a vault, consideration should be made in balancing security vs redundancy in the number of shares and signers for a vault.  If a user signing device is lost and there are enough available shares to reach the vault threshold a re-share request can simply be created to issue new shares to a new user device.  If there are not enough shares available the disaster recovery process will be necessary.

Io.Vault implements a unique backup and recovery process for every vault in an organization.  The recovery process uses a unique 24 word phrase for each signing device (generated upon initial sign-in on every new device) to encrypto copies of the secret shares held locally on the device.  Each user is responsible for downloading and storing an up to date encrypted device back-up and for safe-keeping of their 24 word secret phrase in an offline and physically secure location.  

This process must be used when funds cannot be withdrawn from a vault due to the inability to generate a signed transaction.  This can occur for example, by a critical software malfunction, a malicious DDOS attack, a permanent service shutdown, or a critical loss of user secret shares.  

To recover access to a vault, and the assets contained within, members of the signing party with devices containing enough secret shares to reach the vault threshold must obtain their corresponding up to date encrypted back-up files and device specific 24 word secret phrases.  The organization should then use a publicly available, open source script published on github ([here](https://github.com/aq-systems/tss-app-recovery-tool)) on a secure offline computer to generate, for the first time, a valid private key.

# Best Practices

Always use two test transactions after creating a new vault.  First, verify that the deposit address displayed is valid by making a test deposit.  Finally, ownership of the vault and underlying public addresses should be verified by performing a test withdrawal.

Create vaults with redundancy of users and their devices to avoid requiring implementation of the disaster recovery process for instances of a single user losing a signing device.  

Ensure all users are consistently and frequently backing up their device - at a minimum each user device needs to be backed up each time it participates in creation of a new vault or a vault re-share as these processes result in new shares being created locally on the device. 
