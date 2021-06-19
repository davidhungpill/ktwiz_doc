# AWS 접속 정보



## SSH 접속

AWS 서버에는 Putty 혹은 MobaXTerm 을 사용하여 SSH 접속이 가능

다음 링크에서 mobaXterm 다운 가능 (https://mobaxterm.mobatek.net/download.html)

### WEB(서버1번) 서버 접속 정보

web(서버1번)은 AWS의 public subnet에 있으므로 아래 정보로 SSH 접속이 가능하다.

- public IP : 3.36.248.102

- port : 22

- 도메인 : ec2-3-36-248-102.ap-northeast-2.compute.amazonaws.com

- ID : centos

(비번 및 인증서는 slack으로 공유 하겠습니다.)

![image-20210619165544343](C:\Users\david\AppData\Roaming\Typora\typora-user-images\image-20210619165544343.png)



위와 같이 host, username, port 그리고 인증키를 저장하여 지정하면 접속이 가능합니다.

루트 계정 접속을 위해서는 명령창에서 su - root 하면 됩니다. (비번은 slack으로 공유할게요)



### WAS(서버2번) 서버 접속

WAS 서버는 private subnet에 있어서 직접 접속은 안됩니다.

대신 위의 WEB (서버 1번)에 SSH로 접속후 아래 명령어로 통해 접속 가능합니다.

 ssh -i "ec2_key_pair1.pem" centos@10.0.5.33 



### DB 접속

DB 도 Private subnet에 있어서 직접 접속은 안됩니다.

접속을 위해서는 SSH 터널링을 이용해야 합니다.

먼저 아래 링크에서 pgadmin4를 다운받아서 설치합니다.

(https://www.pgadmin.org/download/pgadmin-4-windows/)

설치후에 바로가기가 생성되지 않으므로 C:\Program Files\pgAdmin 4\v5\runtime\pgAdmin4.exe 를 직접 실행해 주셔야 할거에요.

실행 후  아래 정보로 접속이 가능합니다.

- Public DNS : ktds-db2.cznz2ugarinh.ap-northeast-2.rds.amazonaws.compgAdmin4.exe
- Port : 5432
- ID : postgres
- pw : Test8080!

그리고 SSH 터널링을 위해 아래 정보 설정도 필요합니다.

- USE SSH Tunnel : Yes
- Tunnel host : 3.36.248.102
- Tunnel post : 22
- Username : centos
- authentication : identify file (파일을 slack으로 공유할 pem 파일 선택)

![image-20210619171632599](C:\Users\david\AppData\Roaming\Typora\typora-user-images\image-20210619171632599.png)

![image-20210619171655292](C:\Users\david\AppData\Roaming\Typora\typora-user-images\image-20210619171655292.png)

위와 같이 설정하면 SSH로 WEB(서버1번)에 접속한 상태에서만 pgadmin을 통한 접속이 가능합니다.





