# Linux Essential

Linux 시스템 관리 학습 과정에서 작성한 셸 스크립트 모음. 로그 점검, CPU 부하 테스트, 환경설정 배포, 네트워크 부하 측정 등 관리 실무형 스크립트로 구성.

- 셸: bash
- 대상: RHEL 계열, 사설망 서버(main / server1 / server2)
- 구성: `bin/` 관리 스크립트, `env/` 환경설정 예시

## 목차

1. [실행 방법](#1-실행-방법)
2. [스크립트 구성](#2-스크립트-구성)

## 1. 실행 방법

각 스크립트는 독립 실행. 인자가 필요한 스크립트는 사용법에 맞춰 전달.

```bash
cd bin

# 로그 점검 (인자로 로그 파일 경로 전달)
./chklog.sh /var/log/messages

# 네트워크 부하 테스트 (server / client 모드 지정)
./net_load.sh server     # 서버 측
./net_load.sh client     # 클라이언트 측
```

- 원격 접속 스크립트(cmd.sh, poweroff.sh)는 SSH 키 인증 전제
- 환경설정 스크립트(env_conf.sh)는 적용 후 env_unconf.sh로 원복

## 2. 스크립트 구성

### 로그 / 모니터링

| 파일 | 내용 |
|------|------|
| chklog.sh | 당일 로그에서 warn·error·fail 등 키워드 필터 |

### CPU / 프로세스

| 파일 | 내용 |
|------|------|
| cpu.sh | 무한 연산으로 CPU 부하 발생 |
| cpu2.sh | while 무한 루프 부하 |
| cpu3.sh | trap으로 시그널 처리, 백그라운드 다중 실행 제어 |

### 환경설정

| 파일 | 내용 |
|------|------|
| env_conf.sh | profile·bashrc 등에 설정 일괄 주입 |
| env_unconf.sh | 주입한 설정 원복 |
| env/bashrc.txt | alias·PS1 등 bashrc 설정 예시 |

### 원격 / 네트워크

| 파일 | 내용 |
|------|------|
| cmd.sh | 여러 서버에 동일 명령 SSH 실행 |
| poweroff.sh | 서버 순차 종료 |
| net_load.sh | iperf3 부하 측정 후 gnuplot 그래프 생성 |

### 기타

| 파일 | 내용 |
|------|------|
| testscript.sh | cowsay·boxes 출력 테스트 |
