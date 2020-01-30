# Manage Anaconda on Google Cloud Platform.
Nanyan "Rosalie" Zhu and Chen "Raphael" Liu.

## Latest update
If you used the "Compute Engine" > "Marketplace" > "Deep Learning VM" pre-packaged method (introduced in the previous chapter) to create your VM, you should have anaconda and jupyter installed already. **In this case, your anaconda is installed at /opt/anaconda3/**. You can skip the installation steps and only look at how to utilize them (specifically step 5 to 10).

**Before doing anything else, if you used this method to create your VM, you should execute the following line in the GCP VM SSH Terminal to grant you super user authority, because your anaconda is installed in a protected directory.**
```
sudo su
```

## Overview
This is written for installing and setting up anaconda on GCP, but can be applied on other devices (i.e., your own Mac or Linux computer) with little to not modification as well. Windows users might have more hussles as the commands are quite different. The following instruction assumes a Linux (Ubuntu/Debian/etc) operating system (as how you should have configured your GCP VM instance).

## Step-by-step instructions

<details>
<summary>1. Download and install Anaconda 3.</summary>
<br>

1) Find a suitable Anaconda 3 at the [Anaconda installer archive](https://repo.continuum.io/archive/).
    In this case, we chose Anaconda3-2019.10-Linux-x86_64.sh

2) Download the Anaconda Archive package. In the ssh terminal, enter:
    ```
    wget http://repo.continuum.io/archive/Anaconda3-2019.10-Linux-x86_64.sh
    ```

3) Install the package "bzip2", and install Anaconda 3 with the Archive package.
    ```
    sudo apt-get install bzip2
    bash Anaconda3-2019.10-Linux-x86_64.sh
    ```
    
4) Once you run the installation command, there will be text instructions that guide you through the installation.
    * You can choose to install anaconda at any place you want. You may choose the default **"/home/[username]/anaconda3"** path.
    * When the installation kit asks whether or not to **initialize Anaconda3 by running conda init**, please choose "yes". This will save you the trouble of configuring the ~/.bashrc file, so that you can skip the next step.

</details>


<details>
<summary>2. (Optional) Add the path of anaconda to the system PATH.</summary>
<br>

**This is not necessary if you asked the anaconda installation kit to set the path for you.**

```
sudo nano ~/.bashrc
```

and add the following line to your system file.
```
export PATH="$PATH:/home/[username]/anaconda3/bin"
```
    
Please replace **"[username]"** with your own username. In our case, our username is msnanyanzhu. <img src="/Step01_manage_anaconda_on_GCP/Images/user_name.png" alt="user_name" width="300px" height="40px">

</details>

<details>
<summary>3. Now, refresh the system.</summary>
<br>

You can either run the following code in the SSH Terminal

```
source ~/.bashrc
```

or alternatively, exit out the VM SSH Terminal (by closing the web browser tag hosting the VM SSH Terminal) and reopen the terminal again. Either way, after the refreshing the command "conda" can be recognized.

</details>

<details>
<summary>4. Update Anaconda.</summary>
<br>

```
conda update --prefix /home/[username]/anaconda3 -c anaconda anaconda
```

</details>

<details>
<summary>5. Create Virtual Environment.</summary>
<br>

```
conda create -n [environment name] -c anaconda python=3.7 [package name] [package name]
```
    
Example:
```
conda create -n BMEN4460 -c anaconda python=3.7
```

**environment name** is the name you give to the new anaconda environment. In this case, we use "BMEN4460".

**python=3.7** specifies that the python version 3.7 to be installed in this environment. If you want a different version, change it to what you want.

**-c anaconda** specifies the channel from which the package will be downloaded. Personally I recommend **anaconda**. In case the package is not available in anaconda, go search it on the web and find a decent source.

**package name** specifies the packages to be installed in this environment. It makes no difference whether to specify the package names to be installed here or in Step 7.

</details>

<details>
<summary>6. Activate Virtual Environment.</summary>
<br>

```
conda activate [environment name]
```

Example:
```
conda activate BMEN4460
```

**If you encounter trouble in this step, you may need to close and reopen your SSH Terminal. Remember to execute "sudo su" again if you used the Deep Learning VM quick creation.**

</details>

<details>
<summary>7. Install Packages.</summary>
<br>

```
conda install -c anaconda [package name] [package name] ...
```

**-n [environment name]** specifies which environment to install the packages in. It is not necessary if the environment currently activated is your target environment.
  
**NOTE**: Hierarchy of package installation methods (ranked from "recommended" to "don't try this if you have any other method" according to our experience)
- Option 1 syntax (best)
```
conda install -c anaconda [packagename]
```
Example:
```
conda install -c anaconda jupyter
```
- Option 2 syntax (good)
```
conda install -c conda-forge [packagename]
```
- Option 3 syntax (not very good)
```
conda install [packagename]
```
- Option 4 syntax (not recommended)
```
python -m pip install [packagename]
```
- Option 5 syntax (not recommended)
```
pip install [packagename]
```
</details>

<details>
<summary>8. Install Packages (continued).</summary>
<br>

Besides these popular methods, in case you want to install a non-anaconda package that is not included in either anaconda or conda-forge, the best shot you have to safely install it is by googling **"anaconda install [this non-anaconda package]"**, and find the offical answer given by anaconda cloud.
    
For instance, if you want to install **"dtw"**, doing so will redirect you to **"conda install -c freemapa dtw"**.

</details>

<details>
<summary>9. Download a package from GitHub.</summary>
<br>

To download a package (not a repository) from github, you can use following command:
```
conda install git pip
pip install git+[git_url]
```

Example:
```
git clone https://github.com/jonbarron/robust_loss_pytorch
cd robust_loss_pytorch/
pip install -e .[dev]
```

You can refer to the specific GitHub package when you really come across this case. Note that whichever folder you are currently in when you type the following git clone command, the repository will be downloaded to that folder.

Note that is different from downloading a repository from GitHub, which is much easier:
```
git clone [GitHub repository]
```
Example (we recommend creating a "Projects" folder and cloning this repo there):
```
mkdir Projects
cd Projects
git clone https://github.com/RnR-2018/BMEN4460-NB1-simple_cell_segmentation_with_a_single_layered_perceptron
```

</details>

<details>
<summary>10. Recommended packages for BMEN4460.</summary>
<br>

```
conda install -c pytorch torchvision pytorch
conda install -c simpleitk simpleitk
conda install -c anaconda matplotlib numpy jupyterlab jupyter scikit-learn scikit-image
```
</details>

## End of this chapter: Step01_manage_anaconda_on_GCP.
