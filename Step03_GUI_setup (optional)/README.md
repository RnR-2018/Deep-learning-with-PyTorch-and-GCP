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
        
        gnome-panel &
        gnome-settings-daemon &
        metacity &
        nautilus &
        after x-window-manager &

    Before modification:
    
    <img src="/Step03_GUI_setup (optional)/images/xstartup_before_modification.png" alt="add_new_disk" width="600px" height="200px">
    
    After modification:
    
    <img src="/Step03_GUI_setup (optional)/images/xstartup_after_modification.png" alt="add_new_disk" width="600px" height="300px">

    Remember to use "Ctrl+X" followed by typing "Y" followed by pressing "Return/Enter" to save your changes.

7. (This step is just to refresh the GCP VM and update the settings.) Kill the VNC server session. Close the GCP VM SSH Terminal, re-open the SSH Terminal, and re-start the vncserver.

    The code to kill the VNC server session is:
    ```
    vncserver -kill :1
    ```

    For future uses, you don't need to start VNC server, kill it, exit SSH, open SSH, start VNC server. This is only for the first time you set up the xstartup file. In the future, you only need to start VNC server once and keep it running throughout the duration you want to connect from your local device to GCP VM, and only kill it when you are finished with the connection.
    
8. Log in Google cloud on the GCP VM.
    ```
    gcloud auth login
    ```

9. Configure Google cloud on the GCP VM. Follow the instructions and set up a passphrase.
    ```
    gcloud compute ssh [Instance Name] --project [Project ID]
    ```    
    
    Example:
    ```
    gcloud compute ssh bmen4460 --project gentle-nuance-238411
    ```
    
    - **Instance Name** The virtual machine instance name. (In our case it is "bmen4460")
    <img src="/Step03_GUI_setup (optional)/images/find_instance_name_and_zone.png" alt="GCP_console" width="1000px" height="80px">
    
    - **Project ID** Click on "My First Project" and check the ID. (In our case it is "gentle-nuance-238411")
    <img src="/Step03_GUI_setup (optional)/images/find_project_name.png" alt="GCP_console" width="600px" height="200px"
    
    **Now you are done with the modifications on the side of the GCP VM (the Server).**


## Part 2. On your local device (the Client). (While the VNC server is running.)
*We are only roughly familiar with windows and Mac, and you may need to find your own way out there if you are using other operating systems on your own device.*

<details>
<summary><header>If your device uses a Windows OS.</header></summary>
<br>

1. **On the local device (NOT THE GCP)** download google cloud software development kit (sdk). Install it as instructed.
        [Download google-cloud-sdk here](https://cloud.google.com/sdk/docs/downloads-versioned-archives)

2. Log in google cloud SDK.
    ```
    gcloud auth login
    ```

    A pop-up window on your browser will ask you to log in with your google account.
    
3. Initialize the google cloud configuration.
    ```
    gcloud init
    ```

   Follow the instructions and build your configurations. Faithfully enter the account email, project ID, etc.

4. Create a SSH tunnel between your local device and GCP.
    ```
    gcloud compute ssh [Username]@[Instance Name] --project [Project ID] --zone [Zone ID] --ssh-flag "-L [Port Number]"
    ```

    Example:
    ```
    gcloud compute ssh msnanyanzhu@bmen4460 --project gentle-nuance-238411 --zone northamerica-northeast1-a --ssh-flag "-L 5901:localhost:5901"
    ```
    
    *Note: In fact, if you use gcloud init and enter the fields correctly, the entries --project and --zone are unnecessary.*
    
    - **Instance Name** The virtual machine instance name. (In our case it is "bmen4460")
    <img src="/Step03_GUI_setup (optional)/images/find_instance_name_and_zone.png" alt="GCP_console" width="1000px" height="80px">
    
    - **Project ID** Click on "My First Project" and check the ID. (In our case it is "gentle-nuance-238411")
    <img src="/Step03_GUI_setup (optional)/images/find_project_name.png" alt="GCP_console" width="600px" height="200px">
    
    - **Zone ID** The thing under the "Zone" tag. (In our case it is "us-central1-a")
    <img src="/Step03_GUI_setup (optional)/images/find_instance_name_and_zone.png" alt="GCP_console" width="1000px" height="80px">
    
    - **Port Number** Remember to change the two "5901" to whatever VNC port number you originally set up in part 1. If you used port 5902, for example, you should type **--ssh-flag "-L 5902:localhost:5902".** Also, please use the full number, instead of the abbreviation (i.e., use 5932 instead of 32, etc.).

5. Now there should be a pop-up terminal on your own Windows device, stating that you have connected to the GCP server. This terminal is equivalent to the SSH terminal on the GCP VM. Once you have this pop-up terminal running, you can use VNC viewer to connect to your GCP VM (graphically instead of through a text-based interface).

6. Download and install VNC viewer. Either [TightVNC](https://www.tightvnc.com/) or [RealVNC](https://www.realvnc.com/en/) shall (theoretically) work.

7. Open VNCViewer and type in "localhost:5901" in the "Enter a VNC Server address or search" field. Press "Return/Enter" to connect. Use the password you set up when initializing the server. Now you should see your GCP VM through a graphical interface.

8. Kill the VNC server session (**on the GCP VM Server**) when you are done.
    ```
    vncserver -kill :1
    ```

</details>


### If your device uses a MAC OS.
1. **On the local device (NOT THE GCP)** download google cloud software development kit (sdk). Install it as instructed.
        [Download google-cloud-sdk here](https://cloud.google.com/sdk/docs/downloads-versioned-archives)

2. Log in google cloud SDK. Open **Terminal #1 on you local device**. This terminal will be your local machine that connects to the GCP instance.

    **In Terminal #1:**
    ```
    gcloud auth login
    ```

    A pop-up window on your browser will ask you to log in with your google account.
    
3. Initialize the google cloud configuration.

    **In Terminal #1:**
    ```
    gcloud init
    ```

   Follow the instructions and build your configurations. Faithfully enter the account email, project ID, etc.

4. Create a SSH tunnel between your local device and GCP.

    **In Terminal #1:**    
    ```
    gcloud compute ssh [Username]@[Instance Name] --project [Project ID] --zone [Zone ID] --ssh-flag "-L [Port Number]"
    ```

    Example:
    ```
    gcloud compute ssh msnanyanzhu@bmen4460 --project gentle-nuance-238411 --zone northamerica-northeast1-a --ssh-flag "-L 5901:localhost:5901"
    ```

    *Note: In fact, if you use gcloud init and enter the fields correctly, the entries --project and --zone are unnecessary.*
    
    - **Instance Name** The virtual machine instance name. (In our case it is "bmen4460")
    <img src="/Step03_GUI_setup (optional)/images/find_instance_name_and_zone.png" alt="GCP_console" width="1000px" height="80px">
    
    - **Project ID** Click on "My First Project" and check the ID. (In our case it is "gentle-nuance-238411")
    <img src="/Step03_GUI_setup (optional)/images/find_project_name.png" alt="GCP_console" width="600px" height="200px">
    
    - **Zone ID** The thing under the "Zone" tag. (In our case it is "us-central1-a")
    <img src="/Step03_GUI_setup (optional)/images/find_instance_name_and_zone.png" alt="GCP_console" width="1000px" height="80px">
    
    - **Port Number** Remember to change the two "5901" to whatever VNC port number you originally set up in part 1. If you used port 5902, for example, you should type **--ssh-flag "-L 5902:localhost:5902".** Also, please use the full number, instead of the abbreviation (i.e., use 5932 instead of 32, etc.).

5. Now there should be a pop-up terminal on your own Windows device, stating that you have connected to the GCP server. This terminal is equivalent to the SSH terminal on the GCP VM. Once you have this pop-up terminal running, you can use VNC viewer to connect to your GCP VM (graphically instead of through a text-based interface).

6. Open **Terminal #2 on your local device**. This terminal will be your VNC Viewer command line. Mac is amazing in that it has, on its own, the functionality provided by the VNC viewer software that has to be downloaded externally for Windows.

    **In Terminal #2:**
    ```
    open vnc://localhost:5901
    ```

    Use the password you set up when initializing the server. Now you should see your GCP VM through a graphical interface.
    
7. Kill the VNC server session (**on the GCP VM Server**) when you are done.
    ```
    vncserver -kill :1
    ```

### For both Windows and Mac users.
This is what the graphical user interface on GCP VM looks like.
<img src="/Step03_GUI_setup (optional)/images/GUI_looklike.png" alt="GCP_console" width="700px" height="500px">

## End of this chapter: Step03_GUI_setup.
