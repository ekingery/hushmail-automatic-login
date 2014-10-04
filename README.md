hushmail-automatic-login
========================

Automates a login to hushmail via curl
--------------------------------------

### Why?
[Hushmail](https://www.hushmail.com/) is an anonymous encrypted email service. Their privacy track record is a little suspect, but they do encrypt the stored email using PGP. The free tier forces you to login every three weeks to keep your account active. That seems hard. You know what's not hard? Having a machine login for you. That is lazy. And awesome.

### How? 
A little linux foo is all you need. The hushmail-autologin bash script will make a request to the hushmail login URL to capture a CSRF token. It then uses that token and your credentials to POST to the hushmail auth page using curl. I am seeing some intermittent failures involving complaints about cookies or some arcane curl error. I recommend running it daily to ensure successful logins within a 3 week period. 

The script checks the return value to make sure the login was successful. If not, it exits non-zero and dumps the error message to stdout. If you setup the MAILTO in your cron job, you will get an email whenever the login fails.

### Example Cron Job

	MAILTO=your-email@regular-provider.com
	# login to hushmail every day at 12:38am
	38 0 * * * ~/bin/hushmail-autologin
