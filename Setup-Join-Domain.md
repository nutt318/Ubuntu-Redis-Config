## Install required packages
`apt-get install -y sssd-ad sssd-tools realmd adcli`

## Test discover domain 
`realm discover domainname.local`

## Join server to domain
`sudo realm join -v -U yourusername DOMAINNAME.LOCAL`

## Test if joined to domain (configured should say Kerberos-member)
`realm list`

## To permit only one Active Directory group to logon use the following command
`realm permit -g redisadminsecgroup@domainname.local`

## To give sudo permissions to an Active Directory group
`visudo`

## Added the following line to config file and save
`%redisadminsecgroup@domainname.local      ALL=(ALL)       ALL`
 
##  Modify pam to automatically create a home directory for AD users
`pam-auth-update`
Check "activate mkhomedir". Tab and hit Enter to select OK

## Test SSH Login
`yourusername@domainname.local`
