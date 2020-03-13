# libconainer-1535-systemmd-test-default-dependencies.scop has no PODs.

```

#저널 오류가 발생하고 있음
Dec 12 16:04:29 hub-master.futuregen.com systemd[1]: Scope libcontainer-1538-systemd-test-default-dependencies.scope has no PIDs. Refusing.
Dec 12 16:04:29 hub-master.futuregen.com systemd[1]: Scope libcontainer-1525-systemd-test-default-dependencies.scope has no PIDs. Refusing.
Dec 12 16:04:29 hub-master.futuregen.com systemd[1]: Scope libcontainer-1606-systemd-test-default-dependencies.scope has no PIDs. Refusing.


#도커 설정 테스트 해보기로 함 > 데몬 로드하는데에서 오류가 발생 함 > 원복
systemctl stop docker
sed '/native.cgroupdriver=systemd/d' /usr/lib/systemd/system/docker.service > /etc/systemd/system/docker.service
systemctl daemon-reload
systemctl start docker


#/etc/systemd/system/docker.service 의 파일을 다음의 내용으로 생성하고 해당 이슈를 해결 함 
[Unit]
Description=Docker Application Container Engine
Documentation=https://docs.docker.com
After=network-online.target firewalld.service
Wants=network-online.target

[Service]
Type=notify
# the default is not to use systemd for cgroups because the delegate issues still
# exists and systemd currently does not support the cgroup feature set required
# for containers run by docker
ExecStart=/usr/bin/dockerd 
ExecReload=/bin/kill -s HUP $MAINPID
# Having non-zero Limit*s causes performance problems due to accounting overhead
# in the kernel. We recommend using cgroups to do container-local accounting.
LimitNOFILE=infinity
LimitNPROC=infinity
LimitCORE=infinity
# Uncomment TasksMax if your systemd version supports it.
# Only systemd 226 and above support this version.
#TasksMax=infinity
TimeoutStartSec=0
# set delegate yes so that systemd does not reset the cgroups of docker containers
Delegate=yes
# kill only the docker process, not all processes in the cgroup
KillMode=process
# restart the docker process if it exits prematurely
Restart=on-failure
StartLimitBurst=3
StartLimitInterval=60s

[Install]
WantedBy=multi-user.target
```
