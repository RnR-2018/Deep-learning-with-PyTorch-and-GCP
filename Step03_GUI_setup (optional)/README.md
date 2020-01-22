# Optional Step: Graphical User Interface on GCP

1. On the Google Cloud Platform, navigate to the Virtual Machine section and activate the instance you want to work in.
2. Upgrade apt-get

        sudo apt-get upgrade
        sudo apt-get update
        sudo apt upgrade
        sudo apt update

3. Install the following packages

        sudo apt-get install gnome-shell gnome task-gnome-desktop autocutsel tightvncserver gnome-core gnome-panel

4. Use the path displayed to open the xstartup file

        sudo nano /home/[username]/.vnc/xstartup

5. Replace the code in the xstartup file with the following:

        #!/bin/sh
        autocutsel -fork
        xrdb $HOME/.Xresources
        xsetroot -solid grey
        export XKL_XMODMAP_DISABLE=1
        export XDG_CURRENT_DESKTOP="GNOME-Flashback:Unity"
        export XDG_MENU_PREFIX="gnome-flashback-"
        unset DBUS_SESSION_BUS_ADDRESS
        gnome-session --session=gnome-flashback-metacity --disable-acceleration-check --debug &

6. Run the Vncserver

        vncserver -geometry 1920x1080 :1

    The "**:1"** specifies the port. It is a simplified term for ":5901".

    Design a password for viewing the VNC


7. **On the PC (NOT THE GCP)** create a SSH tunnel between the PC and GCP.

        gcloud compute ssh [Instance Name] --project [Project ID] --zone [Zone ID] --ssh-flag "-L 5901:localhost:5901"

    For Windows PC, I would need to login my Google Cloud SDK first.

        gcloud auth login [Account]

8. Open VNCViewer and use the server "localhost:5901".
9. Kill the VNC server when finished

        vncserver -kill :1
        
        
        
        
- **if you got grey desktop after login use vnc client, try this :**
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
