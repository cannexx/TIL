> [리눅스 - 생활코딩](https://opentutorials.org/course/2598)를 보고 정리한 내용입니다.

# 리눅스 - 생활코딩

## 1.디렉토리와 파일

- ls : 현재 디렉토리에 있는 파일들의 목록 표시
    - -l 옵션
        - 현재 위치하고 있는 디렉토리의 파일과 디렉토리를 list 형태로 자세히 보여준다.
    - -a 옵션
        - 현재 디렉토리에 있는 숨김 디렉토리/파일도 표시
        - 리눅스/유닉스에 앞에 .이 찍혀 있는 디렉토리/파일은 숨김디렉토리/숨김 파일이다.
- pwd : 현재 위치하고 있는 디렉토리 경로 표시
- mkdir 디렉토리명 : 디렉토리 생성. mkdir(make Directory)의 약자
    - -p 또는 –parents 옵션
        - 부모 디렉토리를 생성
        - 생성하고자 하는 디렉토리가 dir1/dir2/dir3/dir4 일때 mkdir -p dir1/dir2/dir3/dir4를 하면 각 부모디렉토리도 생성된다.
- touch 파일명 : 파일생성
- mv 현재파일명 바꿀 파일명 : 파일명 변경

## 2. --help와 man

- 명령어 –help : 해당 명령어에 대한 간단한 설명 표시
- man 명령어 : 해당 명령어에 대한 상세 설명 표시
    - help와 man의 차이는 help는 현재 페이지를 빠져나가지 않고 간단한 설명을 표시하며 man은 전용 페이지로 이동해서 상세한 설명을 표시
    - `/ 검색어` 를 사용하여 특정 단어를 검색할 수 있으며, n키를 사용하여 검색된 단어를 찾아갈 수 있다.
    - q키를 누르면 상세 설명 페이지에서 빠져나올 수 있다.

## 3. sudo

- Super User Do의 약자
- 유닉스 계열의 운영체제의 특징중 하나는 다중 사용자 시스템이다. 그래서 각각의 사용자마다 permission(권한)이 다르다. 특정 명령어나 작업시 Super User의 권한이 필요할 때가 있는데 해당 권한이 필요할 때 sudo를 사용한다.
- sudo 권한을 가진 사람만이 sudo 명령어를 사용할 수 있다.
- sudo 명령어는 유닉스 및 유닉스 계열 운영 체제에서 다른 사용자의 보안권한과 관련된 프로그램을 구동할 수 있게 해주는 프로그램이다. 이것은 substitute user do (다른 사용자의 권한으로 명령을 이행하라는 뜻이다.)

## 4. nano Editor

- Ctrl+g는 nano Editor 설명서로 이동. 설명서에서 Ctrl+x를 하면 설명서 빠져나옴
- Ctrl+o는 Write out(쓰기)
- Ctrl+x는 nano Editor 종료
- Ctrl+k는 현재 커서가 있는 Text가 잘라내기가 된다.
- Ctrl+u는 현재 커서에 붙여넣기를 한다.
- nano는 복사기능은 없고 잘라내기와 붙여넣기만 있다.
- 일부 문자만 복사하고 싶다면 커서를 복사하고 싶은 문자에 놓고 Ctal+6을 누르면 Mark Set이 되며 복사하고 싶은 글자의 뒤에까지 커서를 이동후 Ctrl+k 해서 잘라내기 후 Ctrl+u를 해서 붙여넣기를 한다.
- Ctrl+w 후 검색어를 입력하면 검색을 할 수 있으며 해당 단어를 계속 찾고 싶으면 Ctrl+w후 Enter를 하면서 진행하면된다. 검색어를 변경하지 않으면 처음 입력한 검색어가 계속 저장되어 있다.

## 5. 패키지 매니저

- 패키지 == Application (참고로 명령어도 패키지 이다.)
- 오늘날의 리눅스들은 패키지를 다운받을 수 있는 패키지 매니저를 제공한다.
- 리눅스의 대표적인 패키지 매니져는 apt와 yum이 있다.
- apt-get update
    - 패키지 매니저를 통해 설치할 수 있는 패키지 리스트를 최신으로 업데이트
- apt-cache search 패키지명
    - 시스템에 캐시되어 있는 패키지 정보 검색(다운로드 할 수 있는 패키지 리스트가 뜬다.)
- apt-get upgrade
    - apt-get을 통해 설치한 모든 패키지에 대해 upgrade 진행
- apt-get upgrade 패키지명
    - 해당 패키지 upgrade
- apt-get remove 패키지명
    - 해당 패키지 삭제

## 6. wget

- wget 프로그램을 사용하여 URL을 통해 파일을 다운로드 할 수 있다.
- wget url을 하면 파일 다운로드 진행
- wget -O 파일명 URL
    - -O 옵션을 사용하면 다운로드 받는 파일의 파일명을 지정할 수 있다.    

## 7. 왜 CLI인가

- GUI에 비해 리소스가 적으며, 한번에 다양한 작업을 할 수 있다.

### 순차적 실행

- 예를들어 디렉토리를 생성하고 해당 디렉토리로 이동하는 명령어를 CLI에서는 한 줄로 작성할 수 있다. `;`를 사용해서 여러 명령어를 조합해 순차적으로 실행 시킨다.

  - `mkdir why;cd why`

### 파이프 라인

- 파이프라인이란 하나의 명령(프로그램,프로세스)의 결과를 다른 명령(프로그램,프로세스)의 입력으로 주는 것으로 `|`을 사용하여 파이프라인을 연결

  - 파이프라인을 설명할 수 있는 대표적인 명령어는 grep
    - grep 명령어는 어떠한 정보에서 필요한 정보가 포함되어 있는 행을 찾는 명령어
      - 앞의 명령어의 결과가 grep의 입력으로 들어가 해당 단어들을 검색
      - `ls --help | grep sort cat 파일명 | grep sort ps aux | grep apache`
      - cat 파일명 : 해당 파일의 내용을 보여줌
      - ps : 현재 실행중인 프로세스 리스트를 보여줌

## 8. IO Redirection

- Redirection이란 스트림의 흐름을 바꾸는 것.

### Output

- 아래 그림을 보면 Unix Process는 Standard Input를 받아서 Standard Output 또는 Standard Error을 Output 한다. 예를들어 ls 명령어는 화면에 현재 디렉토리에 있는 디렉토리와 파일을 화면에 출력하는데, ls가 Standard Input이며, 결과를 화면에 출력하는게 Standar Output인 것이다. Standard Error는 Error에 대한 Output 이다. > Command-line Arguments란 명령어 뒤에 파라미터를 의미한다. 예를들어 ls -al 일때 -al이 Command-line Arguments 이다.

    > Unix는 하나의 Input과 두개의 OutPut이 존재

![https://user-images.githubusercontent.com/31675104/61879669-7a7ed680-af2e-11e9-8f33-27796559500b.jpg](https://user-images.githubusercontent.com/31675104/61879669-7a7ed680-af2e-11e9-8f33-27796559500b.jpg)

Review_+UNIX+Programs+Means+of+input_+Means+of+output_

- 만약 ls -l의 결과를 화면이 아닌 파일에 저장할려면 어떻게 해야할까? 그럴때는 Redirection 하면된다. Redirection시 사용하는 기호는 `>`이다.
- ls -l의 결과를 result.txt에 저장
    - `ls -l > result.txt`
- 위에서 Redirection시 `>` 기호를 사용하였는데 `>` 기호 앞에는 1이 생략되어 있다. `1>`는 Standard Output을 의미하며, `2>`는 Standard Error를 의미한다.
- 아래 명령어는 rm rename2.txt가 Standard Output 이면 result.txt에 output을 기록하고 Standard Error이면 error.log에 기록한다는 명령
    - `rm rename2.txt 1> result.txt 2> error.log`

 ### Input

- hello.txt의 내용을 cat의 input으로 받음
    - `cat < hello.txt`
- `cat < hello.txt`와 `cat hello.txt` 의 차이는?
    - `cat hello.txt` 에서 hello.txt는 Command-line Arguments
    - `cat < hello.txt`에서 hello.txt는 Standar Input이다. cat은 Standar Input 으로도 입력을 받을 수 있는 프로그램이기 때문에 가능.
- head 파일명: 앞쪽에 있는 일부 텍스트만 출력하는 명령어(기본 10줄 출력)
    - -n출력할행수
        - 해당 행수만 출력
    - head는 Command-line Arguments로 -n1을 받고 Standar Input으로 linux.txt를 받고 Standar Output을 one.txt에 저장
        - `head -n1 < linux.txt > one.txt`

### Output append

- `>>`는 redirection 결과를 output이 append 한다는 뜻
- `<<`는 동일한 문자가 나오기 전까지 계속 Input이 append 된다는 뜻
    - hello1.txt의 내용은 기존 hello.log에 덮어 쓰기 되는 것이 아닌 추가(append가 된다.)
        - `cat hello.txt > hello.log cat hello1.txt >> hello.log`
    - hhh문자가 나오기 전까지 계속 append 된다.
        - `mail ji@naver.com << hhh qqq aaa xxx hhh // hhh가 나와서 hhh까지 append 된다.`

### Output을 보지 않는 방법

- /dev/null 활용
  
    - /dev/null은 Unix 계열에서 휴지통 같은 것
- ls -al의 Standard Output을 /dev/null로 redirection 시키기 때문에 아무것도 출력되지 않는다.

    ls -al > /dev/null

## 9. 쉘과 커널

- Shell
    - 껍데기, 주변
    - 커널을 감싸고 있음
    - 사용자와 상호작용하는 소프트웨어
    - 사용자가 입력한 명령어를 해석해서 Kernal이 이해할 수 있는 방식으로 변경해서 전달하는 역할
    - 다양한 Shell이 존재하기 때문에 자신에게 맞는 Shell을 사용할 수 있다.
- Kernel
    - 알맹이,핵심,코어
    - OS에서 Core
    - 하드웨어를 감싸고 있음
    - Shell 부터 명령어를 받아 하드웨어를 조작

## 10. 쉘 스크립트

- Shell Script란 Shell에서 사용할 수있는 명령어들의 조합을 모아서 만든 배치파일이다. > 배치 파일은 명령 인터프리터에 의해 실행되게끔 고안된 명령어들이 나열되어 있는 텍스트 파일

- Shell Script 예제

    ```
    #!/bin/bash //OS에게 아래 작성되는 코드가 bin안에 있는 bash에 의해 해석된다고 알려주는 것
    
    if ! [ -d bak ]; then //현재 디렉토리에 bak라는 디렉토리가 존재하지 않는다면 
        mkdir bak   //bak 디렉토리를 생성한다.
    fi  //if문 끝
    cp *.log bak    //현재 디렉토리에 .log로 끝나는 모든 파일을 bak 디렉토리에 copy 한다.
    ```
> 현재 디렉토리에 있는 Shell Script 실행시 ./쉘스크립트이름 으로 실행한다.

## 11. 디렉토리의 구조

[Linux Directory Structure (File System Structure) Explained with Examples](https://www.thegeekstuff.com/2010/09/linux-file-system-structure/?utm_source=tuicool)

![https://user-images.githubusercontent.com/31675104/62005583-64605880-b170-11e9-80f1-2eb4cc1ba3a4.png](https://user-images.githubusercontent.com/31675104/62005583-64605880-b170-11e9-80f1-2eb4cc1ba3a4.png)

filesystem-structure

- `/` - Root
    - `/`는 Root directory를 의미
    - 모든 파일 및 디렉토리는 루트 디렉토리에서 시작
    - Root 사용자 만이 `/`디렉 토리 아래 Write 권한이 있다.
    - `/root`는 root 사용자의 Home directory이며 `/`와는 전혀 다른 의미이다.
- `/bin` - User Binaries
    - 바이너리 실행파일이 들어 있는 디렉토리이다.
        - 실행가능한 프로그램을 바이너리라 하며 bin이라고 부르기도 한다.
    - 단일 사용자 모드에서 사용하는 일반적인 Linux 명령들이 존재하는 디렉토리이다.
    - ps, ls, grep 등이 이 디렉토리에 있다.
- `/sbin` - System Binaries
    - 바이너리 실행파일이 들어 있는 디렉토리이다.
    - `/bin`과의 차이점은 `/sbin`은 시스템 관리자가 시스템 관리 목적으로 사용하는 바이너리가 들어있다.
    - reboot, ifconfig 등이 이 디렉토리에 있다.
- `/etc` - Configuration Files
    - 프로그램에 필요한 설정파일이 들어있는 디렉토리이다.
    - 프로그램을 시작/중지하는 데 사용되는 Shell Script가 해당 디렉토리에 포함된다.
- `/dev` - Device Files
    - device Files 이 들어있는 디렉토리이다.
    - terminal devices, usb, 시스템에 연결된 모든 장치가 포함된다.
- `/proc` - Process Information
    - System Process에 대한 정보가 들어있는 디렉토리 이다.
- `/var` - Variable Files
    - var는 변수 파일을 담고 있는 디렉토리이다.
    - 내용이 계속 변경되고 증가되는 파일이 해당 디렉토리에 포함된다.
    - 각종 로그파일들…
- `/tmp` - Temporary Files
    - 시스템 및 사용자가 만든 임시 파일이 들어있는 디렉토리이다.
    - `/tmp`에 있는 파일은 시스템이 재부팅 될 때 삭제된다.
- `/usr` - User Programs
    - 2차 level 프로그램의 바이너리, 라이브러리 문서, 소스 코드가 들어 있다.(사용자가 설치하는 Program이 위치하는 directory이다.)
    - `/usr/bin`에는 사용자가 설치한 바이너리 파일이 들어있다.
    - `/usr/sbin`에는 사용자가 설치한 시스템 관리자를 위한 바이너리가 들어있다.
- `/home` - Home Directories
    - 사용자가 자신의 개인 파일을 저장할 수 있는 Home Directory가 있는 Directory 이다.
    - `~`을 사용하면 현재 사용자의 Home Directory로 이동한다.
- `/boot` - Boot Loader Files
    - Boot Loader와 관련된 파일이 들어 있는 디렉토리이다.
- `/lib` - System Libraries
    - `/bin` 및 `/sbin` 에 있는 바이너리들이 공통으로 사용하는 libary가 보관되어 있는 Directory

## 12. 프로세스

### 컴퓨터의 구조

- 컴퓨터는 크게 Processor, Memory, Storage로 구성
- Program이 실행되면 Storage에 저장되어 있는 Program을 읽어서 메모리에 적재시키며, Processor는 메모리에 적재된 Program을 읽어와서 처리한다.
- 파일의 형태로 Stroage에 저장되어 있는것을 Program이라 하며, Memory이 적재되어 Processor가 처리하고 있는 Program을 Process라 한다.

### 프로세스 모니터링(ps, top, htop)

- ps : Process List를 보여주는 명령어
    - -aux 옵션
        - 백그라운드에서 실행되고 있는 Process도 표시
- top / htop : 프로세스를 확인할 수 있는 Program인데, htop는 top에 비해 시각적으로 더 뛰어나다.(htop는 설치가 필요하다)

## 13. 파일을 찾는 법

### locate와 find

- locate
    - locate 찾고자하는 파일

    - locate는 디렉토리를 뒤지는 것이 아닌 시스템안에 저장되어 있는 파일들에 대한 정보를 담고 있는 DB를 검색하기 때문에 속도가 빠르다. locate가 사용하는 DB를 mlocate라 한다.

    - mlocate는 시스템에 의해 하루에 한번씩 최신화되며, updatedb 명령어를 사용하여 수동으로 최신화 할 수도 있다.

    - 예제 

      ``` locate *.log //확장자가 log인 파일들을 검색
      updatedb //mlocate 최신화 
      ```
- find
    - locate와 다르게 디렉토리를 검색한다.
    
    - DB가 아닌 디렉토리를 검색하기 때문에 항상 최신화된 파일을 검색할 수 있다.
    
- 디렉토리를 검색하기 때문에 locate에 비해 성능은 떨어지나 다양한 검색 옵션이 존재하며, 항상 최신화된 파일을 검색할 수 있다는 장점이 있다.
  
- 예제 
  
    ``` find / // /는 root 디렉토리부터 검색한다는 의미이다.
    find . // .은 현재 디렉토리 부터 하위 디렉토리까지 검색한다는 의미이다.
    
    find / -name apache.log // -name 은 지정된 형식의 패턴을 가지는 파일을 검색
        
    find / -type f -name apache.log // -type는 지정한 파일타입에 해당하는 파일을 검색
        
    find / -type f -name “apache.log” -exec rm -f {} // -exec는 찾은 파일들을 대상으로 뒤에 나오는 명령어를 실행하라는 의미이며, {}는 찾아진 파일들을 하나씩 대입됨을 의미한다. 따라서 검색된 파일의 개수만큼 -exec 뒤의 명령어가 실행된다. 
    ```

### whereis와 $PATH

- whereis
    - 실행파일을 찾아주는 명령어이다.
    
    - 시스템 전체를 검색하는 것이 아닌 $PATH와 $MANPATH에서 검색한다.
    
    - $PATH는 환경변수라고 부른다.
    
    - 예를들어 ls를 치면 Linux는 $PATH에 등록된 디렉토리를 뒤져서 ls를 찾아서 실행한다.
    
    - 예제
    
       ```
       whereis ls // ls 실행파일 경로와 메뉴얼에 대한 경로 표시
       whereis rm // rm 실행파일 경로와 메뉴얼에 대한 경로 표시
       ```

## 14. 백그라운드 실행

- 백그라운드와 포그라운드(background and foreground)
    - 모든 프로세스는 백그라운드 또는 포그라운드 두 가지 중 하나의 모드로 작동
    - 포그라운드는 현재 유저와 상호작용하고 있는 프로세스이며, 백그라운드는 포그라운드 뒤에서 돌아가고 있는 프로세스이다.
    - `Ctrl + z` : 포그라운드를 백그라운드로 보내는 단축키
    - `jobs` : 백그라운드 작업들의 목록을 보여주는 명령어
    - `fg` : 가장 최신 백그라운드를 포그라운드로 가져오는 명령어
      
        - `fg %숫자` : 해당 숫자에 해당하는 백그라운드를 포그라운드로 가져오는 명령어. 숫자는 jobs 명령어로 확인
    - `kill %숫자` : 해당 숫자에 해당하는 백그라운드를 종료. 숫자는 jobs 명령어로 확인
    - fg를 통해 백그라운드에 있는 프로세스를 포그라운드로 가져올떄 `+`,`-`,`공백` 순서로 불러온다.
    ![https://user-images.githubusercontent.com/31675104/62547799-c1f75200-b8a0-11e9-9ec1-200533e50dc7.PNG](https://user-images.githubusercontent.com/31675104/62547799-c1f75200-b8a0-11e9-9ec1-200533e50dc7.PNG)
    
    - 실행할때부터 백그라운드로 보내기
        - 명령어 뒤에 &가 붙으면 명령어가 실행될 때 백그라운드로 실행된다.
    
        ![https://user-images.githubusercontent.com/31675104/62550418-316f4080-b8a5-11e9-896b-ea63e23ae72e.PNG](https://user-images.githubusercontent.com/31675104/62550418-316f4080-b8a5-11e9-896b-ea63e23ae72e.PNG)
    
        - `ls -alR > result.txt 2> error.log &` 명령어가 백그라운드에서 실행중일때는 Running인 것을 알 수 있으며, 작업이 끝난 뒤에는 Exit 된 것을 알 수 있다.
    
## 15. 항상 실행(daemon, service)

### daemon

daemon이란 리눅스 시스템이 가동될 때 실행되는 백그라운드 프로세스의 일종이며, 사용자의 요청을 기다리고 있다가 요청이 발생하면 이에 적절히 대응하는 리스너와 같은 역할을 한다.

daemon을 가전제품에 비유하면 아래와 같다. *냉장고는 항상 켜져있어야 하는데 그 이유는 언제 사용될지 모르기 때문이다. ** TV는 껐다 킬수 있는데 그 이유는 필요한 시점과 필요할 수 없는 시점을 알 수 있기 때문이다.

위의 비유를 프로그래밍에 비유하면 ls, rm, mkdir 명령어 등은 TV로 생각할 수 있으며, 웹서버는 냉장고로 생각할 수 있다.

### service와 자동실행

- daemon의 목적을 가진 프로그램들은 `/etc/init.d` 디렉토리에 위치한다.
- daemon 실행 및 종료시에는 `service, start, stop` 명령어를 사용한다.

        apt-get install apache2 // 웹서버는 daemon의 목적을 가지기 때문에 /etc/init.d 디렉토리에 위치한다.
        cd /etc/init.d
        sudo service apache2 start // apache2 실행
        sudo serviee apache2 stop // apache2 종료

- daemon은 시스템이 가동될 때 실행되어야 하기때문에 시스템에 등록이 필요한데, daemon을 등록하는 방법은 아래와 같다.
    1. `/etc` 디렉토리로 이동
    2. `/etc` 디렉토리 안에는 rcx.d(x는 숫자) 디렉토리가 있는데 CLI일 경우 rc3.d로 이동하며, GUI일 경우 rc5.d로 이동한다. > CLI일 경우 rc3.d에 있는 daemon들이 실행되며, GUI일 경우 rc5.d에 있는 daemon 들이 실행 된다.
    3. 해당 디렉토리에 들어가면 실제 daemon에 Link가 걸려 있는데, 링크 이름에는 의미가 있다.
        - 링크가 S로 시작되면 시스템이 가동될 때 해당 daemon은 실행되는 것이며, K로 시작되면 해당 daemon은 실행되지 않는 것이다.
        - S,K 뒤에 붙은 숫자는 우선 순위이다.

정리하면 특정 daemon을 시스템이 가동시 실행시키고 싶다면 CLI일 경우에는 rc3.d에 GUI일 경우 rc5.d에 위의 규칙에 따라 실제 daemon 파일에 Link를 걸면딘다.    

## 16. cron

cron 이란 정기적으로 명령을 실행시켜주는 도구(소프트웨어)이다.

`crontab -e` 명령어를 통해 하고자 하는 일을 정의할 수 있다.

![https://user-images.githubusercontent.com/31675104/63689684-9505e180-c845-11e9-945d-900658bd6aa4.png](https://user-images.githubusercontent.com/31675104/63689684-9505e180-c845-11e9-945d-900658bd6aa4.png)

위의 cron 설정은 1분마다 date를 실행하여 성공하면 data.log에 시간을 저장하고, error가 발생하면 출력하도록 하는 설정이다.

## 17. 쉘을 시작할 때 실행

쉘을 시작할 때 특정한 명령어를 실행할 수 있다.

bash를 예로 들면 bash는 Shell이 처음 실행될 때 홈 디렉토리에 있는 .bashrc에 있는 내용을 읽어온다.

    cd ~ // 홈 디렉토리로 이동
    vi .bashrc // .bashrc vim으로 편집

.bashrc 파일 가장 마지막에 `echo 'Hi, bash'` 작성 후 저장한 뒤 bash를 다시 시작하면 아래와 같이 hello가 출력되는 것을 알 수 있다.

![https://user-images.githubusercontent.com/31675104/63774737-da471380-c918-11e9-80ec-3e9719151be0.PNG](https://user-images.githubusercontent.com/31675104/63774737-da471380-c918-11e9-80ec-3e9719151be0.PNG)

![https://user-images.githubusercontent.com/31675104/63774742-dc10d700-c918-11e9-8d19-a9ecb7e5d167.PNG](https://user-images.githubusercontent.com/31675104/63774742-dc10d700-c918-11e9-8d19-a9ecb7e5d167.PNG)
    
## 18. 다중 사용자

### id와 who

`id` 명령어를 통해 현재 사용자의 실제 id와 그룹 id 등을 알 수 있다.

![https://user-images.githubusercontent.com/31675104/63862202-2bbdd400-c9e7-11e9-964a-18db28970dfe.PNG](https://user-images.githubusercontent.com/31675104/63862202-2bbdd400-c9e7-11e9-964a-18db28970dfe.PNG)


`who` 명령어를 통해 현재 시스템에 어떤 사용자가 로그인했는지 알 수 있다.

아래 사진을 보면 현재 시스템에 hun이라는 사용자 2명이 접속한 것을 할 수있다.

![https://user-images.githubusercontent.com/31675104/63862206-2c566a80-c9e7-11e9-9c1c-a813359cb1a4.PNG](https://user-images.githubusercontent.com/31675104/63862206-2c566a80-c9e7-11e9-9c1c-a813359cb1a4.PNG)

# 19. 관리자와 일반 사용자

## 관리자와 일반 사용자

UNIX 계열에서는 크게 2가지 사용자가 있다.

1. Super user or Root user
2. user
- sudo
  
    - sudo는 Super user의 권한을 임시적으로 사용할 수 있는 명령어로, 아무 user나 사용할 수 있는 것이 아니라 Super user가 될 수 있는 권한을 가진 user만이 사용할 수 있다.
- root 계정 lock 거는법
    - root 계정을 사용하지 못하도록 lock을 걸 수 있다.
    - `sudo passwd -l root`
        - `-l`은 lock의 약자이다.
- root 계정 lock 푸는법
    - `sudo passwd -u root`
        - `-u`는 unlock의 약자이다.
    - 만약 root 계정의 비밀번호를 설정한 적이 없다면 unlock시 비밀번호를 설정하라고 한다.
- Super user의 홈 디렉토리와 user의 홈 디렉토리
  
    - user의 홈 디렉토리는 `/home`안에 user 별로 존재하지만 Super user(root)는 특별한 user 이므로 `/root`가 Super user(root)의 홈 디렉토리이다.
- Super user 계정을 사용한다면 prompt가 `#`으로 변하고 user 계정을 사용한다면 `$`로 변한다.
    - user
        ![https://user-images.githubusercontent.com/31675104/63946198-b0742500-caaf-11e9-8db3-b1160556cdb9.PNG](https://user-images.githubusercontent.com/31675104/63946198-b0742500-caaf-11e9-8db3-b1160556cdb9.PNG)

    - Super user
        ![https://user-images.githubusercontent.com/31675104/63946199-b0742500-caaf-11e9-9bba-6dfd10e9785c.PNG](https://user-images.githubusercontent.com/31675104/63946199-b0742500-caaf-11e9-9bba-6dfd10e9785c.PNG)

## 20. 사용자의 추가

### 1. 사용자 계정 생성

    사용자 추가는 Super User의 권한이 있어야 추가가 가능하다.

- useradd 계정명
    - 해당 계정을 생성한다.
- useradd -m 계정명
    - 해당 계정의 home 디렉토리와 계정을 생성한다.
- useradd 계정명 -m -s /bin/bash
    - 해당 계정의 home 디렉토리와 쉘 환경 및 계정을 생성한다.
    - 쉘 환경을 잡아주지 않으면 아래와 같은 문제가 발생한다.

![https://user-images.githubusercontent.com/31675104/64963231-e436b380-d8d3-11e9-8165-2e57825aa401.PNG](https://user-images.githubusercontent.com/31675104/64963231-e436b380-d8d3-11e9-8165-2e57825aa401.PNG)

### 2. 생성한 계정에 비밀번호 설정

계정을 생성한 후에는 해당 계정의 비밀번호를 설정해 주어야 한다.
이떄도 Super User의 권한이 필요하다.

    passwd 계정명

### 3. sudo 권한 부여하는 법

계정 생성시에 sudo 권한을 부여할 수 있고, 계정 생성 후에도 sudo 권한을 부여할 수 있다. 여깃는 계정 생성 후 sudo 권한을 부여하는 법을 알아보겠다.

sudo 권한 부여도 역시 sudo 권한을 가진 계정이 진행할 수 있다.

usermod는 계정 수정시 사용하는 명령어로 -a는 group에 user를 추가한다는 의미이며, -a 사용시 -G는 무조건 사용되어야 하는 옵션이다.

아래 명령의 의미는 해당 계정을 sudo 그룹에 추가하겠다는 의미이며, sudo 그룹에 추가함으로써 해당 계정은 sudo를 사용할 수 있다.

    sudo usermod -a -G sudo 계정명

## 21. 권한(Permission)

### 1. 권한(Permission)

UNIX 계열의 시스템에서 Permission을 통해 제어하는 대상은 File과 Directory 이다. 즉, File과 Directory에 대해 read/write/excute에 대한 Permission을 관리!

    -rw-rw-r-- 1 hun hun 3 sep 17 13:32 perm.txt

1. `-rw-rw-r--`에서 가장 앞에 있는 `-`는 file인지 directory인지 link인지 알려주는 정보로 `-`는 file, `d`는 directory를 뜻한다.
2. `-`뒤에 `rw-rw-r--`는 access mode로 해당 File/directory에 권한을 의미하며, 3개씩 묶어서 3등분으로 나눠서 권한을 표현하며, `r : read / w : write / x : excute` 를 의미한다.
    1. 첫 번째 `rw-`는 owner의 권한을 의미하며, owner는 해당 파일에 대해 `read,write를 할 수 있다는 의미이다.`
    2. 두 번째 `rw-`는 group의 권한을 의미하며, group는 해당 파일에 대해 `read, write를 할 수 있다는 의미이다.`
    3. 세 번째는 other의 권한을 의미하며, other은 해당 파일에 대해 `read를 할 수있다는 의미이다.` > 여기서 other은 owner와 group를 제외한 모든 user를 의미한다.
3. `hun hun`에서 첫 번쨰 hun은 owner를 의미하며, 두 번째 hun은 group를 의미한다.

### 2. 권한을 변경하는 방법(chmod)

chmod를 사용해서 권한을 변경할 수 있다.

`chmod [권한][파일]`

    chmod o-r perm.txt // other가 perm.txt 파일을 read 할 수 없도록 처리
    chmod o+r perm.txt // other가 perm.txt 파일을 read 할 수 있도록 처리
    chmod o+w perm.txt // other가 perm.txt 파일을 write 할 수 있도록 처리
    chmod u-r perm.txt // user가 perm.txt 파일을 read 할 수 없도록 처리
    chmod u+r perm.txt // user가 perm.txt 파일을 read 할 수 있도록 처리

### 3. 실행의 개념과 권한 설정

파일에 excute 권한이 없으면 해당 파일을 실행 할 수 없다.

아래의 내용을 가지는 shell script를 생성하였다.

![https://user-images.githubusercontent.com/31675104/65049246-6ab8c700-d9a0-11e9-82c9-db1eaf4b5e5d.PNG](https://user-images.githubusercontent.com/31675104/65049246-6ab8c700-d9a0-11e9-82c9-db1eaf4b5e5d.PNG)

    #!/bin/bash
    echo 'hi hi hi'

생성된 shell script의 권한을 보면 user에게도 excute 권한이 없기 때문에 Permission denied와 함께 실행이 되지 않는다.

![https://user-images.githubusercontent.com/31675104/65049347-9045d080-d9a0-11e9-922c-47745c4b95cb.PNG](https://user-images.githubusercontent.com/31675104/65049347-9045d080-d9a0-11e9-922c-47745c4b95cb.PNG)

hi-machine.sh 파일에 대해 user에게 excute 권한을 부여하니 실행가능한 파일이라는 뜻으로 파일 이름의 색상이 변경 되었다.

    chmod u+x hi-machine.sh

![https://user-images.githubusercontent.com/31675104/65049446-b4091680-d9a0-11e9-8784-b49d27ab82f0.PNG](https://user-images.githubusercontent.com/31675104/65049446-b4091680-d9a0-11e9-8784-b49d27ab82f0.PNG)

user는 해당 파일에 대한 excute 권한이 있으므로, 파일이 정상적으로 실행 되는 것을 알 수있다.

![https://user-images.githubusercontent.com/31675104/65049542-ddc23d80-d9a0-11e9-8d87-8771869eeeea.PNG](https://user-images.githubusercontent.com/31675104/65049542-ddc23d80-d9a0-11e9-8d87-8771869eeeea.PNG)

### 4. directory의 권한

directory에서 r은 `directory 안에 있는 file나 directory를 열람할 수 있느냐에 대한 권한`이다. 아래 권한에서 other는 perm director 안에 있는 file과 directory를 열람할 수 없다.

    drwxrwx--- 1 hun hun 4096 sep 17 13:32 perm/

![https://user-images.githubusercontent.com/31675104/65050751-e3208780-d9a2-11e9-9871-efa9feb00edc.PNG](https://user-images.githubusercontent.com/31675104/65050751-e3208780-d9a2-11e9-9871-efa9feb00edc.PNG)

directory에서 w는 directory에 속한 file에 대한 write 권한이 없는 것으로 `write 권한이 없기 때문에 파일 생성/삭제/이름 변경/파일 읽기 등이 모두 안된다`. 아래 권한에서 other은 perm 디렉토리에 파일 생성/삭제/이름변경/파일수정 등이 모두 불가하다.

    drwxrwxr-x 1 hun hun 4096 sep 17 13:32 perm/

![https://user-images.githubusercontent.com/31675104/65051288-d2bcdc80-d9a3-11e9-95b1-052a59d9d2f5.PNG](https://user-images.githubusercontent.com/31675104/65051288-d2bcdc80-d9a3-11e9-95b1-052a59d9d2f5.PNG)

directory에서 x는 directory에 cd 명령을 사용해서 `해당 directory에 들어갈 수 있느냐에 대한 권한이다.` 아래 권한에서 other은 perm 디렉토리에 들어갈 수 없다.

    drwxrwxrw- 1 hun hun 4096 sep 17 13:32 perm/

![https://user-images.githubusercontent.com/31675104/65051444-19123b80-d9a4-11e9-9a94-6f6310e16ca9.PNG](https://user-images.githubusercontent.com/31675104/65051444-19123b80-d9a4-11e9-9a94-6f6310e16ca9.PNG)

> 만약 중첩되어 있는 디렉토리에 대해 권한을 모두 바꾸고 싶다면 -R옵션을 사용. R은 Recursive의 약자이다. chmod -R 디렉토리

### 5. chmod 사용법 정리

chmod [options] mode[,mode] file1 [file2 …]

options의 대표적인 것은 -R이 있다 `-R은 재귀적으로 파일들과 디렉터리들의 mode를 바꾸는 것이다.`

mode는 access mode를 뜻하며 `문자열 모드와 8진법 숫자`가 있다. 1. 문자열 모드 - 문자열 모드는 위에서 사용한 방법으로 모드에 래퍼런스와 연산자 모드를 조합 하여 권한을 부여하는 방법이다.

![https://user-images.githubusercontent.com/31675104/65052813-fa14a900-d9a5-11e9-9e8c-476db62155f0.PNG](https://user-images.githubusercontent.com/31675104/65052813-fa14a900-d9a5-11e9-9e8c-476db62155f0.PNG)

![https://user-images.githubusercontent.com/31675104/65052830-00a32080-d9a6-11e9-8a48-bf9d2b144c54.PNG](https://user-images.githubusercontent.com/31675104/65052830-00a32080-d9a6-11e9-8a48-bf9d2b144c54.PNG)

![https://user-images.githubusercontent.com/31675104/65052838-0436a780-d9a6-11e9-932f-b2fad1a6211c.PNG](https://user-images.githubusercontent.com/31675104/65052838-0436a780-d9a6-11e9-932f-b2fad1a6211c.PNG)

1. 8진법 숫자
- 8진법 숫자는 Permission에 해당하는 숫자들을 조합하여 권한을 부여하는 방법이다.

    chmod 777 text.txt //text.txt 파일에서 user,group,other는 read,write,execute 권한을 가진다.
    
    chmod 744 text.txt //text.txt 파일에서 user는 read,write,execute 권한을 가지며 group와 otherdms read의 권한만을 가진다.

![https://user-images.githubusercontent.com/31675104/65052906-1fa1b280-d9a6-11e9-8f59-9b7d39ec5621.PNG](https://user-images.githubusercontent.com/31675104/65052906-1fa1b280-d9a6-11e9-8f59-9b7d39ec5621.PNG)

### 참고

https://en.wikipedia.org/wiki/Chmod#Command_line_examples

## 22. 그룹(group)

### 1. intro

모든 Other가 아닌 특정 Other에게만 파일 또는 디렉토리에 권한(Permission)을 부여하고 싶다면 어떻게 해야할까?

이런 경우에는 특정 Other를 Group로 묶고 해당 Group이 해당 파일 또는 디렉토리를 사용할 수 있도록 권한(Permission)을 부여하면 해당 Group는 해당 파일 또는 디렉토리를 사용할 수 있다.

### 2. groupadd

groupadd는 새로운 그룹을 생성할 때 사용 하는 명령어이다. 기본 사용법은 아래와 같다.

`groupadd [option] 그룹이름`

    groupadd developer //developer 그룹 생성

그룹이 정상적으로 생성되었는지 확인할려면 /etc에 있는 group 파일을 확인하면 된다. 만약 정상적으로 생성되었다면 가장 아래에 해당 group이 생성 되어 있다.

### 3. chown

chownd은 file,directory의 소유자 또는 그룹을 변경할 때 사용 하는 명령어 이다. 기본 사용법은 아래와 같다.

`chmod [option]... [OWNER][:[GROUP]] FILE...`

    usermod -a -G developer hun //사용자 hun을 developer group에 추가
    chown root:developer . //현재 디렉토리의 소유자는 root로, group은 developer로 변경

## 23. 인터넷, 네트워크 그리고 서버

- 인터넷의 기본은 client가 server에 request를 보내고 response를 받는 구조
- 인터넷을 통해 통신을 하기 위해서는 ip주소가 필요.
- ip 주소는 사람이 외우기 어렵기 때문애 Domain을 사용. Domain으로 요청을 하면 DNS 서버에 의해 해당 Domain의 ip를 알아내서 해당 Server에 접속
- `http://ipinfo.io/ip` - 현재 나의 ip를 알 수 있는 웹사이트
- CLI에서는 브라우저를 사용할 수 없기 때문에 curl을 통해 위의 서비스에 요청을 보내면 현재 나의 IP를 알 수있다.
- 아래사진을 보면 현재 내 서버의 ip는 192.168.208.131인데 ipinfo.io/ip로 부터 확인한 나의 ip는 39.122.63.132이다.
    - 192.168.208.131를 가진 서버가 자신의 ip 주소를 알 수 있는 서버에 요청을 보냈는데 전혀 다른 ip가 온 이유는 Public ip와 Private ip의 차이 때문이다.

    ![https://user-images.githubusercontent.com/31675104/65253074-f6fbf300-db34-11e9-9515-25af396e1264.PNG](https://user-images.githubusercontent.com/31675104/65253074-f6fbf300-db34-11e9-9515-25af396e1264.PNG)

## 24. 웹서버(아파치)

### 1.apache 설치

    apt-get update //package 최신화
    apt-get install apache2 //apahce 설치
    service apache2 start //apache 시작
    service apache2 restart //apache 재시작
    service apache2 stop //apache 중지

### 2. apache 테스트

1. 프로세스 확인

아래 사진을 보면 apahce 프로세스가 정상적으로 올라온 것을 알 수있다. > 아래 프로그램은 htop 이다.

![https://user-images.githubusercontent.com/31675104/65374706-d1532300-dcc7-11e9-96d5-40d3a4272748.PNG](https://user-images.githubusercontent.com/31675104/65374706-d1532300-dcc7-11e9-96d5-40d3a4272748.PNG)

캡처

> 위의 그림을 보면 apache의 프로세스가 상당히 많은 것을 알 수있다. apache 프로세스가 많이 올라오는 이유는 apache는 요청 당 프로세스가 처리하는 구조이기 때문에 apache 프로세스가 기본적으로 많이 생성되는 것이다. 만약 현재 생성된 프로세스보다 접속이 더 많아지면 apache 프로세스는 더 생성되며, 접속이 줄어든다면 기존 프로세스들이 종료된다.

1. 웹브라우저에서 확인

apache가 정상적으로 실행되고 있다면 브라우저에서 웹서버가 설치된 ip를 입력하면 아래와 같은 화면을 볼 수있다.

> 참고로 웹서버가 설치된 Linux는 현재 컴퓨터에 가상머신에 있기 때문에 추가 설정없이 바로 접근가능한 상태이다.

![https://user-images.githubusercontent.com/31675104/65374780-b3d28900-dcc8-11e9-87ca-04da684ce62a.PNG](https://user-images.githubusercontent.com/31675104/65374780-b3d28900-dcc8-11e9-87ca-04da684ce62a.PNG)

캡처

1. 웹서버가 설치된 서버에서 웹브라우저 사용

현재 웹서버가 설치된 서버에서 테스트 하는 방법도 있다. 그러기 위해서는 웹브라우저 역할을 하는 `elinks`라는 프로그램이 필요하다.

    apt-get install elinks

위의 프로그램을 설치하고 난 후 `elinks http://localhost` 또는 `elinks http://IP주소`를 입력하면 위와 동일한 내용인 아래와 같은 화면을 볼 수있다.

![https://user-images.githubusercontent.com/31675104/65374820-365b4880-dcc9-11e9-898d-aabb1ec4bed0.PNG](https://user-images.githubusercontent.com/31675104/65374820-365b4880-dcc9-11e9-898d-aabb1ec4bed0.PNG)

캡처

### 3. apache configuration

- unix 계열에서 어떤 프로그램이 어떻게 동작할 것인가에 대한 설정은 /etc에 설정되어 있다.
- apache2에 대한 설정 파일은 /etc/apache2에 존재한다.
- 가장 중요한 파일은 apache2.conf 이다. apache2.conf를 보면 아래의 사진처럼 설정파일을 가져오는 부분이 있는데 아래 설정의 뜻은 /etc/apache2/sites-enabled 디렉토리 안에 있는 확장자가 .conf인 파일을 모두 include 한다는 뜻이다.

    ![https://user-images.githubusercontent.com/31675104/65434595-098a6b00-de5a-11e9-9792-6fe69f30513d.PNG](https://user-images.githubusercontent.com/31675104/65434595-098a6b00-de5a-11e9-9792-6fe69f30513d.PNG)

    캡처

- 아래 사진은 /etc/apache2/sites-enabled 디렉토리이며, .conf로 끝나는 파일이 있는 것을 알 수 있다.

    ![https://user-images.githubusercontent.com/31675104/65434869-83225900-de5a-11e9-8ef7-64fe419ea592.PNG](https://user-images.githubusercontent.com/31675104/65434869-83225900-de5a-11e9-8ef7-64fe419ea592.PNG)

    캡처

- 해당 파일을 열어보면 아래와 같은 설정이 있으며, 설명하자면 80번 포트로 HTTP 요청이 들어오면 DocumentRoot에 있는 index.html을 전송하는 설정이다.

    ![https://user-images.githubusercontent.com/31675104/65434596-0a230180-de5a-11e9-8d2f-41f5f2537557.PNG](https://user-images.githubusercontent.com/31675104/65434596-0a230180-de5a-11e9-8d2f-41f5f2537557.PNG)

### 3. log

- 위에서 말한 apache 설정 파일을 보면 ErrorLog와 CustomLog가 있는 것을 볼 수 있다. ErrorLog는 apache 오류와 관련된 log를 저장하는 파일이며, CustomLog는 apache에 접근한 내역을 볼 수 있는 로그이다.

    ![https://user-images.githubusercontent.com/31675104/65434596-0a230180-de5a-11e9-8d2f-41f5f2537557.PNG](https://user-images.githubusercontent.com/31675104/65434596-0a230180-de5a-11e9-8d2f-41f5f2537557.PNG)

    캡처1

> ${APACHE_LOG_DIR}은 /var/log/apache2이다.

## 25. SSH

- 시큐어 셸(Secure Shell, SSH)은 네트워크 상의 다른 컴퓨터에 로그인하거나 원격 시스템에서 명령을 실행하고 다른 시스템으로 파일을 복사할 수 있도록 해 주는 응용 프로그램 또는 그 프로토콜이다.

출처 : [위키백과 - SSH](https://ko.wikipedia.org/wiki/%EC%8B%9C%ED%81%90%EC%96%B4_%EC%85%B8)

- SSH는 Server와 Client가 있는데 SSH Client를 통해 SSH Server에 접속할 수 있다.

### 1. SSH Server 설치

    sudo apt-get update //패키지 최신화
     sudo apt-get install openssh-server //SSH Server 설치
     sudo service ssh start //SSH Service 시작
     sudo ps -aux | grep ssh //SSH Service가 정상적으로 실행중인지 확인

### 2. SSH Client 설치

    sudo apt-get update //패키지 최신화
     sudo apt-get install openssh-client //SSH Client 설치
     ssh 접속하고자하는계정@ip주소 //Ex.hun@192.168.0.65 : 192.168.0.65에 있는 hun 계정으로 SSH 접속
     ssh -p포트번호 접속하고자하는계정@ip주소 //Ex.hun -p25 @192.168.0.65 : 192.168.0.65에 25번 포트로 hun 계정으로 SSH 접속

## 26. 포트(port)

### 1. 포트란 무엇인가?

- TCP나 UDP 에서 어플리케이션이 상호구분을 위해서 사용하는 번호이다. IP 내에서 프로세스 구분을 하기 위해서 사용한다. 쉽게말하면, 각 프로토콜의 데이터가 통하는 논리적 통로이다. 컴퓨터의 물리적 포트 (랜선) 에서 데이터가 통해오는것처럼, 컴퓨터 안에서 각 프로토콜의 데이터가 컴퓨터 내부의 논리적 포트에 따라 흐른다.
    - 출처 : [나무위키 - 포트](https://namu.wiki/w/%ED%8F%AC%ED%8A%B8)
- 포트는 0 ~ 65535 까지 있다.
- 네트워크에서 0 ~ 1024 까지 Well known port(잘 알려진 포트)라 해서 아주 많은 사람들이 표준처럼 사용하고 있는 시스템 들이 있다. 예를들어 웹서버 80포트, ssh 22 포트

### 2. 포트 포워딩(port forwarding) 

- 특정 포트로 접속시 해당 접속을 특정 컴퓨터로 포워딩하는 기능이다. 
- 예를들어 211.46.24.37:9000 으로 접속시 192.168.0.60:80 으로 포워딩 시키는 것이다.

## 27. 도메인(domain)

### 1. DNS

- Domain Name System
- Domain을 IP로 바꿔주는 System
- 현재 내 컴퓨터 또는 서버가 어떤 DNS를 사용하는지에 대한 정보는 /etc/resolv.conf에 있다. > Domain을 통해 IP를 알아내고 싶다면 `host 명령어를 사용하면 된다. Ex.host google.com`

### 2. host 파일 

- DNS가 있기 전에는 hosts라는 파일을 사용하였다. hosts 파일은 어떤 Domain이 어떤 IP라는 정보를 가지고 있는 파일이다. 
- hosts 파일에 요청한 Domain에 대한 정보가 없으면 DNS로 요청하며, 정보가 있으면 DNS를 요청하지 않고 해당 정보를 사용한다. - host 파일의 위치는 /etc 디렉토리 안에 hosts 파일이다.

### 3. Sub Domain 

- Sub Domain이란 Domain에 발급되는 보조 도메인이다. 주로 같은 도메인을 사용하는데 다른 서버를 지정하고 싶을 때 사용한다. 예를들어 naver.com 도메인 에서 도메인앞에 blog라는 서브도메인이 붙으면 블로그 관련 서버를 가리키고, news라는 서브도메인이 붙으면 뉴스 관련 서버를 가리키는 것이다.

### 4. DNS 동작 원리

1. 클라이언트에는 DNS가 연결되어 있다. (편의상 나의 DNS로 부르겠습니다.)
2. 클라이언트 컴퓨터에 연결되어 있는 나의 DNS는 root DNS의 주소를 알고있다. root DNS는 전세계에 흩어져 있으며 하나가 죽어도 나머지가 역할을 할 수 있도록 여러대로 구성되어 있다.
3. 나의 DNS는 Top-level Domains을 담당하는 DNS가 누구인지 root DNS에게 문의한다.
4. root DNS는 해당 Top-level Domains을 담당하는 DNS의 목록을 나의 DNS에게 돌려준다.
5. 나의 DNS는 Top-level Domains을 담당하는 DNS중 하나를 선택해서 Second-level domain을 관리하는 DNS를 문의한다.
6. Second-level domain을 관리하는 DNS는 해당 domain에 대한 ip를 나의 DNS에게 알려준다.
7. 나의 DNS는 Client에게 해당 IP를 전달한다.

![https://user-images.githubusercontent.com/31675104/65609747-4043bb00-dfeb-11e9-90f8-c17929158baa.PNG](https://user-images.githubusercontent.com/31675104/65609747-4043bb00-dfeb-11e9-90f8-c17929158baa.PNG)

> - Domain 마지막에는 .이 생략되어 있으며 이러한 .을 root라 한다.

## 28. 인터넷을 통한 서버간 동기화 (rsync)

### 1. rsync란?

- rsync란 remote + sync가 합쳐진 단어
- 원격에 있는 파일과 디렉토리를 복사하고 동기화 하기 위해서 사용

### 예제. src 안에 있는 파일들을 dest에 동기화

    cd ~
    mkdir rsync
    cd rsync/
    mkdir src 
    mkdir dest 
    cd src/
    touch test{1..10} //테스트를 위해 src 디렉토리안에 test1 ~ test10 파일 생성
    cd ..
    rsync -a src/ dest //src 밑에 있는 파일을 dest 폴더에 동기화.

> -a 옵션은 archive 모드로 기본적으로 특정 디렉토리를 지정했을때 디렉토리 안에 디렉토리가 존재하면 디렉토리 전체를 복사하는 모드로 동작하며 그리고 변경사항들만 전송하는 모드로 동작하며, 각각의 파일의 현재속성도 같이 전송하는 옵션이다.

### 예제. 증분 카피

rsync의 가장 큰 매력은 증분 카피를 한다는 것. 즉, 전송할 대상이 있을 때만 전송이 한다.

    cd ~
    cd dest/
    rm test10
    cd ..
    rsync -av src/ dest //dest에서 삭제한 test10 파일만 동기화 된다.
    cd src/
    touch test11
    cd ..
    rsync -av src/ dest //src에서 생성한 test11 파일만 동기화 된다.

### 2. Remote sync

- 네트워크를 통해 원격 컴퓨터에 동기화를 할 수 있다.

### 예제

A 컴퓨터에 ~/rsync/src 안에 있는 파일들을 B 컴퓨터의 hun 계정의 ~/rsync/dest로 동기화 할려고한다. B 컴퓨터의 IP 주소는 192.168.0.65 이다.

    rsync -azP ~/rsyncs/src/ hun@192.168.0.65:~/rsync/dest //A 컴퓨터의 ~/rsync/src안에 있는 파일을 B 컴퓨터 ~/sync/dest 에 동기화

> z 옵션은 압축하고 전송한다는 것. P 옵션은 진행사항을 나타내는 옵션이다.

## 29. 로그인 없이 로그인 하기(ssh key)

### 1. ssh public key, private key

아이디, 비밀번호를 사용하지 않고 로그인을 하기 위해서는 Public Key와 Private Key가 필요하다.

![https://user-images.githubusercontent.com/31675104/65966909-b472d880-e49b-11e9-8095-b10463f89da5.PNG](https://user-images.githubusercontent.com/31675104/65966909-b472d880-e49b-11e9-8095-b10463f89da5.PNG)

    ssh-keygen //SSH Key 생성 명령어
    
    Enter file in which to save the key (디렉토리) : Private Key가 생성될 위치
    
    Enter passphrase (empty for no passphrase) // Private Key에 비밀번호를 설정할지에 대한 질문으로 생략해도 된다. 만약 보안을 더 강화하고 싶다면 설정
    
    Enter sam passphrase again: //비밀번호 재확인

위의 과정을 거치고 나면 위에서 지정한 디렉토리에 Public Key와 Private Key가 생성되어 있다.

아래 사진을 보면 디렉토리에 대해서 소유자에 대해서만 rwx 권한이 주어져 있으며 Public Key와 Private Key에 대해서도 소유자에 대해서만 rw 권한이 주어져 있다.

![https://user-images.githubusercontent.com/31675104/65966912-b50b6f00-e49b-11e9-9554-ef83b145e3b1.PNG](https://user-images.githubusercontent.com/31675104/65966912-b50b6f00-e49b-11e9-9554-ef83b145e3b1.PNG)

이제 생성된 public key를 로그인 하고자하는 서버에 로그인하고자 하는 계정의 ~/.ssh 안에 있는 authorized_keys의 마지막에 Public Key의 내용을 붙여주면 된다.

> public key를 authorized_keys에 붙이는 과정에서 실수가 발생할 수 있으므로 ssh-copy-id를 통해 진행하면 좋다.

    ssh-copy-id 계정@ip

위의 명령어 입력 후 해당 계정의 비밀번호를 입력하면 Public Key의 내용이 authorized_keys에 추가된다. 내용이 정상적으로 추가되었다면 아래 명령어로 바로 로그인이 가능하다.

    ssh 계정@ip

### 2. rsync

rsync에 SSH 자동 로그인을 적용하면 cron이나 다른 유용한 유틸들을 사용하여 여러 편한 작업을 진행할 수 있다. (Ex.cron을 사용한 정기적 백업)

rsync는 기본적으로 ssh 프로토콜을 사용하기 때문에 현재 사용자의 ssh 디렉토리에 Public Key와 Private Key가 있는지 확인 후 존재하면 Public Key와 Private Key를 사용해서 전송을 하기 때문에 설정이 되어 있다면 로그인 하지 않고 사용이 가능하다.

아래 예제에서 현재 나의 서버와 나의 서버와 동기화 할 서버는 SSH key 설정이 되어 있는 상태이다.

현재 나의 서버

    cd ~
    mkdir rsync3
    cd rsync3
    touch test{1..100} // test1 ~ test100 파일 생성

현재 나의 서버와 동기화 할 서버

    cd ~
    mkdir rsync_welcome

동기화

    rsync -avz . hong@192.168.0.65:~/rsync_welcome //rsync3 디렉토리 안에 있는 test1~test100을 현재 나의 서버와 동기화 할 서버의 홈디렉토리 안에 있는 rsync_welcome에 동기화

### 3. RSA

암호화 방식은 대칭키 방식과 비대칭키 방식이 존재한다. 1. 대칭키 방식 - 하나의 key로 암호화하고 복호화 하는 방법이다. 2. 비대칭키 방식 - 암호화 할떄 key와 복호화 할 떄 key가 다른 방식으로, Private key를 통해 암호화를 하고 Public key를 통해 복호화 한다. 대표적인 방식으로 RSA가 있다.

Linux에서 SSH 로그인시 인증과정은 아래와 같다. 

1. SSH Client가 SSH Server에 접속하면 SSH Server는 랜덤하게 생성된 key를 SSH Client에게 전달한다. 
2. SSH Client는 현재 유저의 홈디렉토리안에 ssh 디렉토리 안에 있는 id_rsa 파일이 있는지 없는지 찾는다. 만약 파일이 있다면 SSH Server가 전달한 랜덤 key를 암호화하여 SSH Server에게 전송한다. 
3. SSH Server는 보냈던 랜덤 key를 authorized_keys에 있는 공개키를 사용해 복호화해서 자신이 보냈던 랜덤키와 동일한지 확인하고 일치하면 로그인되는 방식이다.

## 30. 연속적으로 명령 실행시키기(;과 &와 &&의 차이)

1. ;
- ;는 성공여부와 상관없이 다음 명령어를 실행 한다.

        mkdir test;cd test //test 디렉토리를 만들지 못하더라도 test 디렉토리로 이동한다.

2. &&

- &&는 성공한 경우에 다음 명령어를 실행한다.

        mkdir test&&cd test //test 디렉토리가 생성이 되어야 test 디렉토리로 이동한다.

3. &

- &는 해당 명령어를 백그라운드로 동작시킬 때 사용한다.

        mkdir test&cd test //test 디렉토리를 백그라운드로 생성함과 동시에 test 디렉토리로 이동하려고 했기 때문에 cd test는 존재하지 않는 디렉토리로 진입하려고 시도하기 때문에 오류가 발생한다.

4. {}

- 명령을 그룹핑할 때 사용한다.

        mkdir test3 && { cd test3; touch abc; echo 'success!!' } || echo 'There is no dir' //test3가 성공하면 cd test3; touch abc; echo 'success!!'이 실행되며 실패하면 echo 'There is no dir'가 실행된다. 프로그래밍의 삼항연산자와 유사하다.