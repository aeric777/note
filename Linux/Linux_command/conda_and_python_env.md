# Conda & Python env

# env unassigned
``` bash
$ conda activate [env_name]  # default in base

$ conda deactivate  # deactivate from current env
```


## env management
``` bash
# check all envs
$ conda env list

# create env (requires env_name, python_ver and pip)
$ conda create --name [env_name] python==[version] pip

# remove env
$ conda remove --name [env_name] --all

# clone env
$ conda create -n [lod_env] --clone [new_env]
```

# uninstall conda
1. remove all conda files in miniconda3(using miniconda as example)
2. delete configuration in you .bashrc(using bash as example)


## Python environment configuration

It's highly recommended that you should managing python virtual env using miniconda or anaconda

``` bash
# first in first
# you can always check more info in /usr/bin

python3 --version   # check version
sudo apt remove python3 # uninstall python
sudo apt install python3.9  # install python3.9
```


``` bash
$ which python  # check where your current python installed
$ sudo whereis python   # look for all the python install in your system


# remove python2.7
$ sudo apt remove python2.7
$ sudo apt remove --auto-remove python2.7

$ sudo apt purge python2.7
$ sudo apt purge --auto-remove python2.7
```