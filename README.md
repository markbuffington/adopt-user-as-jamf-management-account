# adopt-user-as-jamf-management-account

## Background:

In certain Automated Device Enrollment workflows of Macs with Jamf Pro, an IT admin may be required to create a local administrator account as part of their PreStage Enrollment. This account, also referred to as a "Managed Administrator" by Apple, is required to be created in order to either make the user created by the macOS Setup Assistant a Standard user, or when skipping user account creation completely in the Setup Assistant. (Note: This account should not be confused with the "Jamf Management Account," which is an account that can be created by the Jamf management framework after MDM enrollment completes.

This enrollment flow is common when using applications like **Jamf Connect** which can provision and create local users based on cloud identity provider authentication. 

Currently in Jamf Pro, this requires an IT admin to define a common, shared username and password for the managed administrator account for any computer which enrolls in the PreStage Enrollment. In most deployments, this should be avoided to minimize risk from using shared credentials for user accounts across multiple devices. 

Going a step further, you and your organization may wish to not have *any* local administrator accounts for IT staff, as your management tools are able to complete actions where privileges may need escalated. If disk access or user password resets are required, a FileVault personal recovery key (PRK) that's unique per each computer may be a more desirable and method of access instead.


