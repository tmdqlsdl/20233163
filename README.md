# 리눅스 명령어
###### 20233163 임정은

## top
* 현재 OS의 상태를 나타내주는 CLI 어플리케이션임.
* top 명령어는 시스템의 프로세스/멤노리 사용 상태를 5초 간격으로 업데이트하여 출력함.
* top을 실행하는 동안 주기적인 업데이트로 실시간에 근접한 내용을 보여줌.
* 메모리 사용량, CPU 사용량 등을 나타냄.
* 위에는 전체의 요약 , 아래는 각 프로세스마다 구체적인 내용을 포함함.
 ![image](https://github.com/tmdqlsdl/20233163/assets/133830068/240b9d53-4126-46da-8066-f026d850af1b)


#### 요약 영역 (상단 위치)
: 전체 프로세스가 OS에 대해서 리소스를 어느정도 차지하고 있는지를 알려줌
- 대표적인 값 : 시간, 유저, 로드 에버리지,테스크,CPU,메모리
![image](https://github.com/tmdqlsdl/20233163/assets/133830068/0b9d2821-c5fd-46c3-a4a3-f85f72134496)  
1. 가장 먼저 보이는 숫자 : 시스템으미 현재 시간 임. 
 * GMP 기준으로 표시됨.
 * GMT 16:58:55 -> +9 -> 00시 58분 55초 
2. 다음으로 표시되는 것 : OS가 얼마나 살아있는지를 나타냄
 * days 로 표시
 * 위 사진에서 7일과 1시 15분 동안 서버가 살아있음 을 알 수 있음.
3.: 현재 접속중인 유저 세션 수를 나타냄.

### 로드 애버리지
: CPU Load의 이동 평균을 표시함.
CPU 로드란? CPU가 수행하는 작업의 양 -> 실행되거나대기중인 프로세스의 평균임. in 리눅스
싱글 코어 
* 1.0의 값 -> CPU 100%를 사용한다는 뜻
멀티 코어
* 해당 코어 수 만큼 * N을 한 값이 CPU 100%를 사용한다는 의미가 됨.
100% 넘는다면 -? CPU 에서 처리하지 못 하고 대기중인 프로세스가 존재한다는 뜻.

### Taks
: 현재 프로세스들의 상태를 나타내주는 영역임
  - 전체 프로세스, running -> running 상태의 프로세스 , sleeping -> 대기 상태 process , stopped -> 종료된 프로세스 ,   Zombie -> 좀비상태인 프로세스의 수  를 나타냄.
  - 일반적으로 IO 기반의 일과 CPU 기반의 일을 번갈아 가면서 수행함.
  - IO 기반의 일을 하게 될 떄 -> CPU는 idle 타임에 들어감.
  - 프로세스 스케줄링 알고리즘에 의헤 프로세스는 번갈아가면서 실행
  ![image](https://github.com/tmdqlsdl/20233163/assets/133830068/5fdb0193-ecc6-4282-909f-175caf760738)
  * 실행(Runnable) - CPU에 의해서 명령어가 실행중인 Process
  * 준비(Ready) - CPU의 명령어 실행을 기다리는 Process
  * 대기(Waiting) - I/O operation이 끝나기를 기다리는 Process
  * 종료(Terminated) - Ctrl + Z 등의 signal로 종료된 Process
  * Zombie - Process는 root Process로 부터 뿌리내린 자식 Process의 형식으로 트리구조를 형성함. 이 때 부모가 먼저 종료된 다면 root process로 부터 닿을 수 없는 Process가 생김. :zombie 

### CPU 사용량
: CPU가 어떻게 사용되고 있는지 그 사용율을 보여주는 영역임
모든 값의 총 합 = 100% 
 * us : 프로세스의 유저 영역에서의 CPU 사용률
 * sy : 프로세스의 커널 영역에서의 CPU 사용률
 * ni : 프로세스의 우선순위(priority) 설정에 사용하는 CPU 사용률
 * id : 사용하고 있지 않는 비율
 * wa : IO가 완료될때까지 기다리고 있는 CPU 비율
 * hi : 하드웨어 인터럽트에 사용되는 CPU 사용률
 * si : 소프트웨어 인터럽트에 사용되는 CPU 사용률
 * st : CPU를 VM에서 사용하여 대기하는 CPU 비율
 
### 메모리 사용량
%CPU(s) 영역 아래에 메모리와 관련된 영역 있음.
1. 좋은 RAM의 메모리 영역 
2. SWAP 메모리 영역 : 디스크 메모리 처럼 이용함.
 ***일반적으로 Mem의 사용량이 거의 가득 찼을때 사용,***
 ***디스크 임 -> RAM 메모리 속도가 많이 느림***
* total : 총 메모리 양
* free : 사용가능한 메모리 양
* used : 사용중인 메모리 양
3. buff/cache : 커널 버퍼에서 사용되는 메모리를 뜻함
 * IO와 관련되어 사용되는 버퍼에 사용되는 메모리
 * IO에 상대적으로 빠른 속도를 가질 수 있음
5. chache : Disk의 페이지 캐시

---
## PS
* 현재 실행중인 프로세스 목록과 상태를 보여줌 (윈도우의 작업 관리자와 비슷한 것)
* ps 사용법
![image](https://github.com/tmdqlsdl/20233163/assets/133830068/0fc28154-7f48-4631-b181-59e6cd7ec71c)
* 사용법 예시
 >$ ps - ef : 모든 프로세스를 풀 포맷으로 출력
![image](https://github.com/tmdqlsdl/20233163/assets/133830068/f2e28692-938c-4306-bed1-45ffeb20474a)

>$ ps -ef | grep '프로세스명' : '프로세스명'의 프로세스 구동 확인
![image](https://github.com/tmdqlsdl/20233163/assets/133830068/54db4500-c935-43a0-94a8-fbc1c11c3fa0)

출력 내용

![image](https://github.com/tmdqlsdl/20233163/assets/133830068/ed2f346d-8698-4fe8-8b52-9c7330097139)

BSD 계열 옵션

![image](https://github.com/tmdqlsdl/20233163/assets/133830068/0f8aee73-34b6-4c34-afee-cf860e30ca1d)

---
## jobs
: 리눅스 명령어 jobs는 작업이 중지된 상태, 백그라운드로 진행 중인 작업 상태, 변경 되었찌만 보고되지 않은 상태등을 표시함
* 사용법 
   jobs [옵션] [job ID]
   jobs -x command [args]
* 옵션 

![image](https://github.com/tmdqlsdl/20233163/assets/133830068/d8f55cf8-9bbb-49b9-beee-8eb7e4268603)
* jobs로 알 수 있는 세션의 상태

![image](https://github.com/tmdqlsdl/20233163/assets/133830068/837d6f79-10d0-4a9f-8bc2-d001990a0740)

---
## kill
: 프로세스를 지정하고 신호를 보내서 제어하는 명령어임.
* 프로세스를 종료하는 용도로 많이 사용됨.
> 사용법 : kill [옵션]

![image](https://github.com/tmdqlsdl/20233163/assets/133830068/f06f49e9-ebe3-472d-ac98-7842c209b965)
> kill -9
  사용방법 : kill 뒤에 -9옵션으로 프로세스아이디를 저장하고 종료 신호를 입력하는 것이 가장 일반적임.
  
  ![image](https://github.com/tmdqlsdl/20233163/assets/133830068/92559cc2-8502-4b1e-b2d7-c748521898b8)
  
  -ㅣ 옵션을 사용 -> 사용 가능한 모든 신호 확인 가능
  
  ![image](https://github.com/tmdqlsdl/20233163/assets/133830068/f0f27305-7b3c-4529-ae18-c2144b4a384c)

* 신호 번호
 신호이름 으로 신호를 보낼 수 있음
 신호로 강제로 종료시킬 떄 사용 -> -9-SIGKLL 등등 옵션을 주어 사용
  
  

  


 














