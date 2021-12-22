# Ubuntu-Redis-Config
This guide is for Ubuntu 20.04 and running Redis with multiple instances. Also included is a section on how to setup firewall rules for ufw and joining to an Active Directory domain.

### Notes:
****This guide assumes your running as root*</br>
****You may change the default Redis config to your liking, ex. we need a lot of databases so I've changed it to 50 while you may not need that many you can leave it at the default value of 16*</br>
****Suggestions or edits are welcome!*

## Let's Begin!
### Check for updates and install
`apt-get update && apt-get upgrade -y`

## Redis Setup
[a link](https://github.com/nutt318/Ubuntu-Redis-Config/blob/main/Setup-Firewall-Rules.md)
