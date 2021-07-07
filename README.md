# Overview

Jenkins, gitlab을 Docker 컨테이너로 구축하고 CI/CD 기능을 구현한다. 최종적으로 docker를 사용한 Node.js, Spring boot CI/CD 환경 구축을 목표로 한다. 해당 과정은 VirtualBox의 우분투 이미지를 활용하여 작성하였다.

# Version

OS : Ubuntu 18.04.5 LTS

Image : Jenkins/jenkins:lts, gitlab-ce, openjdk:8-jdk

project : spring-boot

# Section 1 : install docker-compose & start

## install docker-compose

```{.bash}
$ sudo curl -L https://github.com/docker/compose/releases/download/1.26.2/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose

$ docker-compose --version
```

## start up docker-compose

```{.bash}
$ docker-compose up --build -d
```

# Section 2 : config ssh

## publish ssh-keygen in jenkins container

host에 있는 컨테이너를 새로 띄우기 위하여 jenkins 컨테이너와 host간 ssh 공개키를 등록한다. jenkins 컨테이너의 id_rsa.pub 내용을 복사하여 host의 authorized_keys 파일에 붙여넣는다.

```
$ docker exec -it jenkins-compose bash

### Jenkins Container
$ ssh-keygen -t rsa
$ exit

### Host
$ cat '<jenkins-container-primaryKey>' >> /home/ban/.ssh/authorized_key
```

## deploy script test

```{.bash}
$ docker exec -it jenkins-compose bash

### Jenkins 컨테이너에서 호스트로 ssh 명령 테스트
$ ssh [유저이름]@$(/sbin/ip route | awk '/default/ { print $3 }')<<EOF
> cd /home/ban/jenkins
> docker-compose up --build -d
> exit
> EOF
```

# Section 3 : config build trigger in jenkins

# Reference

[https://smoh.tistory.com/333](https://smoh.tistory.com/333)

[https://skyblue300a.tistory.com/14](https://skyblue300a.tistory.com/14)

[https://velog.io/@sdg9670/Dockerizing-a-Node.js](https://velog.io/@sdg9670/Dockerizing-a-Node.js)

[https://waspro.tistory.com/554](https://waspro.tistory.com/554)
