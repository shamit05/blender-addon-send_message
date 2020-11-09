## How to Setup Addon
Please note this guide only works on blender 2.8 or newer

First download the main addon file from [here](https://github.com/shamit05/blender-addon-send_message/blob/main/render_send_message_after_render.py)

### Setting up Variables

First, setup all of the variables.

Open the main addon python file that you just downloaded in a text editor and edit the variables on lines 13-16 (fromaddr, frompassword, toaddr, and tempRenderPath)

fromaddr: This is the email address you will be sending the email from. The email will have to be a gmail account and can either be an existing one or you can create a new one. We will go over setting up this email address to actually be able to send the message to another email/phone number in the next section

frompassword: This is the password for the email address you will be sending the email from. This will be stored only locally in the file and sent to google for verification. Again, if you don't feel "safe" saving your password you can setup a new gmail account just for this

toaddr: This is the email you will actually be sending the message and image to. Please check out the sections below if you want to send it to a phone number.

tempRenderPath: When the render is finished it saves a super small sized image to this temporary path so that it can read it and send the image via the email later. This can be located basically almost anywhere on your computer but I like to personally keep it on my SSD to speed up write and read times.

### Setting up Gmail Account

To send the email you need to allow less secure apps. Again if you don't feel secure doing this please create a new gmail account.

To allow this, go to this [link](https://myaccount.google.com/lesssecureapps) and then turn Allow Less Secure Apps to on

### Setting up Addon Requirements

This is the last thing we will have to setup

First locate where blender is (example: C:\Program Files\Blender Foundation\Blender VERSION)

Once inside the folder go to the following path: (BLENDER_VERSION -> python -> bin)

Here you should find a python executable. If so, you located the correct directory.

Next, open up windows powershell as administrator.

Type in the following commands one by one:
```
cd "DIRECTORY WHICH WE LOCATED IN PREVIOUS STEP" # (example: cd "C:\Program Files\Blender Foundation\Blender 2.90\2.90\python\bin")
.\python -m ensurepip --default-pip
.\python -m pip install Pillow
```

That should be all the setup required.

### Actually installing the Addon

Next, go to blender -> edit -> preferences

Afterwards, go to the Add-ons tab and click install Add-on. 

Locate where the main addon file downloaded on your computer and click install the Add-on button.

Lastly, check the button next to the addon to enable it.

### Using the Addon

To use the addon you can go the the search bar and select it. When rendering, instead of pressing F12 or render, do the following steps:

F3 (Search Bar) -> render.send_message -> Click to start rendering

However, for ease of use, you can assign a shortcut to it.

F3 (Search Bar) -> render.send_message -> Right Click -> Assing_Shortcut -> Press a key(s) to assign the shortcut to

Note: I highly recommend assigning the shortcut to CMD F12 as no other shortcut uses it and it will be familiar (F12 is used for rendering)

### Sending a message to your phone number

To send a message to your phone number you can use a mms gateway.

Here is a list of some popular carriers. If you can't find your carrier on here you can try to search it up and find their mms gateway.

To send a text message and picture via email, you must use a MMS to email gateway. Just substitute a 10-digit cell number for ‘number’ for each carrier below:

AT&T: number@mms.att.net

T-Mobile: number@tmomail.net

Verizon: number@vzwpix.com

Sprint: number@pm.sprint.com

XFinity Mobile: number@mypixmessages.com

Virgin Mobile: number@vmpix.com

Tracfone: number@mmst5.tracfone.com

Metro PCS: number@mymetropcs.com

Boost Mobile: number@myboostmobile.com

Cricket: number@mms.cricketwireless.net

Google Fi (Project Fi): number@msg.fi.google.com

U.S. Cellular: number@mms.uscc.net


### Support or Contact

Having trouble with the addon? Try checking the console for errors: 

Window -> Toggle System Console

If you can't solve the error even after checking the system console you can contact me through discord: @shamit0011#0731
