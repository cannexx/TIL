# CentOS 7에 Maven 설치

- 환경
  - OpenJDK 1.8
- 2020/03/21 기준 yum에서 maven 설치시 3.0.5가 설치되므로 다른 방법으로 설치
  - Maven 3.6 Download
    - `wget http://apache.mirror.cdnetworks.com/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz -P /tmp`
  - 압축해제
    - `tar xvf apache-maven-3.6.3-bin.tar.gz -C /usr/lib`
  - 환경변수 설정
    - `vi /etc/profile`
      - MAVEN_HOME=/usr/lib/apache-maven-3.6.3
      - PATH=$PATH:$MAVEN_HOME/bin
    - `source /etc/profile`
  - 설정 확인
    - `mvn -version`