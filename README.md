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
## publish ssh-keygen in boot container
```

```

# Reference
[https://smoh.tistory.com/333](https://smoh.tistory.com/333)

[https://skyblue300a.tistory.com/14](https://skyblue300a.tistory.com/14)

[https://velog.io/@sdg9670/Dockerizing-a-Node.js](https://velog.io/@sdg9670/Dockerizing-a-Node.js)

[https://waspro.tistory.com/554](https://waspro.tistory.com/554)
