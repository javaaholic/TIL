# 리눅스 및 MySQL 설치
목표: 가상머신 환경에 리눅스 및 mysql을 설치한 후 myql에서 host os와 guest os를 연결한다.

## 리눅스 설치 및 설정
[생활코딩](https://opentutorials.org)에 virtualbox, 리눅스, mysql을 설치하는 방법이 자세히 나와 있다.

- VirtualBox 설치
  리눅스를 설치하기에 앞서 먼저 가상머신의 역활을 할 virtualbox를 설치한다. 가상머신에는 대표적으로 vmware와 virtualbox가 있는데 여기서는 virtualbox를 설치한다.

  [다운로드](https://www.virtualbox.org/wiki/Downloads)

- 리눅스 설치
  우분투 데스크탑 버전을 다운로드 받아 설치한다. 설치과정은 간단하므로 생략한다.

  [다운로드](http://www.ubuntu.com/download)

- VirtualBox 네트워크 설정
  host ost와 guest os를 연결하려면 virtualbox에서 네트워크 설정을 해줘야 한다. 설치한 guest os의 네트워크 설정에 들어가서 네트워크 어댑터 사용하기 클릭후 브리지 어댑터를 선택한다.

  - Host-Only - 인터넷 연결 X, host-guest 연결 O
  - NAT - 인터넷 연결 O, host-guest 연결 X
  - 브릿지 - 인터넷 연결 O, host-guest 연결 O

## MySQL 설치 및 설정
우분투 터미널에서 다음 명령어를 입력한다.
```
sudo apt-get install mysql-server mysql-client
```
guest os에 mysql을 설치하고 host os에서 접속하려고 하면 자신의 pc에 mysql을 설치해서 접속할 때 처럼 잘 되지 않는다.

이를 해결하기 위해서는 다음과 같은 설정을 해줘야 한다.
- mysql 권한 설정  
  1. 먼저 mysql db에 관리자 권한으로 로그인하다.
    ```
    mysql -u root -p
    ```
  2. db 변경
    ```
    use mysql;
    ```
  3. 권한 부여
    ```
    GRANT ALL PRIVILEGES ON db.table to 'username'@'host' IDENTIFIED BY 'password';
    ```
    - db.table: 어느 db 어떤 table을 사용하게 할지 설정한다. *.* 로 하면 모든 db의 table에 권한을 주게 된다.
    - username: 연결을 허가할 사용자이름을 입력한다. 새로운 사용자를 만들수도 있다.
    - host: 연결을 허가할 호스트를 입력한다. %로 주게되면 모든 호스트에 연결을 허용한다.
    - password: 비밀번호를 입력한다.
  4. 확인  
    권한 생성이 잘 됬는지 확인할 수 있다.
    ```
    select user, host from user;
    ```

- 외부 접속 주소 설정  
  mysql 설정파일을 열어 다음과 같이 입력한다.
  ```
  $ sudo vi /etc/mysql/my.cnf //관리자 권한으로 설정파일 열기

  //설정파일을 열면 하단에 다음의 내용을 추가한다.
  [mysqld]
  bind-address = 0.0.0.0
  ```
  mysql의 설정이 변경되었으므로 재시작해야 한다.
  ```
  $ sudo /etc/init.d/mysql restart
  ```
  재시작되면 bind-address가 잘 변경되었는지 확인한다.
  ```
  $ mysqld --print-defaults
  ```

- 한글 설정

```
//my.cnf를 열어서 다음의 내용을 추가한다.
sudo vi /etc/mysql/my.cnf

[mysqld]
datadir=/var/lib/mysql
user=mysql
character-set-server=utf8
collation-server=utf8_general_ci
init_connect = set collation_connection = utf8_general_ci
init_connect = set names utf8

[mysql]
default-character-set=utf8

[mysqld_safe]
log-error=/var/log/mysqld.log
pid-file=/var/run/mysqld/mysqld.pid
default-character-set=utf8

[client]
default-character-set=utf8

[mysqldump]
default-character-set=utf8
```

- 테스트  
  마지막으로 host os에서 workbench를 이용해 테스트한다.

## vi 에디터
터미널에서 텍스트를 편집할때 vi에디터를 사용해야 한다. 아래는 간단한 사용법이다.

vi에디터는 3가지 상태를 가진다.

- 편집상태  
  이 상태에서는 입력을 할 수 있다. esc를 누르면 명령대기상태로 돌아간다.

- 명령대기상태  
  여기에서는 입력을 제외한 여러 명령을 할 수 있다. i를 눌러서 커서 위치에서 삽입을 시작한다.

- 명령줄상태  
  저장 및 종료를 할 수 있다. :를 누르고 q를 누르면 종료를 w를 누르면 저장된다. wq를 누르면 저장 및 종료된다.

## 포트포워딩
공유기 설정에 들어가서 외부IP를 입력하면 원하는 내부IP로 설정한 포트를 통해 연결해줄 수 있다.

## 참조
- mysql 설치 및 설정
  - http://powerhan.tistory.com/31
  - http://jaesu.tistory.com/entry/ubuntu-mysql-설치-및-설정하기
  - https://support.rackspace.com/how-to/configuring-mysql-server-on-ubuntu/
- vi 에디터 사용법
  - http://yagi815.tistory.com/146
- virtualbox 네트워크 설정
  - [생활코딩-virtualbox-네트워킹](https://opentutorials.org/course/173/1288)
