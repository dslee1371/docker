# Python package install

## Add repo and install packages as python
```
root@dslee-haproxy:~# subscription-manager repos --enable rhel-7-server-optional-rpms --enable rhel-server-rhscl-7-rpms
리포지터리 'rhel-7-server-optional-rpms'가 이 시스템에 대해 활성화되어 있습니다.
리포지터리 'rhel-server-rhscl-7-rpms'가 이 시스템에 대해 활성화되어 있습니다.

# yum -y install @development
# yum -y install rh-python36

# subscription-manager repos --enable rhel-7-server-optional-rpms \
  --enable rhel-server-rhscl-7-rpms
# yum -y install @development
# yum -y install rh-python36

# yum -y install rh-python36-numpy \
 rh-python36-scipy \
 rh-python36-python-tools \
 rh-python36-python-six
```

## Use python package

```
$ scl enable rh-python36 bash
$ python3 -V
Python 3.6.3

$ python -V  # python now also points to Python3
Python 3.6.3

$ mkdir ~/pydev
$ cd ~/pydev

$ python3 -m venv py36-venv
$ source py36-venv/bin/activate

(py36-venv) $ python3 -m pip install ...some modules...
```

