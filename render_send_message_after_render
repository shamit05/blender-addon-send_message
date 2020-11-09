bl_info = {
    "name": "Send Message After Render",
    "author": "Shamit Surana",
    "version": (0, 0, 1),
    "blender": (2, 80, 0),
    "location": " Search Bar > Create Shortcut > Cmd F12",
    "description": "Sends you a message when done with render",
    "warning": "Make sure to setup variables on lines 13-16 in python file",
    "doc_url": "",
    "category": "Render",
}

fromaddr = "" # Setup all of the variables and enter info inside of quotes
frompassword = "" 
toaddr = ""
tempRenderPath = ""


allVars = [fromaddr, frompassword, toaddr, tempRenderPath]
allVarsNames = ["fromaddr", "frompassword", "toaddr", "tempRenderPath"]
unsetupVariables = []
for a in range(len(allVars)):
	if allVars[a] == "":
		unsetupVariables.append(a)

warning = ""
if unsetupVariables:
	warning =  "WARNING: setup variable(s) "
	for i in range(len(unsetupVariables)):
		warning = warning + allVarsNames[unsetupVariables[i]]
		if len(unsetupVariables) - i > 1:
			warning = warning + ", "
		else:
			warning = warning + " "
	warning = warning + "in python file"

if warning != "":
	print(warning)

import bpy
from datetime import datetime
import smtplib
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from email.mime.base import MIMEBase
from email import encoders
import os
from PIL import Image


def my_handler(scene):
    # datetime object containing current date and time
    now = datetime.now()
    # dd/mm/YY H:M:S
    dt_string = now.strftime("%H:%M:%S on %d/%m/%Y")
    body = str("\nRender complete at " + dt_string)
    print(str(body))
    currentX = bpy.context.scene.render.resolution_x
    currentY = bpy.context.scene.render.resolution_y
    newX = currentX
    newY = currentY
    while newX > 2000:
        newX = newX / 2
        newY = newY / 2

    size = int(newX), int(newY)
    print("Opening image at " + str(datetime.now()))
    im = Image.open(tempRenderPath)
    print("Resizing image at " + str(datetime.now()))
    im_resized = im.resize(size, Image.ANTIALIAS)
    print("Saving image at " + str(datetime.now()))
    im_resized.save(tempRenderPath, optimize=True, quality=85)
    print("Done at " + str(datetime.now()))

    msg = MIMEMultipart()

    msg['From'] = fromaddr
    msg['To'] = toaddr
    msg['Subject'] = "Render Complete"

    msg.attach(MIMEText(body, 'plain'))

    filename = "Render"
    attachment = open(tempRenderPath, "rb")

    part = MIMEBase('application', 'octet-stream')
    part.set_payload((attachment).read())
    encoders.encode_base64(part)
    part.add_header('Content-Disposition', "attachment; filename= %s" % filename)

    msg.attach(part)

    server = smtplib.SMTP('smtp.gmail.com', 587)
    server.starttls()
    server.login(fromaddr, frompassword)
    text = msg.as_string()
    print("Sending Alert")
    server.sendmail(fromaddr, toaddr, text)
    server.quit()
    bpy.app.handlers.render_post.clear()
    bpy.app.handlers.render_complete.clear()


class StartRender(bpy.types.Operator):
    """Object Cursor Array"""
    bl_idname = "render.send_message"
    bl_label = "Alert after Render Test"
    bl_options = {'REGISTER'}

    def execute(self, context):
        try:
            os.remove(tempRenderPath)
        except OSError:
            print("Error: Temp render doesn't exist for deleting")
        if warning != "":
            print(warning)
        print("\nRendering with Alert")
        bpy.context.scene.render.filepath = tempRenderPath
        bpy.ops.render.render("INVOKE_DEFAULT", write_still=True)
        bpy.app.handlers.render_complete.append(my_handler)
        return {'FINISHED'}


def register():
    bpy.app.handlers.render_post.clear()
    bpy.app.handlers.render_complete.clear()
    bpy.utils.register_class(StartRender)


def unregister():
    if my_handler in bpy.app.handlers.render_post:
        bpy.app.handlers.render_complete.remove(my_handler)
    bpy.utils.unregister_class(StartRender)


if __name__ == "__main__":
    register()
