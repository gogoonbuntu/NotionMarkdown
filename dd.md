> 공식문서에서 발췌했습니다.

## Jenkins 기본구조

Java Servlet 기반, war 파일 형태로 제공

[##_Image|kage@WYGzg/btrzle5uTpM/ksmoLTYm1SojZHJFglKDK1/img.png|CDM|1.3|{"originWidth":724,"originHeight":749,"style":"alignLeft"}_##]

## 설정하기 (CasC : Configuration as Code)

Manage Jenkins >> Configuration as Code >> View Configuration

\* 다운로드해서 코드 편집 가능  
\* 반영시 Reload 필요

### yaml 사용

-    CASC\_JENKINS\_CONFIG 경로상의 모든 .yml, yaml, .YML 확장자 파일
-   /.hidden/secret.yml 과 같이 숨김 디렉터리로 숨김 가능
-   심볼릭링크 사용가능. (파일 링크, 디렉토리도 추적함)
-   다른 파일들이 같은 설정을 건드릴시 충돌 발생

## 여러가지 기능

**Jenkins Job :** Jenkins 가 shutdown 됐을 시, 메일로 알람을 보내고 자동으로 재가동 시키는 스크립트 예제 (groovy)  
         링크 : **[https://www.jenkins.io/doc/book/managing/nodes/](https://www.jenkins.io/doc/book/managing/nodes/)**

**Groovy Sandbox** : Groovy 하위 명령어만 실행가능한 안전장치. 관리자 수동 승인 없이 스크립트 실행을 위한 방법

**User Theme** 조정 가능

**빌드 후에도 프로세스 유지시키기** : BUILD\_ID 대신 JENKINS\_NODE\_COOKIE 사용

**빌드 Agent 활용** 기본옵션 : Controller 자체 노드에서 빌드하기, BUT Agent 사용 권장

**Agent, Controller 보안** (Agent 에서 악성 스크립트를 보내지 못하게 제어) 기본 탑재

**빌드 실행시 권한** : 기본 SYSTEM 권한으로 실행. 하지만 권장하지 않음. plugin 사용 추천       
         [https://www.jenkins.io/doc/book/security/build-authorization/](https://www.jenkins.io/doc/book/security/build-authorization/)

**환경변수 활용 / 필터링** 기능 제공

**SSH plugin, Jenkins CLI** 제공

**Jenkins 인스턴스 백업/복원 가이드라인** [https://www.jenkins.io/doc/book/system-administration/backing-up/](https://www.jenkins.io/doc/book/system-administration/backing-up/)   
         Controller 키 별도로 백업할 것, 각종 플러그인 제공, 백업할 필요 없는 디렉터리 등

**젠킨스 로깅** [https://www.jenkins.io/doc/book/system-administration/viewing-logs/](https://www.jenkins.io/doc/book/system-administration/viewing-logs/)

**url 형태로 API를 통한 요청 보내기** (e.g. https://jenkins.url/jobs/test , apiToken 발급필요)

**스레드 덤프 얻기** jstack, jvm 에서도 물론 가능. **Jenkins UI 웹에서도 가능**. 

[##_Image|kage@4uYdI/btrziRbRh7O/RB8l1BrfRKaGsMGRgAIKRK/img.png|CDM|1.3|{"originWidth":728,"originHeight":80,"style":"alignLeft"}_##]

## 소감

Jenkins 자체의 상세 설정을 위주로 다뤄져있다.

기본세팅이 충분히 잘 되어있고, Jenkins 서버 자체의 완성도는 추후에 추구해도 큰 문제는 없다. (폐쇄망이기 때문에)

공식문서에는 Jenkins - Gitlab 연동, Docker 활용 등을 다루고 있지 않다. (Docker 로 Jenkins 설치, 초기 세팅 등은 있음)

\* 프로젝트 Dockerize  
\* 완성도 있는 Dockerize  
Publish Over SSH

## 개인적인 구축 Flow

-   각자 서비스를 골라 Gitlab 에서 자신의 Repository에 Fork, Jenkins에 Hook 주기
-   Jenkins 에서 프로젝트 Build 하는 방법 연구 (Publish over SSH, 어느 단계에서 넘길 것인가?)
-   Build된 프로젝트 Docker Build 하는 방법 연구 (일련의 shell 명령어로 Base Image 위에 execute 하기)  
    -   도커 이미지 용량 축소하는 방법 = 빌드 시간 축소 방법
-   Container 실행하기, 끝
-   (Optional) 최소한의 작동 테스트 방법
-   (Optional) 로깅, 알람
-   (Optional) 모니터링 방법 연구
