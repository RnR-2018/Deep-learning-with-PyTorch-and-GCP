# Optional Step: Graphical User Interface (GUI) on GCP
Nanyan "Rosalie" Zhu and Chen "Rapahel" Liu

## Overview.
This step is absolutely unessential for this course. The purpose of this step is just to build a graphical user interface on GCP, such that you can browse the files and folders, double click to open them, etc. It does not provide additional functionality beyond using the SSH terminal commands, but it might be a little more welcoming for people who are uncomfortable with text-based user interfaces.

There might be other ways to set up a graphical user interface on GCP, but what we introduce here is a comparatively straightforward method to implement. Conceptually you will configure the GCP VM instance as a server, an entity that can serve as a host and welcome connections, and on the other hand you will use your own device (desktop, laptop, etc.) as a client to connect to the server. We will introduce VNC Server-Client pair for this purpose.

## Part 1. On the GCP VM (the Server).
1. On the Google Cloud Platform, navigate to the Virtual Machine section and activate the instance you want to work in. Open the SSH terminal.

2. Upgrade apt-get

        sudo apt-get upgrade
        sudo apt-get update
        sudo apt upgrade
        sudo apt update

3. Install the following packages

        sudo apt-get install gnome-shell gnome task-gnome-desktop autocutsel tightvncserver gnome-core gnome-panel metacity nautilus

    You will probably encounter a pop-up window. Don't panic, it's just asking you to select the language. The installation may take quite a while.

4. Run the VNCserver

        vncserver -geometry 1920x1080 :1

    The "**:1"** specifies the port for the VNC server. It is a simplified term for ":5901". In general, the port number is omitted by 5900, i.e., ":5902" is equivalent to ":2", ":5923" is equivalent to ":23", etc.

    When you run the VNCserver for the first time, you need to design a password as instructed. You will need the password to connect to GCP from your local device.
    
    <img src="/Step03_GUI_setup (optional)/images/vnc_log_file.png" alt="add_new_disk" width="600px" height="200px">

5. Use the path displayed to open the xstartup file. You can choose to use any other text editor besides "nano".

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

    Before modification:
    
    <img src="/Step03_GUI_setup (optional)/images/xstartup_before_modification.png" alt="add_new_disk" width="600px" height="200px">
    
    After modification:
    
    <img src="/Step03_GUI_setup (optional)/images/xstartup_after_modification.png" alt="add_new_disk" width="600px" height="200px">

    **Now you are done with the modifications on the side of the GCP VM (the Server).**


## Part 2. On your local device (the Client).
*We are only roughly familiar with windows and Mac, and you may need to find your own way out there if you are using other operating systems on your own device.*

### If your device uses a Windows OS.
1. **On the local device (NOT THE GCP)** download google cloud software development kit (sdk). Install it as instructed.
        [Download google-cloud-sdk here](https://cloud.google.com/sdk/docs/downloads-versioned-archives)

2. Log in google cloud sdk
    ```
    gcloud auth login
    ```

    A pop-up window on your browser will ask you to log in with your google account.
    
3. Create a SSH tunnel between your local device and GCP.
    ```
    gcloud compute ssh [Instance Name] --project [Project ID] --zone [Zone ID] --ssh-flag "-L 5901:localhost:5901"
    ```

    example:
    ```
    gcloud compute ssh bmen4460-hahaha --project 
    ```
    
    **Instance Name** Whatever name you want to give to the current connection instance.
    
    **Project ID** Click on "My First Project" and check the ID. In 
    <img src="/Step03_GUI_setup (optional)/images/find_project_name.png" alt="GCP_console" width="600px" height="300px">
    
    **Zone ID** The thing under the "Zone" tag.
    <img src="/Step03_GUI_setup (optional)/images/find_zone.png" alt="GCP_console" width="1000px" height="100px">

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
