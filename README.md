# SCINet Notes
==============

## General
----------

### Project Storatge

The project storage lives in `/project/umontana_fire_modeling`. Create a
directory for your data at `/project/umontana_fire_modeling/$USER`. For me,

```sh
[username@Atlas-login-1 ~]$ mkdir /project/umontana_fire_modeling/$USER
```
creates a directory within our project dir that is the same as your username.

**NOTE: Data under `/project/` is not backed up**

### Conda

Load the miniconda module to get access to conda:

```sh
$ module load miniconda
```

#### Conda Setup

```sh
$ mkdir /project/umontana_fire_modeling/$USER/conda
$ mkdir /project/umontana_fire_modeling/$USER/conda/envs
$ mkdir /project/umontana_fire_modeling/$USER/conda/pkgs
$ conda config --add channels conda-forge
$ conda config --set channel_priority strict
```
Add the following to your `~/.condarc` file:

```yaml
pkgs_dirs:
  - /project/umontana_fire_modeling/<USER NAME>/conda/pkgs
```

This sets the cache directory for downloaded python packages to point to the
`pkgs` dir that you created in the previous step. This prevents conda from
filling you local storage quota.

#### Conda Create Env

```sh
$ conda create -p /project/umontana_fire_modeling/$USER/conda/envs/my_env
```

You can now activate your new env with

```sh
$ conda activate /project/umontana_fire_modeling/$USER/conda/envs/my_env
```

## Atlas
--------

Ref: [https://www.hpc.msstate.edu/computing/atlas/](https://www.hpc.msstate.edu/computing/atlas/)

### Account

Print the project account your user name is associated with. This is where your
jobs get charged to. You need it in order to spin up jobs in slurm.

```sh
$ sacctmgr show associations where user=$USER format=account%25,qos%25
                  Account                       QOS
------------------------- -------------------------
   umontana_fire_modeling          debug,normal,ood
```

### Interactive Session

Spin up an interactive session on an Atlas node with:

```sh
[username@Atlas-login-1 ~]$ srun -A umontana_fire_modeling --pty --preserve-env bash
[username@Atlas-0129 ~]$
```

### Check Storage Quota

For the entire project:

```sh
$ /apps/bin/reportFSUsage -p umontana_fire_modeling
------------------------------------------------------------------------------------
Directory/Group             Usage(GB)   Quota(GB)   Limit(GB)      Files  Percentage
------------------------------------------------------------------------------------
umontana_fire_modeling            483        8294        9216      86735         5.8
```

For your home directory:

```sh
$ quota -s
Disk quotas for user <username> (uid 123456789):
     Filesystem   space   quota   limit   grace   files   quota   limit   grace
atlas-nfs.hpc.msstate.edu:/home-atlas
                  2334M  10240M  12288M           48995       0       0
```
