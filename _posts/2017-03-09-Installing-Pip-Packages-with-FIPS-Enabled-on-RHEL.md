---
published: true
---
## How to install pip packages for python when FIPS is enabled on a RHEL7/CentOS7 machine

I came across a problem recently with one of the machines I work with running RHEL7. FIPS is enabled, not allowing the md5 hash to be used for verifying python packages when using pip. 

On RHEL7.3 Python 2.7.5 is installed.
```bash
$: python -V
Python 2.7.5
```

If I attempted to install pip, per [the documentation](https://packaging.python.org/installing/#install-pip-setuptools-and-wheel), I would eventually get a "Unknown hash name: md5" error: 
```bash
$: curl –O https://bootstrap.pypa.io/get-pip.py
$: python get-pip.py
Collecting pip
  Downloading pip-9.0.1-py2.py3-none-any.whl (1.3MB)
Unknown hash name: md5
```

The problem is that FIPS is enabled (noted by the "1"): 
```
$: cat /proc/sys/crypto/fips_enabled
1
```

For my environment, I cannot turn off FIPS. You can spin up a clean CentOS 7 VM and do the above and it works just fine beacuse FIPS isn't enabled. If you run into this issue, then you you need to do the following: 
1. Install pip via rpm:
```
$: curl -O ftp://mirror.switch.ch/pool/4/mirror/centos/7.3.1611/cloud/x86_64/openstack-newton/common/python-pip-8.1.2-1.el7.noarch.rpm


$: sudo yum install python-pip-8.1.2-1.el7.noarch.rpm
```   
2. With pip now installed, install your desired package, but use the `-i` arugment like so:
```bash
$: pip install <SOME_PACKAGE> -i https://pypi.org/simple/


$: pip install lifelines -i https://pypi.org/simple/
```
3. You may get a warning to upgrade, which you can perform like so: 
```bash
sudo pip install --upgrade pip -i https://pypi.org/simple/
```
