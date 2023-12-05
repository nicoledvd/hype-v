# ADDS Commands
# Install ADDS 
install -windowsfeature ad-domain-services -IncludeAllSubFeature -IncludeManagementTools4

install-ADDSForest -DomainName "nicole.ca" -InstallDns

# View Domain Controller Information
Get-ADDomainController -Filter * | Select-Object Name, Domain, Forest, OSVersion, Site 
# Create Organizational Unit (OU)
New-ADOrganizationalUnit -Name "NewOU" -Path "OU=ParentOU,DC=yourdomain,DC=com" 
# Create User Account
New-ADUser -SamAccountName "NewUser" -UserPrincipalName "NewUser@yourdomain.com" -GivenName "FirstName" -Surname "LastName" -Enabled $true -AccountPassword (ConvertTo-SecureString -AsPlainText "Password123" -Force) -PassThru 
# Add User to Group
Add-ADGroupMember -Identity "GroupName" -Members "NewUser" 
# Remove User from Group
Remove-ADGroupMember -Identity "GroupName" -Members "UserToRemove" 
# Get Group Members
Get-ADGroupMember -Identity "GroupName" 

