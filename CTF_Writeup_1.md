Wordpress 5.8.1

WooCommerce plugin 5.7.1
Booster for WoocCommerce plugin 5.4.3
Macumbas 5 ?

admin (seems to not be activated)
Orval_Sanford 

CVE-2021-34646 will allow us to to login as an admin without the necessary credentials

Running the exploit found on https://www.exploit-db.com/exploits/50299 we generate a link that sucessfully allows us to bypass credentials and get logged in as admin.
From there we go to a protected area with a private post that contains the flag, allowing us to complete our first CTF