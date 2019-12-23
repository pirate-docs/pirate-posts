---
title: "Components"
date: 2019-12-23T13:59:56+09:00
draft: false
weight: 100
---

# 컴포넌트 

<div style="text-align:center" >
    <img src="/static/images/kubernetes/clusterdiagram.png" />
    <div><b>쿠버네티스 클러스터 다이어그램</b> (출처. <a href="https://kubernetes.io/ko/docs/concepts/overview/components/">Components</a>)</div>
</div>

## 마스터 컴포넌트 

> 클러스터의 컨트롤 플레인 제공  
> 클러스터의 전반적인 결정을 수행하고, 이벤트 감지 및 반응함   
> 클러스터 내 어떤 머신에서든지 동작될 수 있음 

### kube-apiserver

- 쿠버네티스 api를 노출하는 컨트롤 플레인 컴포넌트
- 여러 kube-apiserver 인스턴스 실행을 통해, 트래픽을 균형있게 조절할 수 있음 

### etcd 

- 모든 클러스터 데이터를 담는 쿠버네티스 백단의 저장소로 사용 (일관성, 고가용성 키-값 저장소)
- etcd 사용시 백업 계획은 필수로 해야함  
(참고. [etcd 공식문서](https://github.com/etcd-io/etcd/blob/master/Documentation/docs.md))
 
### kube-scheduler
 
- 노드가 배정안된 새로운 파드를 감지하고, 그것이 구동될 노드를 선택하는 마스터 상의 컴포넌트 
- 스케줄링 결정시 고려되는 요소
    - 리소스의 개별 및 총체적 요구 사항
    - 하드웨어/소프트웨어/정책적 제약 
    - 어피니티 및 안티-어피니티 명세
    - 데이터 지역성
    - 워크로드 간의 간섭 
    - 데드라인 
    
### kube-controller-manager

- 컨트롤러를 구동하는 마스터 상의 컴포넌트 
- 컨트롤러 포함사항 
    - 노트 컨트롤러 : 노드가 다운되었을 때 통지와 대응에 관한 책임을 가짐 
    - 레플리케이션 컨트롤러 : 적당한 수의 파드를 유지시켜주는 책임을 가짐 
    - 엔드포인트 컨트롤러 : 서비스와 파드를 연결시킴 
    - 서비스 어카운트 & 토큰 컨트롤러 : 새로운 네임스페이스의 기본 계정과 api 접근 토큰 생성

### cloud-controller-manager

- 클라우드 제공사업자오아 상호작용하는 컨트롤러를 작동시킴 
- 클라우드 밴더 코드와 쿠버네티스 코드가 서로 독립적으로 발전할 수 있도록 해줌 
- 참고. 클라우드 제공사업자의 의존성을 갖는 컨트롤러
    - 노드 컨트롤러 : 노드가 멈추고, 클라우드 상에서 삭제되었는지 확인하는 것
    - 라우트 컨트롤러 : 바탕을 이루는 클라우드 인프라에 경로를 구성하는 것
    - 서비스 컨트롤러 : 클라우드 제공사업자 로드밸런서 생성, 업데이트 및 삭제하는 것 
    - 볼륨 컨트롤러 : 볼륨의 생성, 부착, 마운트하는 것과 볼륨 조절을 위해 상호작용하는 것 

## 노드 컴포넌트 

> 동작 중인 파드를 유지시키고, 쿠버네티스 런타임 환경을 제공  
> 모든 노드 상에서 동작하는 컴포넌트 

### kubelet

- 클러스터 각 노드에서 실행되는 에이전트 
- 파드에서 컨테이너가 확실하게 동작하도록 관리함 
- 파드 스펙(PodSpec)의 집합을 받아서 컨테이너가 해당 파드 스펙에 따라 동작하도록 함 

### kube-proxy

- 클러스터의 각 노드에서 실행되는 네트워크 프록시 
- 쿠버네티스의 서비스 개념의 구현부 
- 노드의 네트워크 규칙을 유지 관리함 (내부 네트워크 세션 관리 및 클러스터 바깥의 파드와의 통신)

### container runtime

- 컨테이너 실행을 담당하는 소프트웨어   
ex. [docker](https://www.docker.com/), [containerd](https://containerd.io/), [cri-o](https://cri-o.io/), [rktlet](https://github.com/kubernetes-retired/rktlet) 과 같은 
[컨테이너 런타임 인터페이스](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-node/container-runtime-interface.md)를 구현한 모든 소프트웨어  

## 애드온 

> 쿠버네티스 리소스를 이용해서 클러스터 기능을 구현함  
> 클러스터 단위의 기능을 제공하므로, 네임스페이스 리소스는 `kube-system`에 속함 

### DNS

- 구성환경 내 다른 DNS 서버와 더불어, 쿠버네티스 서비스를 위해 DNS 레코드를 제공해줌 
- 쿠버네티스에 의해 구동되는 컨테이너는 DNS 서버를 자동으로 포함함 

### 웹 UI (대시보드)

- 쿠버네티스 클러스터를 위한 범용의 웹 기반 ui
- 클러스터에서 동작하는 애플리케이션에 대한 관리와 고장처리를 할 수 있도록 해줌 

### 컨테이너 리소스 모니터링

- 중앙 데이터베이스 내에 컨테이너들에 대해 기록
- 기록한 데이터를 열람하기 위한 ui 제공 

### 클러스터-레벨 로깅 

- 검색/열람 인터페이스와 함께 중앙 로그 저장소에 컨테이너 로그 저장 

## 관련링크
- [Kubernetes](https://kubernetes.io/)
- [Kubernetes components](https://kubernetes.io/ko/docs/concepts/overview/components/)

