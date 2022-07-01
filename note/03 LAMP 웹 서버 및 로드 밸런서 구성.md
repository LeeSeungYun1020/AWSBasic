# LAMP 웹 서버 및 Application Load Balancer 구성

## 개요

클라우드에 Linux에 Apache 웹 서버 MySQL 데이터베이스 PHP 앱을 구성함.

## 사용하는 AWS 서비스

1. Amazon VPC
2. Amazon EC2
3. Amazon EBS
4. Amazon EFS
5. Elastic Laad Balancer - Application Load Balancer 

## 기본 네트워크 환경 구성

1. VPC 생성
   * AWS는 불특정 다수가 사용하는 공용 웹 공간
   * 다른 사용자와 사용하는 네트워크의 분리가 필요
   * DNS Hostname을 enable하여 EC2같은 리소스들이 host name을 생성할 수 있도록 함
2. Subnet 생성
   * VPC의 IP 대역 나눔
   * VPC의 CIDR 대역보다 작아야
3. Internet Gateway 생성
   * 외부 인터넷과 통신 가능하도록 함
   * VPC에 부착 필요
4. Route Table 생성, Route 설정
   * 네트워크간의 통신에 있어서 목적지, 대상지 등으로 데이터 패킷 이동 정보를 구성하는 규칙
   * public subnet은 internet gateway를 통해 외부와의 통신 가능

## Public EC2 인스턴스 생성 및 LAMP 웹서버 구성

1. EC2 생성
    * AMI(Amazon Machine Image)
    * LAMP 웹 서버 구성
    * Security group
    * Storage(EBS)
    * Key pair
2. Index.php 파일 생성
3. 웹 브라우저에서 LAMP 웹 서버 작동 테스트

## Custom AMI를 통한 Public EC2 인스턴스 생성

1. Custom AMI 생성
2. Custom AMI를 이용하여 EC2 추가 생성
3. 웹 브라우저에서 LAMP 웹 서버 작동 테스트

## EFS를 통한 네트워크 파일 시스템 구성

1. EFS(Elastic File System)용 Security group 생성
2. EFS 생성
    * Availability zone
    * Lifecycle
    * Performance/Throughput mode
    * Network
3. EFS를 EC2 인스턴스에 마운트
4. 웹 브라우저를 통한 EFS 마운트 테스트

## Application Load Balancer를 통한 이중화 네트워크 구성

1. 로드 밸런서의 목표가 될 Target group 생성
    * Target Type
    * Protocol/Port
    * Target registration
2. Application Load Balancer 구성
    * Scheme
    * Network
    * Security group
    * Listener, Rule
3. 웹 브라우저로 로드 밸런서 작동 테스트

## Bastion host와 NAT Gateway를 통한 Private EC2 인스턴스의 외부 통신 구성

1. Private subnet에 EC2 생성
2. Public subnet의 EC2를 통해 Private subnet의 EC2에 접속
3. NAT 게이트웨이 생성
4. Route table 설정(트래픽 이동경로 설정)
5. Private subnet의 EC2의 외부 통신 테스트

## Application Load Balancer를 통한 이중화 네트워크 재구성
1. Target group 생성 (private subnet EC2 대상)
2. Application Load Balancer 구성
3. 웹 브라우저를 통한 로드 밸런서 작동 텍스트