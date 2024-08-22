# ubuntu-frr-pod

### building ubuntu-frr container image for both amd64 and arm64, and upload it to AWS ECR, change 01234567890 to your AWS account ID
```
aws ecr get-login-password --region us-east-1 | sudo docker login --username AWS --password-stdin 01234567890.dkr.ecr.us-east-1.amazonaws.com
sudo docker buildx build --platform linux/amd64,linux/arm64 -t 01234567890.dkr.ecr.us-east-1.amazonaws.com/sigitp-ecr:ubuntu-frr --push .

[optional, pruning docker space]
docker system prune --all --force --volumes
```

### example build output:
```
Admin:~/environment/ubuntu-frr-dockerfile $ docker system prune --all --force --volumes
Deleted Images:
untagged: 291615555612.dkr.ecr.us-east-1.amazonaws.com/sigitp-ecr:ubuntu-netutils
deleted: sha256:1273d7525ff77623e110aeaf82c810edb5f39babb683ebbad6ec5aa3696c95a7
deleted: sha256:0eb24efda6630436ebb85dff44ffa1bbf0c1bb0bd631849bf69f85f81c86b320
deleted: sha256:15b0d17810626c7e2a701e06b2c80ae78f1243b22fe6cdc0c6f0aa4a393a3d2f
deleted: sha256:f0a56a63552e2e345d2c0832dfc10abd3b49acd78c3a7d19da9ebf7844c6e917
deleted: sha256:682a3e48b42ca17db2af18d2a32026de3eda0590956d83997954a74163522f0c
deleted: sha256:e38dce54ae2e6c951eed8690781035b8a671642011965a8ace93da44a6471b9a
deleted: sha256:07bc96704117e0a9a7ff07c1cf016ccf418e9725bb6622181208125df5ecd12c
deleted: sha256:54146c695a3be683d66f1a6743a94de93aa23ae24420e1220f9d86babf065e06
deleted: sha256:cdc96e5c1e3e153fe57fb21426f5d8155d72d900ad4ea4c34a0e70c94fb401a0
deleted: sha256:29cabf21707171b5c1abe044d2703b21cf726ef9c7db6a1ca789c1bd4e945b4c
deleted: sha256:cbe28a07e910da1daafaa1815e5479a705c28db21e6c8f9633d0b53cce92d0a5

Deleted build cache objects:
lkkfgvhp5qgavbyrke1he4qn0
1tj93ptpamtccez30n9veyhek
ciwaakap5b9yq9ciu0vzpnrxt
nyh2axvbjspoadjzneg655uk5
l4k504y14f6t7gruirqqstsbv
uav9kcnljbdj6p218fpgt4dxa
0kc84dsu10bj6uci9q6i1a6gs
xjsgg27gzkgblopt56j7ldohq
z6k6ueado1nh8n02nfmh8e6fv
x65qhyu4y7nhs85v7m4zd0hd6
0hcpa1s20n4bxcc8jzlzt9lrt
k9b3qbogvmzax6x8zzosdw67e
xnlhmy2wpkmz3if5xag11xyiw
ig8ack3uoawal10nlao5rs104
wb0uz9ygmbp3u3axitl72wmik
7v660gez32xkn6b2gxe3aqbd6
symwkdhapjh7tqcft3y057toy
3v6bjkek757wp0ts7kf2ymo5f
gg5pxv0wslwrq1g70h9b66jno
dm6p4rt6fdwmbnkpb0bt5hr6n

Total reclaimed space: 1.239GB

Admin:~/environment/ubuntu-frr-dockerfile $ sudo docker buildx build --platform linux/amd64,linux/arm64 -t 291615555612.dkr.ecr.us-east-1.amazonaws.com/sigitp-ecr:ubuntu-frr --push .
[+] Building 290.1s (19/19) FINISHED                                                                                                             docker:default
 => [internal] load build definition from Dockerfile                                                                                                       0.0s
 => => transferring dockerfile: 483B                                                                                                                       0.0s
 => [linux/arm64 internal] load metadata for docker.io/library/ubuntu:jammy                                                                                0.6s
 => [linux/amd64 internal] load metadata for docker.io/library/ubuntu:jammy                                                                                0.6s
 => [internal] load .dockerignore                                                                                                                          0.0s
 => => transferring context: 2B                                                                                                                            0.0s
 => [linux/amd64 1/6] FROM docker.io/library/ubuntu:jammy@sha256:adbb90115a21969d2fe6fa7f9af4253e16d45f8d4c1e930182610c4731962658                          2.4s
 => => resolve docker.io/library/ubuntu:jammy@sha256:adbb90115a21969d2fe6fa7f9af4253e16d45f8d4c1e930182610c4731962658                                      0.0s
 => => sha256:857cc8cb19c0f475256df4b7709003b77f101215ebf3693118e61aac6a5ea4ff 29.54MB / 29.54MB                                                           0.5s
 => => extracting sha256:857cc8cb19c0f475256df4b7709003b77f101215ebf3693118e61aac6a5ea4ff                                                                  1.9s
 => [linux/arm64 1/6] FROM docker.io/library/ubuntu:jammy@sha256:adbb90115a21969d2fe6fa7f9af4253e16d45f8d4c1e930182610c4731962658                          2.3s
 => => resolve docker.io/library/ubuntu:jammy@sha256:adbb90115a21969d2fe6fa7f9af4253e16d45f8d4c1e930182610c4731962658                                      0.0s
 => => sha256:e63ce922f0229bde5aea9f366c46883dcd23747e7d2c541f16665f199dbf98b8 27.36MB / 27.36MB                                                           0.6s
 => => extracting sha256:e63ce922f0229bde5aea9f366c46883dcd23747e7d2c541f16665f199dbf98b8                                                                  1.7s
 => [linux/arm64 2/6] RUN apt-get update && apt-get -y upgrade                                                                                            57.7s
 => [linux/amd64 2/6] RUN apt-get update && apt-get -y upgrade                                                                                            10.4s
 => [linux/amd64 3/6] RUN apt-get install -y lsb-release net-tools wget git vim curl tcpdump iputils-ping tree jq telnet sudo nano gnupg2                 21.0s
 => [linux/amd64 4/6] RUN curl -s https://deb.frrouting.org/frr/keys.asc | sudo apt-key add -                                                              1.2s
 => [linux/amd64 5/6] RUN echo deb https://deb.frrouting.org/frr $(lsb_release -s -c) frr-stable | sudo tee -a /etc/apt/sources.list.d/frr.list            0.4s
 => [linux/amd64 6/6] RUN apt update && apt install -y frr frr-pythontools                                                                                 9.7s
 => [linux/arm64 3/6] RUN apt-get install -y lsb-release net-tools wget git vim curl tcpdump iputils-ping tree jq telnet sudo nano gnupg2                139.9s 
 => [linux/arm64 4/6] RUN curl -s https://deb.frrouting.org/frr/keys.asc | sudo apt-key add -                                                              8.9s 
 => [linux/arm64 5/6] RUN echo deb https://deb.frrouting.org/frr $(lsb_release -s -c) frr-stable | sudo tee -a /etc/apt/sources.list.d/frr.list            1.0s 
 => [linux/arm64 6/6] RUN apt update && apt install -y frr frr-pythontools                                                                                51.4s 
 => exporting to image                                                                                                                                    27.0s 
 => => exporting layers                                                                                                                                   18.3s 
 => => exporting manifest sha256:fee564eb723ef2958d8536b9cb813293baa0e6c1e0aba0e7d704c4ee5eef167e                                                          0.0s 
 => => exporting config sha256:df7f89083e45e26bec3a41324082973acafe986537da899cb3c7075aa570f2c3                                                            0.0s 
 => => exporting attestation manifest sha256:cdd94f398d310466fa85e4a851bb083025d6de042b3ae3d7bb6e3f99a9682a42                                              0.0s 
 => => exporting manifest sha256:5ef25730feb795bdb0be8997e5510c9e8cd31c040c67a65db3de8de1039d51d2                                                          0.0s 
 => => exporting config sha256:fc30bdf591b7212bb6a9d104fe31e9e0391c6e5fb918a72b859646a658c41101                                                            0.0s 
 => => exporting attestation manifest sha256:cf7cc9db884308c2f7e9a85385461e272a6faf271c6e0c44103cdee0c7073223                                              0.0s 
 => => exporting manifest list sha256:da5d74e8ba7902f8f37fe84450a6ac2f0bd334dcb7f24db830fb88c995369e51                                                     0.0s
 => => naming to 291615555612.dkr.ecr.us-east-1.amazonaws.com/sigitp-ecr:ubuntu-frr                                                                        0.0s
 => => unpacking to 291615555612.dkr.ecr.us-east-1.amazonaws.com/sigitp-ecr:ubuntu-frr                                                                     2.9s
 => => pushing layers                                                                                                                                      4.2s
 => => pushing manifest for 291615555612.dkr.ecr.us-east-1.amazonaws.com/sigitp-ecr:ubuntu-frr@sha256:da5d74e8ba7902f8f37fe84450a6ac2f0bd334dcb7f24db830f  1.5s
 => [auth] sharing credentials for 291615555612.dkr.ecr.us-east-1.amazonaws.com                                                                            0.0s
 => pushing 291615555612.dkr.ecr.us-east-1.amazonaws.com/sigitp-ecr:ubuntu-frr with docker                                                                 0.7s
 => => pushing layer 77dd9b026404                                                                                                                          0.5s
 => => pushing layer 282bc9c8a685                                                                                                                          0.5s
 => => pushing layer ed8a69e36eb7                                                                                                                          0.5s
 => => pushing layer 0e5fd1281aec                                                                                                                          0.5s
 => => pushing layer 857cc8cb19c0                                                                                                                          0.5s
 => => pushing layer 2eb360eebc72                                                                                                                          0.5s
 => => pushing layer 36732106a133                                                                                                                          0.5s
 => => pushing layer e63ce922f022                                                                                                                          0.5s
 => => pushing layer 89ec9bdced26                                                                                                                          0.5s
 => => pushing layer 2360a3e41d2d                                                                                                                          0.5s
 => => pushing layer 038b6df92bf9                                                                                                                          0.5s
 => => pushing layer 8c4ad779b3bf                                                                                                                          0.5s
 => => pushing layer acdfb06f9bab                                                                                                                          0.5s
 => => pushing layer afd5aeb140f4                                                                                                                          0.5s
Admin:~/environment/ubuntu-frr-dockerfile $
```

### example pod launch on Kubernetes cluster:
```
kubectl apply -f https://raw.githubusercontent.com/sigitp-git/ubuntu-frr-pod/main/ubuntu-frr-pod.yaml
```

### example frr vtysh:
```
Admin:~/environment $ kubectl exec -it ubuntu-frr -- bash
root@ubuntu-frr:~# cd /etc/frr
root@ubuntu-frr:/etc/frr# pwd
/etc/frr
root@ubuntu-frr:/etc/frr# ls -la
total 24
drwxr-x---. 1 frr  frr    21 Aug 22 19:12 .
drwxr-xr-x. 1 root root   17 Aug 22 18:33 ..
-rw-r-----. 1 frr  frr  4129 Aug 22 19:12 daemons
-rw-r-----. 1 frr  frr   489 Aug  3 06:02 frr.conf
-rw-r-----. 1 frr  frr  6663 Aug  3 06:02 support_bundle_commands.conf
-rw-r-----. 1 frr  frr    32 Aug  3 06:02 vtysh.conf

# enable bgpd and bfdd daemons by editing daemons file
root@ubuntu-frr:/etc/frr# vim daemons
bgpd=yes
bfdd=no

# start frr
root@ubuntu-frr:/etc/frr# service frr start
 * Starting watchfrr with command: '  /usr/lib/frr/watchfrr  -d  -F traditional   zebra mgmtd bgpd staticd bfdd'
 * Started watchfrr
root@ubuntu-frr:/etc/frr# vtysh

Hello, this is FRRouting (version 10.1).
Copyright 1996-2005 Kunihiro Ishiguro, et al.

ubuntu-frr# show run
Building configuration...

Current configuration:
!
frr version 10.1
frr defaults traditional
hostname ubuntu-frr
log syslog informational
no ipv6 forwarding
service integrated-vtysh-config
!
end
ubuntu-frr# 
```

### example frr config:
```
export RtrAsn=65000
export FrrAsn=65001
export FrrIp=172.31.147.205
export Rtr1Ip=172.31.201.21
export Rtr2Ip=172.31.202.115
export Prefix1=101.101.101.0/24

sudo -E tee /etc/frr/frr.conf > /dev/null <<EOF 
!
frr version 9.1
frr defaults traditional
hostname frr-vpc-rs-test-router
log syslog debug
no ipv6 forwarding
!
debug bgp neighbor-events
debug bgp updates in
debug bgp updates out
debug bgp zebra
debug bgp bfd
debug bfd distributed
debug bfd peer
debug bfd zebra
debug bfd network
!
router bgp ${FrrAsn}
bgp router-id ${FrrIp}
no bgp default ipv4-unicast
neighbor ${Rtr1Ip} remote-as ${RtrAsn}
neighbor ${Rtr1Ip} bfd
neighbor ${Rtr1Ip} disable-connected-check
neighbor ${Rtr2Ip} remote-as ${RtrAsn}
neighbor ${Rtr2Ip} bfd
neighbor ${Rtr2Ip} disable-connected-check
!
address-family ipv4 unicast
  network ${Prefix1}
  neighbor ${Rtr1Ip} activate
  neighbor ${Rtr1Ip} route-map OUTBOUND out
  neighbor ${Rtr2Ip} activate
  neighbor ${Rtr2Ip} route-map OUTBOUND out
exit-address-family
exit
!
route-map OUTBOUND permit 10
exit
!
bfd
peer ${Rtr1Ip}
peer ${Rtr2Ip}
exit
!
exit
!
end
EOF
```
