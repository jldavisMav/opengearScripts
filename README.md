# opengearScripts
Scripts written for use with Opengear devices

Custom scripts should be written to /etc/config/scripts, per Opengear support. You may need to create the scripts directory manually.
Scripts that are run by the autoresponder are run as root, and will need to make sure that the permissions are set accordingly (for my testing scripts were owned by root and set with 777 permissions).

### enable-wifi: 
Designed to be run as an autoresponder for SMS messaging, will enable wifi temporarily or send information on the cellular modem state (connection state, signal strength, and IP address). Script is looking for keywords wifi # or cell. Script does not care about case of commands and will not respond to other commands. No security is implemented as part of the script, so if security is a concern it is suggested it be done via the autoresponse configuration (list of allowed cell numbers and/or regex check of input). Keep in mind, scripting on Opengear is somewhat limited due to the small OS installation.
  * Wifi #: By sending the SMS message Wifi followed by a number, the Opengear (assuming it is appropriately equipped) will enable the local wifi access point for a number of hours equal to the number. The script will send a reply to the number that sent the message saying that the wifi is being enabled for that time, and will send another message when the wifi is disabled. During the delay between enable and disable script is in a sleep state, not a cron job.
  * Cell: A simple request with the word cell will respond back with the modem state (connected or disconnected), radio signal strength (in negative decibels), and public IP address of the modem.
