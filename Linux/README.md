# 리눅스 명령어 모음

---
## 파일 시스템 탐색

- pwd (print working directory)
- cd (change directory)
  - cd ..
  - cd lucid
- ls (list segments)
  - l을 붙이면 좀더 자세히
  - a를 붙이면 숨긴 파일도
  - r를 붙이면 정렬방향 변경
  - t를 붙이면 시간순으로 내림차순
- rm (): 삭제
  - -r을 붙이면 디렉토리안 하위 파일도 싸그리 삭제
  - f를 붙이면 묻지도 따지지도 않고 삭제

- mkdir (make directory): 디렉토리 생성
  - -p: 하위 디렉토리 까지 생성
    - mkdir -p a/b/c/d/e/ 
- rmdir (remove directory): 빈 디렉토리 삭제

- lsblk : 사용 가능한 블록 장치  나열 

- mount : SD카드 혹은 USB 연결시 수동으로 연결하는 법

- df (): 저장된 장치의 다양한 정보
  - -h를 붙이면 이쁘게

## 시스템 조작

- uname : 시스템 측정 세부 사항 등의 정보를 얻기위한 명령어

- ps (): 돌고 있는 프로세스 
   - -e를 붙이면 모든 프포세스 포여주기
   - -f를 붙이면 자세히
   - ps -ef | grep hwang 로 같이 쓰기도 함
   - grep (): 파일내에 특정 문자열을 찾아 그 행들을 보여줌
- kill -9 {PID} : 프로세스를 죽인다.

- service : 시스템 서비스를 호출
- batch : 정의된 일정에 따라 시스템 서비스 실행
- shutdown : halt, init과 함께 시스템 종료

- touch : 유요한 빈 파일을 작성
- cat : 새파일 작성 및 터미널에서 파일 내용을 보고 출력을 다른 명령행이나 파일로 리디렉션함
- head : 파일 시작 부분을 보여준다.
- tail : 파일의 끝 부분부터 보여준다.
  - -n은 끝에서 어드정도까지
  - f는 로그파일을 계속때
  - \> 를 하면 다른 파일에 저장

- cp (copy): 복사
  - -r을 붙이면 디렉토리 통째로

- mv (move) : 파일 혹은 디렉토리 위치 이동
- ㅌcomm : 두 개의 파일을 공통 행과 구별되는 행으로 비교
- less : 터미널 세션을 방해하지 않으며 파일 내에서 양방향으로 탐색
- ln : 디스크 공간의 파일이나 디렉토리의 심벌릭 링크의 여러 인스턴스 생성
- cmp : 파일을 비교하고 결과를 표준 출력 스트림으로 인쇄
- dd : 파일을 한 유형에서 다른 유형으로 복사 및 변환
- alias : 터미널에서 파일의 다른 문자열로 단어를 바꾸는 것

## 알쓸리명

https://dora-guide.com/linux-commands/





- netstat (): 네트워크 연결상태
  - -a를 붙이면 모든 소켓
  - t를 붙이면 tcp만
- - 
- - 
- ipconfig (): ip 확인
- 
- 
- - 
- find (): 파일 찾기
  - .은 현재와 하위 디렉토리
  - /는 루트까지 포함한 전체
- man (): 명령어에 대한 설명
- chmod (): 파일의 권한 바꾸기
- rwxr-xr-x
  - -R을 붙이면 그 하위까지 다 변경
  - r: 읽기 가능
  - w: 쓰기 가능
  - x: 실행 가능
- chmod 777 파일명 
  - 7이란 읽고 쓰기 권한
  - 4 읽고
  - 2 쓰고
  - 1 실행 가능
  - 6 읽고 쓰기 
- top : 시스템의 상태를 전반적으로 파악(CPU,  Memory, Process)
   - vmstat(proc(대기하는 프로세스 등에 대한 정보), cpu, io,memory, swap )과 유사
- iostat : 디스크 입출력 정보를 보여줌
- free -m 메로리 확인