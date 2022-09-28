# adopt-user-as-jamf-management-account

## At JNUC, will have last bits with screenshots that were in presentation added to this tonight... <3 Mark


## Background:

In certain Automated Device Enrollment workflows of Macs with Jamf Pro, an IT admin may be required to create a local administrator account as part of their PreStage Enrollment. This account, also referred to as a "Managed Administrator" by Apple, is required to be created in order to either make the user created by the macOS Setup Assistant a Standard user, or when skipping user account creation completely in the Setup Assistant. (Note: This account should not be confused with the "Jamf Management Account," which is an account that can be created by the Jamf management framework after MDM enrollment completes.

This enrollment flow is common when using applications like **Jamf Connect** which can provision and create local users based on cloud identity provider authentication. 

Currently in Jamf Pro, this requires an IT admin to define a common, shared username and password for the managed administrator account for any computer which enrolls in the PreStage Enrollment. In most deployments, this should be avoided to minimize risk from using shared credentials for user accounts across multiple devices. 

Going a step further, you and your organization may wish to not have *any* known passwords for IT administrator accounts, as your management tools are able to complete actions where privileges need escalatation. If disk access or user password resets are required, a FileVault personal recovery key (PRK) that's unique per each computer may be a more desirable and secure method of access instead.

## Workflow Summary:

This workflow allows the Jamf management framework (aka "Jamf Agent") to randomize the password of the additional administrator account created from a Jamf Pro PreStage Enrollment. It does this by "adopting" that account to randomize the password and stores that account's password in Jamf Pro's database as the password for the "Jamf Management Account."

Ongoing, if the password for this account needs to be used, a policy may be targeted to the computer to change the password of a computer's Jamf Management Account to a known password. This action will be logged in the computer's policy history, and after the password is used, an additional policy can be targeted to the computer to randomize that account password again.

## Requirements:

- Additional admin account created from a PreStage created during Setup Assistant
- Jamf Management Account configured in User-Initiated Enrollment settings to use the _exact same credentials_ as the above account
- Extension Attribute to determine whether a Bootstrap Token is escrowed*
- Policy to change the Jamf Management Account password to a randomized value, scoped to a Smart Computer Group which contains the criteria for the bootstrap token being escrowed already.


### Note on Bootstrap Token EA Requirement:

**Warning:** Not including this component into your workflow may result in the first SecureToken user being assigned to the administrator account which has a randomized password that is only known by the Jamf Pro database. This isn't good, and should be avoided. 

By including a check for the existence of a Bootstrap Token before changing the MDM-created admin account to a randomized password, this ensures that the Jamf policy will only run after the primary user of the computer has signed in, received the first SecureToken, and also had the bootstrap token automatically escrowed to Jamf Pro.


## Workflow: Setup Instructions

## Workflow: Deployment Play-by-Play
