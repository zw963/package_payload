# package_payload

Package payload is for package a executable binary and all it's dependencies into only one file in linux.

# How to use it.

This project comes with a sample app, which called [dte](https://gitlab.com/craigbarnes/dte), a powerful 
command line editor for editing in remote linux host or docker, a perfect replacement for nano.

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

The first args `example/bin/dte` is where the binary file name you want to place.
The secondary args `example/dte` is the location of `dte folder` which need package.

Use package_payload, you can package all your's personal config along with binary into only one bash script, 
and copy to anywhere run it directly.

e.g. you want use it on your's VPS, we assume 123.123.123.123.

```sh
$: scp example/bin/dte user@123.123.123.123:
$: ssh user@123.123.123.123
S: ./dte
```
or if you have root access, you can do like this too.

```sh
$: example/bin/dte root@123.123.123.123
dte                                   100%  449KB   1.5MB/s   00:00    
Web console: https://10-8-2-238:9090/ or https://10.8.2.238:9090/

Last login: Wed Apr 21 17:21:47 2021 from 118.73.114.209
[root@10-8-2-238 ~]# 
```
