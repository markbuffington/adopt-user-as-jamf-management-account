# adopt-user-as-jamf-management-account

## Summary:

In certain Automated Device Enrollment workflows of Macs with Jamf Pro, an IT admin may be required to create a local administrator account as part of their PreStage Enrollment. This account, also referred to as a "Managed Administrator" by Apple, is required to be created in order to either make the user created by the macOS Setup Assistant a Standard user, or when skipping user account creation completely in the Setup Assistant. 

This enrollment flow is common when using applications like **Jamf Connect** which can provision and create local users based on cloud identity provider authentication. 

Currently in Jamf Pro, this requires an IT admin to define a common, shared username and password for the managed administrator account for any computer which enrolls in the PreStage Enrollment. In most deployments, this should be avoided to minimize risk from using shared credentials. Further, you may 

This can be problematic when:
- Your organization 
