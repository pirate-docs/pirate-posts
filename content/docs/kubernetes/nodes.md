---
title: "Nodes"
date: 2019-12-23T16:10:38+09:00
draft: false
weight: 100
---

# 노드 

> 쿠버네티스에서 하나의 워커 머신 
> 클러스터에 따라, VM 또는 물리 머신이 될 수 있음 
> 파드를 동작시키기 위해 필요한 서비스를 포함하며 마스터 컴포넌트에 의해 관리됨 

## 노드 상태 

- 포함 요소 
    - [주소](#주소)
    - [컨디션](#컨디션)
    - [용량](#용량)
    - [정보](#정보) 
- 노드 상태 및 상세 정보 확인 방법  
```
    kubectl describe node <insert-node-name-here>
```

### 주소 

- HostName : 노드 커널에 의해 알려진 호스트명 
- ExternalIP : 클러스터 외부에서 이용 가능한 ip 주소 
- InternalIP : 클러스터 내에서만 라우트 가능한 주소 

### 컨디션 

| Node Condition | Description |
|---|---|
| Ready | *True* : 노드 양호 (파드 수용 가능 상태) <br /> *False* : 노드 상태 불량 (파드를 수용 못할 경우) <br /> *Unknown* : 노드로부터 응답을 받지 못한 경 |
| MemoryPressure | *True* : 노드 메모리가 넉넉하지 않은 경우 (반대의 경우, *False*) |
| PIDPressure | *True* : 노드 상에 많은 프로세스들이 존재하는 경우 (반대의 경우, *False*) |
| DiskPressure | *True* : 디스크 용량이 넉넉하지 않은 경우 (반대의 경우, *False*) |
| NetworkUnavailable | *True* : 네트워크가 올바르게 구성되지 않은 경우 (반대의 경우, *False*) |

- 노드 컨디션 표현 (json)

```json
{
        "conditions": [{
             "type": "Ready",
             "status": "True",
             "reason": "KubeletReady",
             "message": "kubelet is posting ready status",
             "lastHeartbeatTime": "2019-06-05T18:38:35Z",
             "lastTransitionTime": "2019-06-05T11:41:27Z"
        }]
}
```

### 용량

- 노드 상에서 사용 가능한 리소스 (CPU, 메모리, 스케줄 가능한 최대 파드 수 등)
- 용량 블록 : 노드에 있는 리소스 총량을 나타냄 

### 정보 

- 커널 버전, 쿠버네티스 버전 (kubelet, kube-proxy 버전) 등 일반적인 정보 제공 
- Kubelet을 통해 노드로부터 수집됨 

## 관리 

- 노드는 쿠버네티스에 의해 생성되지 않음 
- 클라우드 제공사업자에 의해 외부로부터 생성되거나, 물리적 또는 가상 머신의 풀 내에서 존재함 
- 쿠버네티스 노드 인터페이스와 상호작용하는 3개 컴포넌트
    - 노드 컨트롤러
    - kubelet
    - kubectl

### 노드 컨트롤러

- 노드의 다양한 측면을 관리하는 쿠버네티스 마스터 컴포넌트 
- 역할 
    1. 등록 시점에 노드에 CIDR 블럭 할당 
    2. 내부 노드 리스트를 최신상태로 유지 
    3. 노드의 동작 상태 모니터링 

### 노드의 Self-Registration

- kubelet 플래그(`--register-node`)가 *True*(기본값)일 경우, api 서버에 스스로 등록 시도 
- Self-Registration에 대해, kubelet은 아래 옵션과 함께 시작됨
    - `--kubeconfig` : apiserver에 스스로 인증하기 위한 자격증명의 경로 
    - `--cloud-provider` : 메타데이터를 읽기 위해, 클라우드 제공사업자와 소통할지에 대한 방법
    - `--register-node` : 자동으로 api 서버에 등록 
    - `--register-with-taints` : taint 리스트 (`<key>=<value>:<effect>`)
    - `--node-ip` : 노드의 ip 주소
    - `--node-labels` : 클러스터 내 노드를 등록할 경우 추가되는 레이블 
    - `--node-status-update-frequency` : kubelet이 마스터에 노드 상태를 게시하는 빈도 
- `--register-node=false`로 설정할 경우, 관리자가 수동으로 노드 오브젝트 생성/관리 

### 노드 용량 

- 노드의 용량(cpu 수와 메모리 양)은 노드 오브젝트의 한 부분 
- (일반적으로) 노드는 스스로 등록하고 노드 오브젝트 생성시 자신의 용량을 알림  
  수동으로 노드를 관리한다면, 노드 추가할ㄹ때 노드 용량을 설정해야 함 

## 관련링크
- [Kubernetes](https://kubernetes.io/)
- [Kubernetes nodes](https://kubernetes.io/ko/docs/concepts/architecture/nodes/)

