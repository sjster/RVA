
**These instructions apply for a cloud instance, server or local machine which has a Ubuntu OS and the ssh user set to 'ubuntu'.** For other users, replace /home/ubuntu/ with /home/{USER} in the .yml files and the .conf files. Currently, the playbook is not setup to work on non-Ubuntu installations. 

## Ubuntu

1. Edit the hosts file to add the IP address of your instance

2. Assuming you have ansible installed and the cloud instance has ubuntu as the ssh user with install privileges, run the following from the ansible folder:

   ansible-playbook -i ./hosts cloud_h2o.yml

   This reads from the file jupyter.conf to setup a JupyterLab server, **change ports as appropriate in this file but make sure that the relevant ports are also open on the instance**. Also, **set a password for the JupyterLab instance in the jupyter.conf file**.

## H2O

This ansible playbook installs a H2O instance into a conda environment named keras_env. This has Jupyterlab installed and is accessible at port 80. 

## H20 GPU

You can install H2O for GPU into a conda environment named keras_env2 with the command

conda create -c conda-forge -c h2oai -y -n keras_env2  h2o4gpu-cuda10 pandas scikit-learn jupyter jupyter_client==5.3.3 jupyterlab

Start Jupyterlab from the command line as 

/home/ubuntu/Anaconda/envs/keras_env2/bin/jupyter lab --allow-root  --ip 0.0.0.0 --no-browser --port 8000 --NotebookApp.token={password}

Make sure your instance has port 8000 open so that you can access your JupyterLab instance
