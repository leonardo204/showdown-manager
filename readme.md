# Showdown Web Manager
iodides님이 제작하신 Showdown을 Web에서 관리할 수 있도록 제작

## 제작 및 구동 환경
 * Synology DSM 6.0
 * Java8
 * Nginx
 * PHP 7.0(5.6+)
 * Kiaalap Template : https://github.com/puikinsh/kiaalap
 * Showdown v1.51 : https://iodides.tistory.com/7
 
## 설치 방법 by Synology DSM 6.0
 ```
    * 혹시 모를 오동작및 DB 오류를 위해 반드시 SQLDB.db를 백업후 진행해 주세요.
    * 문제 발생시 백업한 DB를 이용해 복구가 가능합니다.
     
    1. DB백업을 위해 Showdown 프로세스 Kill 
        $ kill -9 `ps -ef | grep 'Server.jar' | awk '{print $2}'`
        
    2. Showdown 설치 디렉토리에 권한 할당
        http : 읽기/쓰기
 
    3. Showdown 디렉토리의 SQLDB.db 파일 백업
        $ cp -rfp SQLDB.db SQLDB.db.backup

    4. Showdown 디렉토리의 SQLDB.db에 권한 할당
        http : 읽기/쓰기

    5. Showdown 디렉토리의 Client.jar 파일에 권한 할당
        http : 읽기/쓰기
    
    6. Showdown Manager 설치 디렉토리에 권한 할당
        http : 읽기
    
    7. Synology Web Station 설정
        Nginx + PHP 7.0 or 5.6 + PHP 확장 에서 pdo_sqlite 체크

    8. JAVA8 설치 디렉토리 확인
        Showdown을 사용중이라면 Consol 접속 가능 할 것.
        $ echo $JAVA_HOME
        /var/packages/Java8/target/j2sdk-image/jre
        
    9. Showdown Manager 설정 파일 수정
        $ cd [Showdown Manager 설치 디렉토리]
        $ vi config.php
        
            $http_path = ""; // Showdown Manager 설치되어 있는 디렉토리
            $client_path = ""; // Showdown 설치되어 있는 디렉토리
            $start_page = 1; // 메뉴 번호 1~7
        
            $JAVA_HOME = "/var/packages/Java8/target/j2sdk-image/jre"; // 시스템의 $JAVA_HOME 위치
            
    10. Showdown Server 구동 및 구동 확인
        $ nohup ./start.sh &
        $ ps axf | grep java
            java -jar Server.jar
            
    11. Showdown Client 종료 확인
        Showdown이 사용하는 sqlite 특성상 cli.sh, cli.bat, Client.jre 등 동작시 정상적으로 작동하지 않습니다.
        Showdown Manager를 이용해서 수정할 경우 수정 시점에 Showdown Client가 종료되어 있는 것을 확인해 주세요.
        
```    

## Version History
    * v0.1 / 20190512
        Drama 기능 추가
    * v0.2 / 20190513
        TV/엔터 기능 추가
        시작 메뉴 config 추가
    * v0.3 / 20190514
        객체화로 소스 리뉴얼
    * v0.4 / 20190514
        SQL Lock 이슈로 인해 객체화 롤백
    * v0.5 / 20190516
        모니터링 관련 Client 명령어 처리 부분 DB Access로 변경
        config.php 설정에 자동 접속 페이지를 설정할 수 있는 start_page 추가 
        Episode Page 오픈시 제일 하단으로 자동 스크롤 추가
    * v0.5.1 / 20190516
        1000개 이상 되는 에피소드 정렬 이슈 수정 
        
## 알려진 버그
    * 현재 500개 이상되는 에피소드를 가진 방송의 경우 모든 에피소드 정보가 안보여 지는 이슈
    
## 남기는 말
  먼저 Showdown을 제작 및 공개해주신 iodides님께 감사드립니다.<br>
  기본적인 기능만 급하게 만들게 되어 보안 및 소스 코드의 구조화등 많은 부분이 부족한 소스 입니다.<br> 
  동작 방식은 최대한 iodides님이 만든 형태를 안건드리는 형태 입니다.<br>
  그로 인해 일부 기능은 현재 Shell(client.sh)에서만 가능 합니다.<br>
  이용에 참고해 주세요.<br>
  Showdown을 사용함에 있어 조금이나마 도움이 되었으면 합니다.
  
  감사합니다.
