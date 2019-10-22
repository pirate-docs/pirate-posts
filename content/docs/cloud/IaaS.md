---
title: "IaaS"
date: 2019-10-17T08:46:46+09:00
bookFlatSection: true
weight: 90
---

# IaaS (Infrastructure as a Service)

## 정의

- 서버, 스토리지, 네트워크를 필요에 따라 인프라 자원을 사용할 수 있게 클라우드 서비스를 제공하는 형태
- 대표적인 기술 : 서버 가상화, 데스크톱 가상화 등 (ex. [하이퍼 바이저 (Hypervisor)]({{< relref "/posts/hypervisor" >}})) 

## 서비스 형태에 따른 구분

<div style="text-align:center" >
    <img src="/static/images/cloud/iaas.png" />
    <div><b>Infrastructure as a Service</b> (출처. <a href="https://developer.ibm.com/kr/cloud/softlayer-bluemix-infra/">IBM Developer</a>)</div>
</div>

#### On-Premise (IDC)

- 소프트웨어 등 솔루션을 클라우드같은 원격 환경이 아닌 자체적으로 보유한 전산실 서버에 직접 설치 및 운영하는 방식 
- 데이터센터 레벨부터 물리적 인프라(서버/스토리지/네트워크), 가상화를 위한 [하이퍼바이저]({{< relref "/posts/hypervisor" >}}) 레벨, 그리고 서버 가상화 솔루션을 통한 가상서버 레벨까지 모두 컨트롤(관리) 가능 

#### Other Cloud Customers

- 일반적인 퍼블릭클라우드 (IaaS)
- 고객은 가상서버 레벨에 대해서만 컨트롤 가능 
    - 장점
        - 데이터센터, 물리적 인프라, [하이퍼바이저]({{< relref "/posts/hypervisor" >}}) 레벨에 대해서 신경쓸 필요없음 
        - 가상서버에 대해서만 관리하면 됨 
    - 단점
        - 가상서버 하위 레벨에 대한 관리 불가
        - 정형화된 [하이퍼바이저]({{< relref "/posts/hypervisor" >}})와 가상 인프라 지원에 대해서만 접근/사용할 수 있음 

#### 하이브리드 방식 (퍼블릭클라우드 + 호스팅)

- 서비스 환경에 따라 On-Premise와 일반적인 퍼블릭클라우드의 장단점을 취하기 위함 
- [베어메탈(bare metal)]({{< relref "/posts/bare-metal" >}}) 클라우드 방식 제공으로, 사용자에게 특정 물리 호스트 전체 제어권을 줄 수 있음 (ex. [IBM softlayer](https://www.ibm.com/kr-ko/cloud/info/softlayer-is-now-ibm-cloud))

### 대표적인 서비스

- [Amazon EC2 (Amazon Elastic Compute Cloud)](https://aws.amazon.com/ko/ec2/)
- [Azure IaaS (Microsoft)](https://azure.microsoft.com/ko-kr/overview/what-is-azure/iaas/)
