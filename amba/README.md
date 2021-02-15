

# Users Guide

## Get source repositories
> Refer to ***riscv_env_setup.pdf***

> In this document ${REPO_ROOT} refers to the directory where the repositories were installed.

## Apply a patch into the build script to use docker environment
> This patch allows the toolchain to be stored into `${REPO_ROOT}/riscv-toolchain` directory.

> By default the toolchain will be installed into `~/riscv-toolchain` but it is not suitable for using docker environment.
```
cd ~/swallow-riscv/tools
patch -p1 < tools.patch
```

## Build docker

> You need to change `USERID`, `USERPASSWD` and `SHARED_VOLUME_LOCAL` in the `Makefile`.

> Do `make`

```
make
```

## Start docker

> Just to `make run`
```
make run
```

## Initialize
### [HOST] Login to the docker as `root`. (The password of `root` is `root`)
> I recommend you to use the same username in between your desktop and docker to avoid permission issues.

```
ssh localhost -p 7022 -l root
```
> Then you can see below:
```
The authenticity of host '[localhost]:7022 ([127.0.0.1]:7022)' can't be established.
ECDSA key fingerprint is SHA256:JlLrtyvmXJbYg+oQ84D4IRT7PyjGX8N2JxHWQqJjfSc.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '[localhost]:7022' (ECDSA) to the list of known hosts.
root@localhost's password:
```
> Enter `root` for the password and you can login to the docker.

### [DOCKER] Add a user

```
adduser <YOUR-USERNAME>
```
> Then you can see below:
```
Adding user `<USERNAME>' ...
Adding new group `<USERNAME>' (1000) ...
Adding new user `<USERNAME>' (1000) with group `<USERNAME>' ...
Creating home directory `/home/<USERNAME>' ...
Copying files from `/etc/skel' ...
Enter new UNIX password: 
Retype new UNIX password: 
passwd: password updated successfully
Changing the user information for <USERNAME>
Enter the new value, or press ENTER for the default
	Full Name []: 
	Room Number []: 
	Work Phone []: 
	Home Phone []: 
	Other []: 
Is the information correct? [Y/n] 
[docker] exit or <CTRL-D>
```

### [HOST] Login to the docker as `YOUR-USERNAME`.
```
ssh localhost -p 7022
or
ssh localhost -p 7022 -l <YOUR-USERNAME> # if you don't use the same username.
```

### [DOCKER] Setup toolchain path in the docker
```
echo export PATH=$PATH:/swallow-riscv/riscv-toolchain/bin >> ~/.bashrc
source ~/.bashrc
```

### [DOCKER] Build for the first time.
> First build makes a toolchain and stores them into `/swallow-riscv/riscv-toolchain`
```
cd /swallow-riscv
./tools/build.sh -b drone -f
```
