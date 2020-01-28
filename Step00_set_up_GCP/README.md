# Tutorial to set up the Google Cloud Platform
Nanyan "Rosalie" Zhu and Chen "Raphael" Liu

## Overview.
To the best of our knowledge, new users to the google cloud platform are granted $300 worth of computational resources for free. Students affiliated to academic institution may ask their professors whether or not the courses they are enrolled in cooperate with GCP. If so, it is likely that even more GPU-hours can be available.

## Step-by-step instructions.

<details>
<summary>1. Go to Google Cloud > GCP console.</summary>
<br>

Go to [https://cloud.google.com](https://cloud.google.com).

You will see an interface similar to this (though it might change from time to time). Click on the "Go to console" button and let it take you to the GCP console.
![GCP_homepage](/Step00_set_up_GCP/Images/GCP_homepage.PNG)

</details>

<details>
<summary>2. GCP console interface.</summary>
<br>

You should see an interface like this, assuming you have logged in your google account.
<img src="/Step00_set_up_GCP/Images/GCP_console.png" alt="GCP_console" width="600px" height="300px">

</details>

<details>
<summary>3. VM instances.</summary>
<br>

Navigate to and click on the "Compute Engine" > "VM instances" button. Just FYI, "VM" stands for "virtual machine".
<img src="/Step00_set_up_GCP/Images/VM_instances_button.png" alt="VM_instances_button" width="300px" height="400px">

</details>

<details>
<summary>4. Create a VM instance.</summary>
<br>

Wait for the compute engine to get ready. Once ready, click on "Create" to create a new VM instance.
<img src="/Step00_set_up_GCP/Images/VM_instance.png" alt="VM_instance" width="800px" height="300px">

</details>

<details>
<summary>5. Configure the VM instance.</summary>
<br>

Configure the VM according to your needs. Most configurations can be modified after the intialization.
- The region and zone probably doesn't matter.
- Please select the computational resources (number of CPUs and amount of memory) according to your needs. In this case we selected 4 CPUs and 26 GB memory. You might want larger memory depending on your project.
- Also note that on the upper right corner there is an estimation of the monthly cost based on your current configuration. That gives you a rough idea on how you want to manage your budget.
- For students enrolled in the BMEN4460 instructed by Dr. Andrew Laine and Dr. Jia Guo, you are strongly suggested to select the "Debian GNU/Linux 9 (stretch)" for the Boot disk.
- Don't try to add GPUs yet, there will be a future section on how to do that.
- In the "firewall" section (not included in the following screenshot), you probably want to check "allow HTTP traffic" and "allow HTTPS traffic" in case you need network connection to your VM.
- At last, you may need a larger disk than the default setup to store more data. (In fact, the default setup cannot even contain anaconda that we will download soon.) In the "boot disk" section, click on "change", and make the disk as large as you wish. As our habit, we typically use something like 100 GB.
<img src="/Step00_set_up_GCP/Images/VM_configuration.png" alt="VM_configuration" width="800px" height="600px">

<img src="/Step00_set_up_GCP/Images/make_disk_larger.png" alt="add_new_disk" width="400px" height="300px">

Click "create" on the very bottom of the page once you are confident in the selections.

</details>

<details>
<summary>6. How to start/stop the VM instance, <strong>and friendly warnings</strong>.</summary>
<br>

- **The VM is automatically started now. You need to manually stop it if you don't need it right away.**
- **Whenever the VM is in the "start" status you are charged for the computational resource. We have a friend being charged $400+ because she forgot to hit "stop" and left the VM running for several months after a computer science course. So please "stop" it when you are not using it.**
- In most cases, you only need to use the "start" and "stop" button. If you click "reset" you will most likely lose any data you put on the VM. If you are done with the course and really no longer what this VM you can "delete" it as you wish.
<img src="/Step00_set_up_GCP/Images/start_VM.png" alt="VM_configuration" width="800px" height="300px">

</details>

<details>
<summary>7. Open VM SSH Terminal.</summary>
<br>

After you "start" the instance, you may open the SSH Terminal by clicking the following button. It usually takes half a minute or so before you are brought to the next window.
<img src="/Step00_set_up_GCP/Images/VM_SSH_open.png" alt="VM_configuration" width="800px" height="200px">

</details>

<details>
<summary>8. VM SSH Terminal.</summary>
<br>

The GCP VM SSH terminal looks like this. You can pretty much use any Linux command line code here.
<img src="/Step00_set_up_GCP/Images/VM_SSH_terminal.png" alt="VM_configuration" width="800px" height="200px">

</details>

<details>
<summary>9. Transfer files to GCP VM through Cloud Storage.</summary>
<br>

You can choose a way to transfer your files to GCP VM from [here](https://cloud.google.com/compute/docs/instances/transfer-files). Note that you will be transferring from/to your local device to/from a Linux VM instance.

The recommended way is to transfer file to the GCP VM over the Cloud Storage bucket. Note that the Cloud Storage bucket allow for unlimited memory (probably?) as long as you have an GCP account. You will not be charged over the duration you transfer files from your local device to Cloud Storage bucket; you will only be charged when you transfer from the Cloud Storage bucket to the GCP VM.

The following instructions are copied from [Cloud Storage official website](https://cloud.google.com/compute/docs/instances/transfer-files).
  1. Create a new Cloud Storage bucket or identify an existing bucket that you want to use to transfer files.
  2. From your workstation, upload files to the bucket.
  3. Connect to your instance over SSH or RDP:
  - Connect to a Linux instance over SSH.
  - Connect to a Windows instance over RDP.
  4. On your instance, download files from the bucket.

</details>

## End of this chapter: step00_set_up_GCP.
