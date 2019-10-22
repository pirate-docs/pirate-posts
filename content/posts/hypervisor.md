---
title: "Hypervisor"
date: 2019-10-17T11:04:58+09:00
---

## 하이퍼바이저(Hypervisor)란?

### 의미

- 호스트 컴퓨터 1대에서 다수의 운영체제를 동시에 실행할 수 있도록 해주는 가상 플랫폼
- 가상화머신모니터 또는 가상화머신매니저(Virtual Machine Monitor, Virtual Machine Manager, 줄여서 VMM)라고도 불림

<div style="text-align:center" >
    <img src="/static/images/cloud/hypervisor.png" />
    <div><b>Type-1 and type-2 hypervisors</b> (출처. <a href="https://en.wikipedia.org/wiki/Hypervisor">Wikipedia</a>)</div>
</div>

### 분류
- Type-1 (native, bare-metal)
    - 하이퍼바이저가 하드웨어에서 직접 실행
    - 게스트 운영체제는 하드웨어에서 2번째 수준으로 실행
    - 종류
        - [Xen](https://xenproject.org)
        - [XenServer (Citrix)](https://xenserver.org)
        - [ESX Server (VMware)](https://www.vmware.com/kr/products/vsphere.html)
        - L4 microkernel (ex. [L4 projects](http://www.l4hq.org))
        - TRANGO ([Wikipedia](https://en.wikipedia.org/wiki/Trango_Virtual_Processors))
        - [POWER 하이퍼바이저 (IBM)](https://www.ibm.com/support/knowledgecenter/en/POWER6/iphb2/iphb2hypervisor.htm)
        - [하이퍼-V (Microsoft)](https://docs.microsoft.com/ko-kr/virtualization/hyper-v-on-windows)
- Type-2 (hosted)
    - 호스트 운영체제에서 실행
    - VM 내부에서 동작되는 게스트 운영체제는 하드웨어에서 3번째 수준으로 실행
    - 종류
        - [VMware Server](https://www.vmware.com/kr/products/vcenter-server.html)
        - [VMware Workstation](https://www.vmware.com/kr/products/workstation-pro.html)
        - [VMware Fusion](https://www.vmware.com/kr/products/fusion.html)
        - [QEMU](https://www.qemu.org)
        - [Virtual PC, Virtual Server (Microsoft)](https://azure.microsoft.com/ko-kr/services/virtual-machines)
        - [Virtual Box (Sun)](https://www.virtualbox.org)
        - [Parallels Workstation, Parallels Descktop](https://www.parallels.com/kr/)