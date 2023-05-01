# devops-project

## 목차

- [01. Vagrant + VM(VirtualBox)](#01-vagrant--vmvirtualbox)
  - [Provisioning(프로비저닝)](#provisioning프로비저닝)
    - [수동](#수동)
    - [자동](#자동)
  - [출처](#출처)
    - [소스코드](#소스코드)
    - [내용](#내용)
  - [스택](#스택)

## 01. Vagrant + VM(VirtualBox)

<details>
<summary><b>접기/펼치기</b></summary>

### Provisioning(프로비저닝)

"프로비저닝"이란 IT 인프라의 설정과 관리를 위한 프로세스를 말합니다. 이 과정은 소프트웨어 설치, 구성, 실행을 포함하며, 이러한 작업들은 수동으로 수행될 수 있지만 자동화된 툴을 통해 진행될 수도 있습니다.

#### 수동

vagrant file을 이용하여. VM생성, OS설치

[Manual Provisioning](<01.Vagrant+VM(VirtualBox)/Manual_Provisioning>)

#### 자동

vagrant file과 shellscript를 이용하여 VM생성, OS설치, APP설치, 설정을 자동화

[Automated Provisioning](<01.Vagrant+VM(VirtualBox)/Automated_Provisioning>)

### 설계

![이미지](img/01.vagrant+virtualbox.jpg)

### 출처

#### 소스코드

- [devopshydclub/vprofile-project](https://github.com/devopshydclub/vprofile-project)

#### 내용

- [Udemy - DevOps Projects | 20 Real Time DevOps Projects](https://www.udemy.com/course/devopsprojects/)

### 스택

<p align="left">
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/mysql/mysql-original-wordmark.svg" alt="mysql" width="40" height="40"/>
  <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/nginx/nginx-original.svg" alt="nginx" width="40" height="40"/>
   <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/tomcat/tomcat-original.svg" alt="tomcat" width="40" height="40"/>
   <img src="img/stacklogo/rabbit mq.png" alt="rabbitMQ"  height="40"/>
   <img src="img/stacklogo/memcached.png" alt="memcached" height="40"/>
</p>

</details>
