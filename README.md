# package_payload

Package payload is for package a folder into a executable binary for UNIX-LIKE system.

# How to use it.

Maybe the most easy way to understand how this package work is use examples.

This project comes with some pre-packaged app:

1. [dte](https://gitlab.com/craigbarnes/dte), a very powerful command line editor for editing in remote linux host or docker, a perfect replacement for nano, and more, you can check original unpacked version dte [here](https://github.com/zw963/package_payload/tree/main/example/dte). __NOTICE: To achieve the best user experience, please use it together with [wezterm](https://github.com/wez/wezterm)__, and if you are a Emacs enthusiast, you can try my [.wezterm.lua](https://gist.github.com/zw963/b02e1cd320538a7276f0e0b666b2b8cc) for a awesome emacs user experience, with in docker, remote VPS etc.
2. docker_bash, as it name, run bash for docker,  a script for easy interact with docker.
   it can work as following:
   - docker_bash a_docker_image
   - docker_bash a_existing_container
   - docker_bash a_failed_container
   - docker_bash a_docker_volume
   
   For the purpose of package_payload, we want to attach dte editor into docker_bash, when we in container, we can use dte free.

## 1. package dte editor files which in folder `packages/dte` into `bin/dte`.

```sh
$:  ./package_payload bin/dte packages/dte/
./
./.dte/
./.dte/rc
./bin.real/
./bin.real/dte
./bin/
./bin/dte
./bin/dteinit
./bin/nano
./bin/update_dte
./share/
./share/man/
./share/man/man1/
./share/man/man1/dte.1
./share/man/man5/
./share/man/man5/dte-syntax.5
./share/man/man5/dterc.5
```

The first args `bin/dte` is where the new packaged binary you want to place.
The secondary args `packages/dte/` is the folder where the `dte editor` files live in.
`package/dte/bin/dte` must exists, and must executable, and will be invoke when packaged script is running.

**NOTICE:** current dte keyboard binding configured as a emacs replacement, if you are not a emacser, you need adjust [config file](https://github.com/zw963/package_payload/blob/main/example/dte/.dte/rc) follow [offical document](https://craigbarnes.gitlab.io/dte/dterc.html)

Use package_payload, you can package binary along with all your's personal config into only one file (bash script).

**Now, we have a lonely binary `bin/dte`, you can copy it to any unix-like system,  and run it directly.**

e.g. copy to your's remote VPS with IP of 123.123.123.123.

```sh
$: scp example/bin/dte user@123.123.123.123:
$: ssh user@123.123.123.123
S: ./dte
```

There is a more quicky way to copy script into VPS's /usr/local/bin/ then ssh logged in.

```sh
 ╰─ $ dte root@192.168.50.111
dte                       100%  491KB  17.0MB/s   00:00    
Last login: Fri Jan 19 00:44:22 2024 from 192.168.50.44
[root@localhost ~]# dte -V
dte 1.11.1-317-gb5aa677c
[root@localhost ~]# 

```

## 2. package docker_bash with dte.

    - create folder, `packages/docker_bash/bin`, and copy original docker_bash script into it.
	 - `cd packages/docker_bash/bin`
	 - create a hardlink to above packaged dte editor. `ln ../../../bin/dte .`
	 - cd back to project root folder. 
	 - run `./package_payload bin/docker_bash packages/docker_bash/`
 
Now, we have a lonely binary `bin/docker_bash`, you can try play it with docker, and don't forget,  
you can always use `dte` or a alias `nano` when you in container.

# Following is the list of pre-packaged binary.

[dte](/bin/dte)

[docker_bash](/bin/docker_bash)

[iotop](/bin/iotop)
