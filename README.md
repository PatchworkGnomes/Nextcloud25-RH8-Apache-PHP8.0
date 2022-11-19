# Nextcloud25-RH8-Apache-PHP8.0

This was a small project for a friend a while ago, they suggested I post it on GitHub...
<br />
So, please…without hesitation, give me feedback.  More important, give me the best practice. I have no qualms with people showing and telling me how to better my limited knowledge.
<br />
<br />
Quote by Ram Dass: (or << Backtrack)<br /> 
“The quieter you become, the more you can hear.”

## Dependencies

Keep in mind of Internal and External DNS and rules on your routers\firewalls, assuming you want this to be public.
Also note that the versions may be different, based on when you install
* NextCloud Hub 3 (25.0.1)
* Red Hat Enterprise Linux 8.7 (Ootpa)
* PHP 8.0.20
* Apache/2.4.37 (Red Hat Enterprise Linux)
* certbot 1.22.0
* Ver 15.1 Distrib 10.3.35-MariaDB

## Installing\Executing 

What I like to do for this is log in as root or sudo -i.  then copy the script into the /tmp/ and then kick it off.
The first part of the script is for variables. 
A few things to consider first:

### SERVER STUFF
This is basically going to be your external DNS name for your website.  Its what you will enter into the URL
* SERVERNAME=ncloud.Your.Domain

### CERT STUFF
The last line on the Script enables CertBot to create the SSL cert for the site. It is commented out, so make sure you have the External DNS setup properly and your firewall rules setup.  CertBot also needs port 80 and 443.  Please be careful how you setup your firewalls\NAT\Port forwarding

Email for Certbot that will notify when the Cert is expiring. Doesn't have to be real, but recommend
* CERTMAIL=your@email.com
 
### DB STUFF
This is the name of the database that will create for nextcloud
* DBNAME=nextcloud

This is the username that is needed for the nextcloud database. NOTE: This is not a nextcloud user account
* USER=nextclouduser

This is the name of the nextcloud Admin user
* ADMIN=admin

### PASSWORD STUFF
This generates a random password for the root account of mariadb. You can change it if you wish
* date +%s | sha256sum | base64 | head -c 16 > /tmp/.MARIADBPASSWORD

This generates a random password for the nextcloud user account in mariadb. You can change it if you wish
* date +%s | sha256sum | base64 | head -c 16 >> /tmp/.APPPASSWORD

This generates a random password for the Nextcolud admin user account password. You can change it if you
* date +%s | sha256sum | base64 | head -c 16 >> /tmp/.ADMINPASS

### TRUSTED DOMAIN STUFF
If you try to log in and you get a "Trusted Domain error" you will have to add it.  You can do that by editing /var/www/html/nextcloud/config/config.php, you may have to add the domain name or IPs.  

### CLEANING UP
When the script is done running it will remind you that there are passwords and scripts in the /tmp. Keep them there as long as you need them, but do remember to clean house.  If a bad actor popped into you machine, they would have the key to your kingdom.
