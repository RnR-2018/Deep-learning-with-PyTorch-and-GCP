# Optional Step: Graphical User Interface on GCP
Nanyan "Rosalie" Zhu and Chen "Rapahel" Liu

## Step-by-step instructions.
### On the GCP VM (the web browser you open).
1. On the Google Cloud Platform, navigate to the Virtual Machine section and activate the instance you want to work in.
2. Upgrade apt-get

        sudo apt-get upgrade
        sudo apt-get update
        sudo apt upgrade
        sudo apt update

3. Install the following packages

        sudo apt-get install gnome-shell gnome task-gnome-desktop autocutsel tightvncserver gnome-core gnome-panel
        

4. Run the Vncserver

        vncserver -geometry 1920x1080 :1

    The "**:1"** specifies the port. It is a simplified term for ":5901".

    Design a password for viewing the VNC
    
5. Use the path displayed to open the xstartup file

        sudo nano /home/[username]/.vnc/xstartup

6. Replace the code in the xstartup file with the following:

        #!/bin/sh
        autocutsel -fork
        xrdb $HOME/.Xresources
        xsetroot -solid grey
        export XKL_XMODMAP_DISABLE=1
        export XDG_CURRENT_DESKTOP="GNOME-Flashback:Unity"
        export XDG_MENU_PREFIX="gnome-flashback-"
        unset DBUS_SESSION_BUS_ADDRESS
        gnome-session --session=gnome-flashback-metacity --disable-acceleration-check --debug &

### On your local PC (not the web browser!)
7. **On the PC (NOT THE GCP)** download google cloud software development kit (sdk).
        [Download google-cloud-sdk here](https://cloud.google.com/sdk/docs/downloads-versioned-archives)

8. Create a SSH tunnel between the PC and GCP.

        gcloud compute ssh [Instance Name] --project [Project ID] --zone [Zone ID] --ssh-flag "-L 5901:localhost:5901"

    **Instance Name** Whatever name you want to give to the current connection instance.
    
    **Project ID** Click on "My First Project" and check the ID.
    <>
    
    **Zone ID** The thing under the "Zone" tag.
    <>

9. For Windows PC, you would need to log in your Google Cloud SDK first.

        gcloud auth login [Account]

10. Open VNCViewer and use the server "localhost:5901".
11. Kill the VNC server when finished

        vncserver -kill :1
        
        
## For Mac

1. Go to Google Cloud Platform. Start the VM instance.
2. Open **Terminal #1**. This terminal will be your **GCP instance**.

    **In Terminal #1:**

        gcloud auth login
        gcloud compute ssh --project gentle-nuance-238411 bmen4460

    Once the terminal brings up the GCP instance interface, open the VNC Server.

        vncserver -geometry 1920x1080 :1

3. Open **Terminal #2**. This terminal will be your local machine that connects to the GCP instance.

    **In Terminal #2:**

        gcloud auth login
        gcloud compute ssh bmen4460 --project gentle-nuance-238411 --zone us-central1-a --ssh-flag "-L 5901:localhost:5901"

    This will bring up a pop-up screen which also shows the GCP instance interface. Do not need to do anything with that.

4. Open **Terminal #3**. This terminal will be your VNC Viewer command line.

    **In Terminal #3:**

        open vnc://localhost:5901

5. Remember to shut down the VNC Server after you are finished. **In Terminal #1**:

        vncserver -kill :1
        
        
        
        
        
        
## **if you got grey desktop after login use vnc client, try this :**
  ```
  nano ~/.vnc/xstartup
  ```
  add this code :
  ```
  gnome-panel &
  gnome-settings-daemon &
  metacity &
  nautilus &
  after x-window-manager &
  ```
