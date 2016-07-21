qcom-oe-manifest
================

Qualcomm OE BSP standalone manifest repository

These are the setup/test scripts for the Qualcomm OE BSP layer. This manifest can be used to (re)build QCOM BSP layer for OpenEmbedded core.

To configure the scripts and download the build metadata, do:
```
$ mkdir ~/bin
$ PATH=~/bin:$PATH

$ curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
$ chmod a+x ~/bin/repo
```
Run repo init to bring down the latest version of Repo with all its most recent bug fixes. You must specify a URL for the manifest, which specifies where the various repositories included in the Android source will be placed within your working directory. To check out the current branch, specify it with -b:
```
$ repo init -u https://github.com/ndechesne/qcom-oe-manifest.git -b jethro
```
When prompted, configure Repo with your real name and email address.

A successful initialization will end with a message stating that Repo is initialized in your working directory. Your client directory should now contain a .repo directory where files such as the manifest will be kept.

To pull down the metadata sources to your working directory from the repositories as specified in the default manifest, run
```
$ repo sync
```
When downloading from behind a proxy (which is common in some corporate environments), it might be necessary to explicitly specify the proxy that is then used by repo:
```
$ export HTTP_PROXY=http://<proxy_user_id>:<proxy_password>@<proxy_server>:<proxy_port>
$ export HTTPS_PROXY=http://<proxy_user_id>:<proxy_password>@<proxy_server>:<proxy_port>
```
More rarely, Linux clients experience connectivity issues, getting stuck in the middle of downloads (typically during "Receiving objects"). It has been reported that tweaking the settings of the TCP/IP stack and using non-parallel commands can improve the situation. You need root access to modify the TCP setting:
```
$ sudo sysctl -w net.ipv4.tcp_window_scaling=0
$ repo sync -j1
```
Setup Environment
-----------------

Any MACHINE from meta-qcom/conf/machine can be used. This manifest is supposed to be used to build a pristine OpenEmbedded Core 'nodistro' configuration.

```
$ . setup-environment
$ MACHINE=<machine> bitbake <image>
```
e.g. MACHINE=dragonboard-410c bitbake core-image-minimal

Updating the sandbox
--------------------

If you need to bring changes from upstream then use following commands
```
$ repo sync
```
Rease your local committed changes
```
$ repo rebase
```
If you find any bugs please report them here

https://github.com/ndechesne/qcom-oe-manifest/issues

If you have questions or feedback, please subscribe to

https://lists.linaro.org/mailman/listinfo/openembedded

Maintainer
-------------------------

* Nicolas Dechesne <nicolas.dechesne@linaro.org>
