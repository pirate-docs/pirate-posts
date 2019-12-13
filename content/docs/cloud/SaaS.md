---
title: "SaaS"
date: 2019-10-17T08:44:35+09:00
bookFlatSection: true
draft: false
weight: 100
---

# SaaS (Software as a Service)

## 정의

- 클라우드 환경에서 동작하는 응용프로그램을 서비스 형태로 제공하는 것 
- 주문형 소프트웨어(on-demand software)라고도 불림

<div style="text-align:center" >
    <img src="/static/images/cloud/saas.png" />
    <div><b>Software as a Service</b> (출처. <a href="https://blog.v-comply.com/saas-platform/">v-comply</a>)</div>
</div>

## 특징

- 네트워크 기반으로 접근하고 관리하는, 상업적으로 사용 가능한 소프트웨어
- 사용자가 웹을 통해 애플리케이션에 접근하고, 중앙에서 활동 관리 
- 1:N 모델(single instance, multi-tenant)에 가까움 (아키텍처, 가격, 파트너링, 관리 등이 포함)

### 장점 

- 퍼블릭 클라우드에 있는 소프트웨어를 웹을 통해 언제 어디서나 사용할 수 있음 
- 네트워크를 통해 서비스되므로 사용하기 쉽고, 최신 소프트웨어 업데이트를 빠르게 제공받을 수 있음 

### 단점

- 데이터 처리 및 보관이 외부 클라우드 서비스에서 이루어지기 때문에 데이터 노출의 위험이 있을 수 있음
- 인터넷을 통해 접속 가능하므로, 인프라가 외부와 단절되어 있거나 통신 환경이 열악한 곳에서는 이용할 수 없음 

## 서비스 형태

### 로그인 타입

- 아이디와 패스워드를 부여받고 홈페이지 통해 서비스를 이용하는 형태 
- 별도의 설치 시간이 필요없고, 누구나 빠르게 서비스에 접근할 수 있음 
- 대표적인 사례 : Google Apps, MS office 365, 더존 클라우드팩스, 한컴 넷피스24 등 

### API 타입 

- 퍼블릭 클라우드 속에 설치되어있는 소프트웨어 패키지를 api로 제공받아, 기업서버([ERP]({{< relref "/posts/erp" >}}))에 적용해서 서비스를 이용하는 형태
- 기업의 [ERP]({{< relref "/posts/erp" >}}) 또는 [CRM]({{< relref "/posts/crm" >}})과의 연동성이 관건 
- API 타입은 특정 시스템과의 연동이 반드시 필요하기 때문에 일반 사용자용으로 제공하지 않음 
 
## 대표적인 서비스 

- [Gmail](https://mail.google.com/)
- [Google Apps](https://apps.google.com)  