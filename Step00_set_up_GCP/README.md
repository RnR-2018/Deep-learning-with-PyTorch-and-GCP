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
<img src="/Step00_set_up_GCP/Images/VM_instance.png" alt="VM_instance" width="500px" height="200px">

6. Configure the VM according to your needs. 
- The region and zone probably doesn't matter.
- Please select the computational resources (number of CPUs and amount of memory) according to your needs. In this case we selected 4 CPUs and 26 GB memory. You might want larger memory depending on your project.
- Also note that on the upper right corner there is an estimation of the monthly cost based on your current configuration. That gives you a rough idea on how you want to manage your budget.
- For students enrolled in the BMEN4460 instructed by Dr. Andrew Laine and Dr. Jia Guo, you are strongly suggested to select the "Debian GNU/Linux 9 (stretch)" for the Boot disk.
- In the "firewall" section (not included in the following screenshot), you probably want to check "allow HTTP traffic" and "allow HTTPS traffic" in case you need network connection to your VM.
<img src="/Step00_set_up_GCP/Images/VM_configuration.png" alt="VM_configuration" width="800px" height="600px">

7.
