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

If you are a new user, this will bring you to a page where Google asks you to log in. **For students in BMEN4460, please remember to log out of all non-Columbia google accounts before logging in with you Columbia account. Otherwise it will be very likely for you to set up a personal non-Columbia GCP account by mistake!** The log in process is quite straightforward, and please mind to not check the "auto-payment" (or something like that) option. You should receive a $300 computational resources for free as a new user, plus the $50 additional coupon provided by Dr. Andrew Laine if you are in BMEN4460. **Before you redeem your coupons, please also remember to sign out all non-Columbia google accounts!**

</details>

<details>
<summary>2. GCP console interface.</summary>
<br>

You should see an interface like this, assuming you have logged in your google account.
<img src="/Step00_set_up_GCP/Images/GCP_console.png" width="600px" height="300px">

</details>

<details>
<summary>3. VM instances.</summary>
<br>

Navigate to and click on the "Compute Engine" > "VM instances" button. Just FYI, "VM" stands for "virtual machine". **Don't create a VM yet!** You could potentially create a VM in this webpage (and the instructions is included in the misc section), but there is a easier way to do this which we are introducing here.

<img src="/Step00_set_up_GCP/Images/VM_instances_button.png" width="300px" height="400px">

</details>

<details>
<summary>4. Create a VM instance (easy, one-click deal).</summary>
<br>

Go to 


</details>

<details>
<summary>4. Create a VM instance.</summary>
<br>

Wait for the compute engine to get ready. Once ready, click on "Create" to create a new VM instance.
<img src="/Step00_set_up_GCP/Images/VM_instance.png" width="800px" height="300px">

</details>

</details>

## End of this chapter: step00_set_up_GCP.

</br>
</br>
</br>

### Misc: An alternative way to create a VM instance.
We believe this is an old-fashioned way and is less one-click-deal.

<details>
<summary>4. Create a VM instance.</summary>
<br>

Wait for the compute engine to get ready. Once ready, click on "Create" to create a new VM instance.
<img src="/Step00_set_up_GCP/Images/VM_instance.png" width="800px" height="300px">

</details>

<details>
<summary>5. Configure the VM instance.</summary>
<br>

Configure the VM according to your needs. Most configurations can be modified after the intialization.
**You will probably need a VM without GPU and a VM with GPU. The following settings are for the VM without GPU.**

- The region and zone probably doesn't matter.
- Please select the computational resources (number of CPUs and amount of memory) according to your needs. In this case we selected 4 CPUs and 26 GB memory. You might want larger memory depending on your project.
- Also note that on the upper right corner there is an estimation of the monthly cost based on your current configuration. That gives you a rough idea on how you want to manage your budget.
- For students enrolled in the BMEN4460 instructed by Dr. Andrew Laine and Dr. Jia Guo, you are strongly suggested to select the "Debian GNU/Linux 9 (stretch)" for the Boot disk.
- Don't try to add GPUs yet, there will be a future section on how to do that.
- In the "firewall" section (not included in the following screenshot), you probably want to check "allow HTTP traffic" and "allow HTTPS traffic" in case you need network connection to your VM.
- At last, you may need a larger disk than the default setup to store more data. (In fact, the default setup cannot even contain anaconda that we will download soon.) In the "boot disk" section, click on "change", and make the disk as large as you wish. As our habit, we typically use something like 100 GB.
<img src="/Step00_set_up_GCP/Images/VM_configuration.png" width="800px" height="600px">

<img src="/Step00_set_up_GCP/Images/make_disk_larger.png" width="400px" height="300px">

Click "create" on the very bottom of the page once you are confident in the selections.

</details>

<details>
<summary>6. How to start/stop the VM instance, <strong>and friendly warnings</strong>.</summary>
<br>

- **The VM is automatically started now. You need to manually stop it if you don't need it right away.**
- **Whenever the VM is in the "start" status you are charged for the computational resource. We have a friend being charged $400+ because she forgot to hit "stop" and left the VM running for several months after a computer science course. So please "stop" it when you are not using it.**
- In most cases, you only need to use the "start" and "stop" button. If you click "reset" you will most likely lose any data you put on the VM. If you are done with the course and really no longer what this VM you can "delete" it as you wish.
<img src="/Step00_set_up_GCP/Images/start_VM.png" width="800px" height="300px">

</details>

<details>
<summary>7. Open VM SSH Terminal.</summary>
<br>

After you "start" the instance, you may open the SSH Terminal by clicking the following button. It usually takes half a minute or so before you are brought to the next window.
<img src="/Step00_set_up_GCP/Images/VM_SSH_open.png" width="800px" height="200px">

</details>

<details>
<summary>8. VM SSH Terminal.</summary>
<br>

The GCP VM SSH terminal looks like this. You can pretty much use any Linux command line code here.
<img src="/Step00_set_up_GCP/Images/VM_SSH_terminal.png"  width="800px" height="200px">

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

<details>
<summary>10. But I want GPU on my VM... How?</summary>
<br>

As we have mentioned before, the VM configuration above are just for a VM without GPU. However, there are future cases that you do need a GPU, for example, an assignment with GPU requirement or the final project. Therefore we made this section specifically to help you set up a VM with GPU.

**Please note that you'd better stop the VM with GPU once it is successfully created, and never start it when you truly need it, because the unit cost of the GPU-VM is significantly higher than its non-GPU counterpart.**

  <details>
  <summary>Action 1. Upgrade your account.</summary>
  <br>
  
  Do not let this title scare you. The upgrade action is free (to the best of our knowledge).
  
  Go to GCP Console > "IAM & admin" > "Quotas".
  
  <img src="/Step00_set_up_GCP/Images/Quotas.PNG" width="500px" height="200px">
  
  Click on "upgrade account"
  
  <img src="/Step00_set_up_GCP/Images/Quotas_upgrade_account.PNG" width="300px" height="100px">
  
  </details>

  <details>
  <summary>Action 2. Check your GPU quotas.</summary>
  <br>
  
  Once you upgraded your account, you can take a look at your GPU quotas. You can clearly see 4 options, "Quota type", "Service", "Metric", and "Location". Go to "Metric" and deselect everything by clicking on the "None" button in blue, and only select "GPUs (all regions)". You will see that your GPU limit is set to 0, which means you are not allowed any GPU.
  
  <img src="/Step00_set_up_GCP/Images/Quotas_GPUs.PNG" width="600px" height="200px">
  </details>
  
  <details>
  <summary>Action 3. Request increase in GPU quotas.</summary>
  <br>
  
  The next thing to do is to request an increase in your GPU quotas. Select that quota, click on "EDIT QUOTAS" and file a request. Fill in your contact information and update the quota limit to 1 instead of 0.
  
  <img src="/Step00_set_up_GCP/Images/Quota_request_global.PNG" width="800px" height="300px">
  
  Once you have sent that request, you will be notified by both the following words and a confirmation email. **It usually takes 2 business days for the request to be approved.**
  
  <img src="/Step00_set_up_GCP/Images/Quota_request_global_sent.PNG" width="400px" height="150px">
  
  </details>
  
  <details>
  <summary>Action 4. VM configuration - with GPU.</summary>
  <br>
  
  This time we are about to create a VM with GPU. Please use the link provided by [GCP Deep Learning VM](https://console.cloud.google.com/marketplace/details/click-to-deploy-images/deeplearning?_ga=2.19262078.750252723.1580157876-591983468.1579623379).
  
  The recommended configurations are as follows. Please remember to ask it to install the NVIDIA GPU Driver.
    
  </details>

