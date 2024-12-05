# GoogleSites-Cloudflare
Google Sites is great. Cloudflare is great. Getting them to work together is a pain. Here's how you do it.


## DNS Entries needed. These IP addresses are Google's servers
#A Records
yourdomain.com.	216.239.32.21
yourdomain.com.	216.239.34.21
yourdomain.com.	216.239.38.21
yourdomain.com.	216.239.36.21

#AAAA Records
yourdomain.com.	2001:4860:4802:38::15
yourdomain.com.	2001:4860:4802:34::15
yourdomain.com.	2001:4860:4802:32::15
yourdomain.com.	2001:4860:4802:36::15

#CNAME Records. Cloudflare's Proxy should be **OFF**. The TTL should be set for **1 hour**.
www.yourdomain.com.	ghs.googlehosted.com.

#TXT Records. Get this site ownership verification text from Google Sites. You'll need to select the DNS txt entry to prove you own the domain.
yourdomain.com.	"google-site-verification=######################################"

## Next, you need a redirect rule. Find this under domain ==> Rules ==> Page Rules. This is #required so the naked domain can be redirected to the "www" domain since that's registered #in the CNAME entry as ghs.googlehosted.com

URL (required) https://yourdomain.com/*

Pick a Setting (required) Forwarding URL
Select status code (required) 301-Permanent Redirect

Enter destination URL (required)
https://www.yourdomain.com/$1

### This infor comes from https://community.cloudflare.com/t/google-sites-dns-settings-in-cloudflare/560618 with some additions from me in order to get the darn thing to work. This information is out there... but it's dispersed.
