# devops-project

## 목차

- [01. Vagrant + VM(VirtualBox)](#01-vagrant--vmvirtualbox)
- [02. AWS Cloud for Web App Setup [Lift & Shift]](#02-aws-cloud-for-web-app-setup-lift-and-shift)

## 01. Vagrant + VM(VirtualBox)

<details>
<summary><b>접기/펼치기</b></summary>

### 🖍 Provisioning(프로비저닝)

"프로비저닝"이란 IT 인프라의 설정과 관리를 위한 프로세스를 말합니다. 이 과정은 소프트웨어 설치, 구성, 실행을 포함하며, 이러한 작업들은 수동으로 수행될 수 있지만 자동화된 툴을 통해 진행될 수도 있습니다.

#### 🕯 수동

vagrant file을 이용하여. VM생성, OS설치

[Manual Provisioning](<01.Vagrant+VM(VirtualBox)/Manual_Provisioning>)

#### 🔦 자동

vagrant file과 shellscript를 이용하여 VM생성, OS설치, APP설치, 설정을 자동화

[Automated Provisioning](<01.Vagrant+VM(VirtualBox)/Automated_Provisioning>)

### 🏗 설계

![이미지](img/01.vagrant+virtualbox.jpg)

### ⛳️ 검증

<details>
<summary>접기/펼치기</summary>

![이미지](img/validate/01/01-1.png)
![이미지](img/validate/01/01-2.png)

</details>

### 📃 출처

#### 소스코드

- [devopshydclub/vprofile-project](https://github.com/devopshydclub/vprofile-project)

#### 내용

- [Udemy - DevOps Projects | 20 Real Time DevOps Projects](https://www.udemy.com/course/devopsprojects/)

### 🛠 스택

<p align="left">
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/mysql/mysql-original-wordmark.svg" alt="mysql" width="40" height="40"/>
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/nginx/nginx-original.svg" alt="nginx" width="40" height="40"/>
   <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/tomcat/tomcat-original.svg" alt="tomcat" width="40" height="40"/>
   <img src="img/stacklogo/rabbit mq.png" alt="rabbitMQ"  height="40"/>
   <img src="img/stacklogo/memcached.png" alt="memcached" height="40"/>
</p>

</details>

## 02. AWS Cloud for Web App Setup [Lift & Shift]

<details>
<summary><b>접기/펼치기</b></summary>

이 프로젝트는 AWS 클라우드 컴퓨팅 프로젝트로, "리프트 앤 시프트 전략"을 사용해 AWS 클라우드로 애플리케이션을 이동하는 것을 목표로합니다.

### 🖍 Lift & Shift (리프트 앤 시프트)

"리프트 앤 시프트"는 기존의 온-프레미스 시스템을 클라우드로 그대로 이전하는 전략입니다.
이것은 "클라우드 마이그레이션"또는 "애플리케이션 재호스팅"이라고도 불립니다. 이 전략의 주요 목표는 클라우드의 이점을 신속하게 활용하면서 애플리케이션 코드나 데이터를 거의 변경하지 않는 것입니다.

### 🏗 설계

01에서 사용했던 스크립트를 이용하여, 리프트 앤 시프트 전략을 사용해 AWS 클라우드로 프로비저닝합니다.  
MySQL, RabbitMQ, Memcached를 하나의 보안 그룹으로 묶어 각각 인스턴스에 프로비저닝하고, Route 53을 이용해, 각각의 private IP를 이름으로 매핑합니다.  
app01 인스턴스를 생성하고, tomcat을 설치 후 s3를 이용해 어플리케이션 배포 파일을 받아와. tomcat9으로 구동시킵니다. 이때 tomcat의 application.properties를 수정하여, Route53으로 매핑한 이름으로 설정을 수정해줍니다. app 인스턴스를 타겟으로 로드밸런서를 생성하고, 오토스케일링 설정을 통해, 인스턴스 종료 시 시작 구성을 이용해 자동생성되게 합니다.(현재 AWS는 시작 구성을 추천하지 않고, 시작 템플릿을 권장합니다.)

**요약**

1. 키 쌍 생성 : EC2 인스턴스에 로그인하기 위한 키 쌍을 생성.
2. 보안 그룹 생성 : 로드 밸런서, 톰캣, 백엔드 서비스들을 위한 보안 그룹을 설정
3. 인스턴스 시작 : 사용자 데이터를 포함한 인스턴스를 시작. 사용자 데이터는 01 프로젝트에서 사용한 shell script를 사용합니다.
4. IP-이름 매핑 : Route53에서 IP를 이름으로 매핑함.
5. 로드 밸런서 설정 : HTTPS 연결을 사용하는 로드 밸런서를 설정.
6. DNS 매핑: GoDaddy DNS에서 웹사이트를 가리키는 엔드포인트를 로드 밸런서에 매핑.
7. 오토스케일링 그룹 구성 : 톰캣 인스턴스에 대한 오토 스케일링 그룹을 구성

![이미지](img/02.aws+cloud+setup.jpg)

### ⛳️ 검증

<details>
<summary>보안그룹</summary>

![이미지](img/validate/02/보안그룹.png)

</details>

<details>
<summary>백앤드 보안그룹</summary>

![이미지](img/validate/02/백엔드SG.png)

</details>

<details>
<summary>어플리케이션 보안그룹</summary>

![이미지](img/validate/02/APP-SG.png)

</details>

<details>
<summary>로드밸런서 보안그룹</summary>

![이미지](img/validate/02/로드밸런서SG.png)

</details>

<details>
<summary>생성된 인스턴스들</summary>

![이미지](img/validate/02/생성된인스턴스들.png)

</details>

<details>
<summary>Route53-IP-매핑</summary>

![이미지](img/validate/02/Route53-IP-매핑.png)

</details>

<details>
<summary>오토스케일링 그룹</summary>

![이미지](img/validate/02/오토스케일링그룹.png)

</details>

<details>
<summary>톰캣 설정</summary>

```sh
#JDBC Configutation for Database Connection
jdbc.driverClassName=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://db01.vprofile.in:3306/accounts?useUnicode=true&characterEncoding=UTF-8&zeroDateTimeBehavior=convertToNull
jdbc.username=
jdbc.password=

#Memcached Configuration For Active and StandBy Host
#For Active Host
memcached.active.host=mc01.vprofile.in
memcached.active.port=11211
#For StandBy Host
memcached.standBy.host=
memcached.standBy.port=11211

#RabbitMq Configuration
rabbitmq.address=rmq01.vprofile.in
rabbitmq.port=5672
rabbitmq.username=test
rabbitmq.password=test

#Elasticesearch Configuration
elasticsearch.host =
elasticsearch.port =9300
elasticsearch.cluster=vprofile
elasticsearch.node=vprofilenode
```

</details>

### 📃 출처

#### 소스코드

- [devopshydclub/vprofile-project](https://github.com/devopshydclub/vprofile-project)

#### 내용

- [Udemy - DevOps Projects | 20 Real Time DevOps Projects](https://www.udemy.com/course/devopsprojects/)

### 🛠 스택

#### OS

<p align="left">
<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/centos/centos-original.svg" alt="centos" height="40"/>
<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/ubuntu/ubuntu-plain-wordmark.svg" alt="ubuntu" height="40"/>
</p>

#### AWS

<p align="left">
<img src="https://d2q66yyjeovezo.cloudfront.net/icon/d88319dfa5d204f019b4284149886c59-7d586ea82f792b61a8c87de60565133d.svg" alt="aws" height="40"/>
<img src="https://d2q66yyjeovezo.cloudfront.net/icon/f5d2c00d40914bff4f82f29f9ef768bc-53a84099cf556710383a52b4612a8612.svg" alt="aws" height="40"/>
<img src="https://d2q66yyjeovezo.cloudfront.net/icon/02b55e4f52388520bfe11f959f836e68-b8cdde73b02af863b91a2296bbd10b4c.svg" alt="aws" height="40"/>
<img src="https://d2q66yyjeovezo.cloudfront.net/icon/c0828e0381730befd1f7a025057c74fb-43acc0496e64afba82dbc9ab774dc622.svg" alt="aws" height="40"/>
<img src="https://d2q66yyjeovezo.cloudfront.net/icon/0ebc580ae6450fce8762fad1bff32e7b-0841c1f0e7c5788b88d07a7dbcaceb6e.svg" alt="aws" height="40"/>

</p>

#### APP

<p align="left">
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/mysql/mysql-original-wordmark.svg" alt="mysql" width="40" height="40"/>
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/nginx/nginx-original.svg" alt="nginx" width="40" height="40"/>
   <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/tomcat/tomcat-original.svg" alt="tomcat" width="40" height="40"/>
   <img src="img/stacklogo/rabbit mq.png" alt="rabbitMQ"  height="40"/>
   <img src="img/stacklogo/memcached.png" alt="memcached" height="40"/>
</p>

</details>
