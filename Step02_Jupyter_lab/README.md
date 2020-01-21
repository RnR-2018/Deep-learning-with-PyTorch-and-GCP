# Managing Jupyter Lab.
Nanyan "Rosalie" Zhu and Chen "Raphael" Liu

- Activate the environment you need to work with
    ```
    conda activate [myenv]
    ```
- Install a jupyter notebook kernel in the respective environment
    ```
    python -m ipykernel install --user --name [myenv] --display-name "[Python (myenv)]"
    ```
- Now the jupyter kernel is distinctively pointing to the python in the corresponding environment

- Make sure that you have installed jupyter lab or jupyter notebook. If not, you can use following command to install one of them.
    ```
    conda install jupyter jupyterlab -c anaconda
    or 
    conda install jupyter jupyternotebook -c anaconda
    ```
- The next step is open jupyter lab
    ```
    jupyter lab
    ```
