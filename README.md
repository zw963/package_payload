# package_payload

Package payload is for package a executable binary and all it's dependencies into only one file on linux.
It should works on any UNIX-LIKE system, e.g. OSX, BSD etc because it only just a tiny bash script.

# How to use it.

Maybe the most easy way to understand how this package work is use examples.

This project comes with two sample app:

1. [dte](https://gitlab.com/craigbarnes/dte), a very powerful command line editor for editing in remote linux host or docker, a perfect replacement for nano, and more, you can check original unpacked version dte [here](https://github.com/zw963/package_payload/tree/main/example/dte). 
2. docker_bash, as it name, run bash for docker,  a script for easy interact with docker.
   it can work as following:
   - docker_bash a_docker_image
   - docker_bash a_existing_container
   - docker_bash a_failed_container
   - docker_bash a_docker_volume
   
   For the purpose of package_payload, we want to attach dte editor into docker_bash, when we in container, we can use dte free.

## 1. package dte editor files which in `example/dte` into only one file `example/bin/dte`.

```sh
$:  ./package_payload example/bin/dte example/dte
./
./bin.real/
./bin.real/dte
./bin/
./bin/nano
./bin/update_dte
./bin/dteinit
./bin/dte
./share/
./share/man/
./share/man/man5/
./share/man/man5/dte-syntax.5
./share/man/man5/dterc.5
./share/man/man1/
./share/man/man1/dte.1
./.dte/
./.dte/rc
```

The first args `example/bin/dte` is where the new packaged binary you want to place.
The secondary args `example/dte` is a folder, is where the `dte editor` files live in,  `example/dte/bin/dte` must exists, and must executable, and will be run when packaged script is running.

**NOTICE:** current dte keyboard binding configured as a emacs replacement, if you are not a emacser, you need adjust [config file](https://github.com/zw963/package_payload/blob/main/example/dte/.dte/rc) follow [offical document](https://craigbarnes.gitlab.io/dte/dterc.html)

Use package_payload, you can package binary along with all your's personal config into only one file (bash script).

**Now, we have a lonely binary `example/bin/dte`, which can be run anywhere even after delete all original files in `example/dte`.**

e.g. you want use this editor on your's remote VPS with IP of 123.123.123.123.

```sh
$: scp example/bin/dte root@123.123.123.123:/usr/local/bin/
$: ssh root@123.123.123.123
S: dte
```

## 2. package docker_bash with dte.

    - create folder, `example/docker_bash/bin`, and copy original docker_bash script into it.
	 - `cd example/docker_bash/bin`
	 - create a hardlink to above packaged dte editor. `ln ../../bin/dte dte`
	 - cd back to project root folder. run `./package_payload example/bin/docker_bash example/docker_bash`
 
Now, we have a lonely binary `example/bin/docker_bash`, you can try play it with docker, and don't forget,  
you can always use `dte` or a alias `nano` when you in container.

# Following is the list of pre-packaged binary.

[docker_bash](/example/bin/docker_bash)
