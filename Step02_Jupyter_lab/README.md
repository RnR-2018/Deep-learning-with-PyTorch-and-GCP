# Jupyter Lab on GCP.
Nanyan "Rosalie" Zhu and Chen "Raphael" Liu

## Latest update
If you used the "Compute Engine" > "Marketplace" > "Deep Learning VM" pre-packaged method (introduced in the previous chapter) to generate your VM, you should have anaconda and jupyter installed already. In this case, you can skip the installation steps and only look at how to utilize them.

## Overview
This chapter has two major sections.
* Section 1. Configure GCP to accomodate jupyter lab.
* Section 2. Use jupyter lab on GCP.

## Section 1. Configure GCP to accomodate jupyter lab.

<details>
<summary><strong>Step 1. Configure a static external IP address.</strong></summary>
<br>

*To be honest this is not essential, but will make your future life easier. If the IP address is not set to be static, it might change every now and then, and you might have to look up the new IP address each time you need it.*

On GCP, go to "VPC network" > "External IP addresses".

<img src="/Step02_Jupyter_lab/Images/external_IP_address.png" alt="add_new_disk" width="200px" height="350px">

Change the IP address from "Ephemeral" to "Static". Give it a name you like.

<img src="/Step02_Jupyter_lab/Images/configure_static_address.png" alt="add_new_disk" width="300px" height="100px"> <img src="/Step02_Jupyter_lab/Images/configure_static_address_continued.png" alt="add_new_disk" width="300px" height="150px">

</details>

<details>
<summary><strong>Step 2. (Important) Update firewall rules.</strong></summary>
<br>

1. On GCP, go to "VPC network" > "Firewall rules".

<img src="/Step02_Jupyter_lab/Images/firewall_rules.png" alt="add_new_disk" width="500px" height="150px">

2. Set up a new firewall rule as shown below.
*To be frank, you can choose another port number, but we would recommend 4460 since that's the same as your course ID. In this way you won't need to keep track of too many numbers.*

<img src="/Step02_Jupyter_lab/Images/configure_firewall_rules.png" alt="add_new_disk" width="300px" height="500px"> <img src="/Step02_Jupyter_lab/Images/configure_firewall_rules_continued.png" alt="add_new_disk" width="300px" height="500px">

</details>

<details>
<summary><strong>Checkpoint</strong></summary>
<br>

At this stage, we want you to keep track of two things.

1) **Your external IP address.** Can be found in GCP > "Compute Engine" > "VM instances".
(In our case, 35.203.66.22)

<img src="/Step02_Jupyter_lab/Images/your_external_IP_address.png" alt="add_new_disk" width="600px" height="50px">

2) **Your port number that allows HTTP/HTTPS incoming traffic.** Can be found in GCP > "VPC network" > "Firewall rules".
(In our case, port 4460)

<img src="/Step02_Jupyter_lab/Images/your_port_allowed.png" alt="add_new_disk" width="600px" height="50px">

</details>

</details>

## Section 2. Use jupyter lab on GCP.

<details>
<summary><strong>Step 1. Initiate jupyter lab.</strong></summary>
<br>

1. Activate anaconda environment.

Go to GCP, start your VM instance, open SSH terminal. If unfamiliar, refer to chapter "Step00_set_up_GCP".

Activate the environment you need to work with
```
conda activate [myenv]
```

Example:
```
conda activate BMEN4460
```

After doing this, the "(base)" in the command line will become "([myenv])".
    
<img src="/Step02_Jupyter_lab/Images/activate_environment.png" alt="add_new_disk" width="600px" height="50px">


2. Make sure that you have installed jupyter lab.

*If it is already installed (as it should if you followed through chapter "Step01_manage_anaconda_on_GCP"), you can skip this. If not, you can use following command to install one of them. We personally prefer jupyter lab.*
```
conda install jupyter jupyterlab -c anaconda
```


3. Install a jupyter kernel in the respective environment.

```
python -m ipykernel install --user --name [myenv] --display-name "[Python (myenv)]"
```

Example:
```
python -m ipykernel install --user --name BMEN4460 --display-name "Python3.7 BMEN4460"
```    
    
Now the jupyter kernel is distinctively pointing to the python in the corresponding environment.

</details>


<details>
<summary><strong>Step 2. (Important) Create and modify a jupyter configuration file.</strong></summary>
<br>

*For this step, credit goes to [https://tudip.com/blog-post/run-jupyter-notebook-on-google-cloud-platform/](https://tudip.com/blog-post/run-jupyter-notebook-on-google-cloud-platform/). We were unaware of this before.*


1. Create the config.

```
jupyter lab --generate-config
```

A configuration file (somehow named after jupyter notebook instead of jupyter lab) will be created.

<img src="/Step02_Jupyter_lab/Images/create_jupyter_config.png" width="800px" height="50px">


2. Modify the config.

The next step is comparatively challenging, especially if you have no prior experience with text editors. You will need to access the config file using either the "nano" editor (as what we will use for demonstration) or any other editor you prefer.

```
nano /home/[username]/.jupyter/jupyter_notebook_config.py
```

and this will open the config file with the "nano" editor interface. To be frank it is quite intimidating at the first glance.
    
<img src="/Step02_Jupyter_lab/Images/jupyter_config_file.png" width="600px" height="600px">

You need to add the following lines to pretty much anywhere that is not commented out within the config file.

```
c = get_config()
c.NotebookApp.ip = '*'
c.NotebookApp.open_browser = False
c.NotebookApp.port = 4460
```

*Remember to replace the port "4460" with whatever you set up as your port number that allow HTTP/HTTPS traffic.*

The modified config file looks like this. We are so lazy and arrogant that we add the new configuration commands at the very top of the file. Once done, use Ctrl+X to exit and type "Y" to save changes, and follow up with an "Return/Enter" to confirm overwriting the existing config file.

<img src="/Step02_Jupyter_lab/Images/jupyter_config_file_modified.png" width="400px" height="300px">

**Now you are done with the difficult part.**


</details>

<details>
<summary><strong>Step 3. Open a Jupyter Lab.</strong></summary>
<br>

The next step is to open jupyter lab. Remember you should have your environment activated.

```
jupyter lab
```

The following lines shall show up in the SSH terminal.
    
<img src="/Step02_Jupyter_lab/Images/open_jupyter_lab.png" width="800px" height="200px">
    
Do you see that website url highlighted in red? You should notice the number following the colon is the port number allowing traffic that you set up earlier in this tutorial. Now copy the entire url, but replace the string (in our case "bmen4460") ahead of the colon with your external IP address (in our case 35.203.66.22). What you will get is something like:

```
http://35.203.66.22:4460/?token=a4a65a7cd90703e893dda91719d614ef68b2a071fe88d1af
```

Copy and paste that url to a browser on your own PC/laptop/etc. That will open up a jupyter lab page on your own device.
    
<img src="/Step02_Jupyter_lab/Images/opened_jupyter_lab.png" width="600px" height="400px">

</details>

### A sample Jupyter Lab notebook that you can try out.
[Simple cell segmentation with a single layered perceptron](https://github.com/RnR-2018/BMEN4460-NB1-simple_cell_segmentation_with_a_single_layered_perceptron). Instructions on how to download the repository (notebook along with data) is given.

## End of this chapter: Step02_Jupyter_lab.
