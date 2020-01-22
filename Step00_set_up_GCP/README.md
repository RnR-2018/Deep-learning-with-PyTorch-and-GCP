# Tutorial to set up the Google Cloud Platform
Nanyan "Rosalie" Zhu and Chen "Raphael" Liu

## Overview.
To the best of our knowledge, new users to the google cloud platform are granted $300 worth of computational resources for free. Students affiliated to academic institution may ask their professors whether or not the courses they are enrolled in cooperate with GCP. If so, it is likely that even more GPU-hours can be available.

## Step-by-step instructions.

1. Go to [https://cloud.google.com](https://cloud.google.com).

2. You will see an interface similar to this (though it might change from time to time). Click on the "Go to console" button and let it take you to the GCP console.
![GCP_homepage](/Step00_set_up_GCP/Images/GCP_homepage.PNG)

3. You should see an interface like this, assuming you have logged in your google account.
<img src="/Step00_set_up_GCP/Images/GCP_console.png" alt="GCP_console" width="600px" height="300px">

4. Navigate to and click on the "VM instances" button. Just FYI, "VM" stands for "virtual machine".
<img src="/Step00_set_up_GCP/Images/VM_instances_button.png" alt="VM_instances_button" width="300px" height="400px">

5. Wait for the compute engine to get ready. Once ready, click on "Create" to create a new VM instance.
<img src="/Step00_set_up_GCP/Images/VM_instance.png" alt="VM_instance" width="800px" height="300px">

6. Configure the VM according to your needs. Most configurations can be modified after the intialization.
- The region and zone probably doesn't matter.
- Please select the computational resources (number of CPUs and amount of memory) according to your needs. In this case we selected 4 CPUs and 26 GB memory. You might want larger memory depending on your project.
- Also note that on the upper right corner there is an estimation of the monthly cost based on your current configuration. That gives you a rough idea on how you want to manage your budget.
- For students enrolled in the BMEN4460 instructed by Dr. Andrew Laine and Dr. Jia Guo, you are strongly suggested to select the "Debian GNU/Linux 9 (stretch)" for the Boot disk.
- In the "firewall" section (not included in the following screenshot), you probably want to check "allow HTTP traffic" and "allow HTTPS traffic" in case you need network connection to your VM.
- You don't need to modify anything not mentioned here.
<img src="/Step00_set_up_GCP/Images/VM_configuration.png" alt="VM_configuration" width="800px" height="600px">

7. You may need to create an additional big disk to store you data in it. Click "add new disk" botton on the bottom left and create your new disk.
<img src="/Step00_set_up_GCP/Images/add_new_disk.png" alt="add_new_disk" width="400px" height="450px">

8. Click "create" on the very bottom of the page once you are confident in the selections.
- **The VM is automatically started now. You need to manually stop it if you don't need it right away.**
- **Whenever the VM is in the "start" status you are charged for the computational resource. We have a friend being charged $400+ because she forgot to hit "stop" and left the VM running for several months after a computer science course. So please "stop" it when you are not using it.**
- In most cases, you only need to use the "start" and "stop" button. If you click "reset" you will most likely lose any data you put on the VM. If you are done with the course and really no longer what this VM you can "delete" it as you wish.
<img src="/Step00_set_up_GCP/Images/start_VM.png" alt="VM_configuration" width="800px" height="300px">

9. After you "start" the instance, you may open the ssh terminal by clicking the following button. It usually takes half a minute or so before you are brought to the next window.
<img src="/Step00_set_up_GCP/Images/VM_SSH_open.png" alt="VM_configuration" width="800px" height="200px">

10. The GCP VM SSH terminal looks like this. You can pretty much use any Linux command line code here.
<img src="/Step00_set_up_GCP/Images/VM_SSH_terminal.png" alt="VM_configuration" width="800px" height="200px">

11. Finally, you need to mount the new big disk you created in your VM. you can follow the instruction [here](https://www.cloudbooklet.com/attach-and-mount-disks-to-vm-instance-in-google-cloud/).</br>
**NOTE:**  In our case, we use `/demo-mount` as our mount point.



## End of this chapter: step00_set_up_GCP.
