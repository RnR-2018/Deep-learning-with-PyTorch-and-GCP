# Manage Anaconda on Google Cloud Platform.
Nanyan "Rosalie" Zhu and Chen "Raphael" Liu.

## Overview
This is written for installing and setting up anaconda on GCP, but can be applied on other devices as well. The following instruction assumes a Linux operating system.

## Step-by-step instructions
1. Download and install Anaconda 3.
    1. Find a suitable Anaconda 3 at the Anaconda installer archive

        [Anaconda installer archive](https://repo.continuum.io/archive/)

        In this case, we chose Anaconda3-2019.10-Linux-x86_64.sh

    2. Download the Anaconda Archive package. In the ssh terminal, enter:

            wget http://repo.continuum.io/archive/Anaconda3-2019.10-Linux-x86_64.sh

    3. Install the package "bzip2", and install Anaconda 3 with the Archive package.

            sudo apt-get install bzip2
            bash Anaconda3-2019.10-Linux-x86_64.sh

2. Add the path of anaconda to the system PATH.

        export PATH="$PATH:/home/[username]/anaconda3/bin"

    Please replace "[username]" with your own username. For instance, in this case <img src="/Step01_manage_anaconda_on_GCP/Images/user_name.png" alt="username" width="200px" height="20px"> the username is "msnanyanzhu". 

3. Now, exit out the VM SSH terminal (by exiting out this webpage) and reopen the terminal again. Now the command "conda" can be recognized.

4. Update Anaconda

        conda update --prefix /home/[username]/anaconda3 -c anaconda anaconda

5. Create Virtual Environment [environment name].

        conda create -n [environment name] -c anaconda python=3.7 [package name] [package name]

    **python=3.7** specifies that the python version 3.7 to be installed in this environment. If you want a different version, change it to what you want.

    **-c anaconda** specifies the channel from which the package will be downloaded. Personally I recommend **anaconda**. In case the package is not available in anaconda, go search it on the web and find a decent source.

    **package name** specifies the packages to be installed in this environment. It makes no difference whether to specify the package names to be installed here or in Step 7.

6. Activate Virtual Environment

        source activate [environment name]

7. Install Packages

        conda install -c anaconda [package name] [package name] ...

    **-n [environment name]** specifies which environment to install the packages in. It is not necessary if the environment currently activated is your target environment.
  
  **NOTE**: Hierarchy of package installation methods (ranked from "recommended" to "don't try this if you have any other method" according to our experience)
  - No.1

      > conda install -c anaconda **packagename**

  - No.2

      > conda install -c conda-forge **packagename**

  - No.3

      > conda install **packagename**

  - No.4

      > python -m pip install **packagename**

  - No.5

      > pip install **packagename**
  
    Besides these popular methods, in case you want to install a wierd package that is not included in either anaconda or conda-forge, the best shot you have to safely install it is by googling "anaconda install [this wierd package]", and find the offical answer given by anaconda cloud. For instance, if you want to install "dtw", doing so will redirect you to "conda install -c freemapa dtw".

8. To download a package from github, you can use following command:
      > conda install git pip<br/>
      > pip install git+<git_url>

9. Recommended packages for BMEN4460.

## End of this chapter: Step01_manage_anaconda_on_GCP.
