---
published: true
title: '[컴퓨터 보안] Access Control'
layout: post
subtitle: 'csReview Computer Security'
categories: csReview
tags: ComputerSecurity
comments: true
---


# Acess Control
자원을 무단으로 사용하는 것을 방지한다.
![Security Functions](https://sundongkim-dev.github.io/assets/img/relationshipAmongAccessControl.jpg)
## Access Control Policies
아래 세 가지 policy들은 상호 배타적이지 않다.
- Mandatory access control policy
- Discretionary access control policy
- Role-based access control policy

### Access control Requirements
+ reliable input
+ support for fine and coarse specifications
+ least privilege
+ open and closed policies
+ separation of duty
+ policy combinations and conflict resolution
+ administrative policies
+ dual control

### Acess Control Basic Elements
- Subject: Object에 접근 가능한 entity
    + 프로세스와 같은 개념
    + Owner, Group, World 세 개의 클래스로 보통 이루어짐
- Object: Resource  
- Access right: Subject가 Object에 접근하는 권리  
  ex) Read, Write, Execute, Delete, Create, Search...  

## Mandatory access controls(MAC)
Mandatory access control(MAC)은 사용자가 소유권에 관계없이 파일에 대한 사용 권한을 정의할 수 없도록 하는 매우 restrictive scheme이다. 대신, security decisions들은 중앙 정책 관리자가 결정한다.   
각 보안 규칙은 당사자를 나타내는 Subject들, 접근 중인 Resource를 참조하는 entity 및 해당 Resource에 접근할 수 있는 범위를 정의하는 등의 권한으로 구성된다.  
대표적인 예시로, Security-Enhanced Linux(SELinux)가 이러한 Mandatory access control을 사용하고 있다.

## Discretionary access controls(DAC)
Discretionary access controls(DAC)는 Entity가 다른 Entity로 하여금 일부 Resource에 접근할 수 있도록 하는 scheme이다.  
종종 Access Matrix를 사용하여 제공된다.  
![Access Matrix](https://sundongkim-dev.github.io/assets/img/accessMatrix.jpg)
그러나 공간을 너무 많이 잡아먹는다는 이유로, 이러한 Linked-List형식의 자료구조로 구현되는 경우도 있다.  
![Linked List ver.](https://sundongkim-dev.github.io/assets/img/linkedListAccessMatrix.jpg)
![Extended Access Matrix](https://sundongkim-dev.github.io/assets/img/extendedAccessMatrix.jpg)

### Access Control Function
![Extended Access Matrix](https://sundongkim-dev.github.io/assets/img/accessControlFunction.jpg)

### Protection Domains
- Object와 그 Object들에 대한 접근 권한의 집합
- Access matrix 관점에서 행은 protection domain이라 할 수 있다.
- 사용자는 사용자 접근 권한의 하위 집합을 사용하여 프로세스를 생성할 수 있다.
  - 프로세스와 도메인 간의 연결은 정적 또는 동적일 수 있다
  - 사용자 모드에서 메모리의 특정 영역은 사용으로부터 보호되고 특정 명령은 실행되지 않을 수 있다.
  - 커널 모드에서 privileged instructions들은 실행될 수 있고 메모리의 보호 영역은 접근될 수 있다.

### Unix File Access control
**UNIX 파일들은 index nodes(i-nodes)로 관리된다.**
+ 특정 파일에 필요한 주요 정보로 제어함
+ 여러 파일 이름은 단일 i-node와 연결될 수 있다
+ 활성된 i-node는 정확히 하나의 파일과 연결된다
+ 파일 속성, 권한과 제어 정보가 i-node에서 정렬된다
+ 디스크에는 i-node table과 i-node list(파일 시스템에 있는 모든 파일의 i-node를 포함)가 있다.
+ 파일을 열 때, 파일의 i-node는 메인 메모리로 가져와 memory resident i-node table에 저장된다.

**Directories들은 계층 트리로 구성된다.**
+ 파일 및 다른 directories들을 포함할 수 있다.
+ 파일 이름과 연결된 i-node에 대한 포인터를 포함한다.

### UNIX file access control
- User ID: 고유 사용자 식별 번호
- Group ID: Primary 그룹의 member를 식별
- 12 Protection bits(파일 소유자, 그룹 구성원 및 기타 모든 사용자에 대한 읽기, 쓰기 및 실행 권한 지정)
- Owner ID, Group ID와 Protection bits는 파일 i-node의 일부이다.
![UNIX File Access Control](https://sundongkim-dev.github.io/assets/img/UNIXFileAccess.jpg)

### Traditional UNIX File Access control
+ set user ID (SetUID)
+ set group ID (SetGID)
  + 권한 있는 프로그램이 일반적으로 액세스할 수 없는 파일/자원에 액세스할 수 있도록 한다.

+ sticky bit
  + 디렉토리에 적용될 때, 디렉토리에 있는 파일의 소유자만 해당 파일의 이름 변경, 이동 또는 삭제할 수 있도록 지정한다.
+ superuser
  + 일반적인 접근 제어 제한에서 자유로움

## Role-Based Access Control(RBAC)
User와 Resource사이에 Role(역할)을 만들어 그 역할들을 통해 자원에 접근하게 끔 하는 방식이다. 이 또한 Access Control Matrix가 있는데 다음과 같다.  
![RBAC Access Matrix](https://sundongkim-dev.github.io/assets/img/RBACaccessMatrix.jpg)
위와 같이 유저들은 우선 역할을 배정받고, 그 역할들은 각각 어떤 Object에 어떤 권한이 있는 지를 나타낸다.  

**Constraints**
1. Mutually Exclusive Roles
  + 사용자는 하나의 집합의 한 Role에만 할당될 수 있다.
  + 집합의 한 Role에만 모든 권한(액세스 권한)을 부여할 수 있다.  
2. Cardinality
  + Role에 대한 최대 수 설정
3. Prerequisite Roles
  + 다른 역할에 이미 할당된 사용자만이 특정 역할에 할당할 수 있도록 지정한다.

### NIST RBAC model
![NIST RBAC model](https://sundongkim-dev.github.io/assets/img/NIST_RBACmodel.jpg)
- Object: 접근 제어의 대상인 시스템 리소스(파일, 프린터, 터미널, 데이터베이스 레코드 등)
- Operation: 프로그램의 실행 가능한 이미지, 호출 시 사용자에게 일부 기능을 실행한다
- Permission: 하나 이상의 RBAC 보호 개체에 대한 작업 수행 승인

### Core RBAC
+ Administrative Functions
  + 사용자 집합에서 사용자 추가 및 삭제
  + 역할 집합에서 역할 추가 및 삭제
  + 역할 할당에 대한 사용자 인스턴스 생성 및 삭제
  + 역할 할당 권한 인스턴스 생성 및 삭제

+ Supporting System Functions
  + 사용자 세션 만들기
  + 세션에 active role을 추가
  + 세션에서 역할을 삭제
  + 세션 Subject에 요청된 Operation을 수행할 수 있는 권한이 있는지 확인

+ Review Functions
  + 관리자가 모델 및 모델의 모든 요소를 볼 수는 있지만 수정할 수는 없음

### Hierarchical RBAC
+ General Role Hierarchies
+ Limited Role Hierarchies

**Static Separation of Duty Relations(SSD)**
+ 사용자가 집합의 한 역할에 할당된 경우, 사용자가 집합의 다른 역할에 할당되지 않도록 상호 배타적인 역할 집합을 정의할 수 있다
+ 역할 집합에 Cardinality 제약 조건을 둘 수 있음
+ 역할 집합에서 n개 이상의 역할에 사용자가 할당되지 않는 쌍(역할 집합, n)으로 정의
+ 역할 집합을 만들고 삭제하고 역할 구성원을 추가 및 삭제하는 관리 기능을 포함한다
+ 기존 SSD 집합의 속성을 보기 위한 Review functions를 포함한다

**Dynamic Separation of Duty Relations(DSD)**
+ 사용자에게 사용 가능한 권한을 제한함
+ 사용자 세션 내 또는 세션 간에 활성화될 수 있는 역할에 대한 제약 조건 설정  
+ 제약 조건을 쌍(역할 집합, n)으로 정의한다. 여기서 n은 2이하의 자연수로, 어떤 사용자 세션도 역할 집합에서 n개 이상의 역할을 활성화할 수 없는 속성을 가진다.  
+ 관리자가 서로 다른 중복되지 않는 시간에 사용자에 대한 특정 기능을 지정할 수 있다.  
+ DSD 관계를 정의하고 보기 위한 Administrative & Review ffunctions를 포함한다

## Attribute-based Access control(ABAC)
- 속성들을 결합하는 정책을 기반으로 한다
  + 사용자 속성, 리소스 속성, 환경 속성 등
  + 나이, 역할, 직업명, ... / 읽기, 삭제, 보기, ...
- 다른 속성을 evaluate할 수 있는 복잡한 boolean 규칙 집합을 표현할 수 있다.
