# Managing Jupyter Kernel.
Nanyan "Rosalie" Zhu and Chen "Raphael" Liu

## Overview
This chapter has two major sections.
* Section 1. Set up the essential configurations on GCP to empower the use of jupyter lab.
* Section 2. Use jupyter lab on GCP.

## Section 1. Set up the essential configurations on GCP to empower the use of jupyter lab.
### Step 1. Configure a static external IP address.
*To be honest this is not essential, but will make your future life easier. If the IP address is not set to be static, it might change every now and then, and you might have to look up the new IP address each time you need it.*

1. On GCP, go to "VPC network" > "External IP addresses".
<>


## Section 2. Use jupyter lab on GCP.

- Activate the environment you need to work with
    ```
    conda activate [myenv]
    ```
    
- Make sure that you have installed jupyter lab or jupyter notebook. If not, you can use following command to install one of them.
    ```
    conda install jupyter jupyterlab -c anaconda
    ```
    or
    ```
    conda install jupyter jupyternotebook -c anaconda
    ```
- Install a jupyter notebook kernel in the respective environment
    ```
    python -m ipykernel install --user --name [myenv] --display-name "[Python (myenv)]"
    ```
- Now the jupyter kernel is distinctively pointing to the python in the corresponding environment

- The next step is open jupyter lab
    ```
    jupyter lab
    ```
