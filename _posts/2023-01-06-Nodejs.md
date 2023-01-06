---
layout: single
title:  "Node.js 개요"
---

# Node.js 개요



## 1. Node.js 소개



### Node.js

##### • 2009년 Ryan Dahi

##### • 자바 스크립트 언어

##### • 크롬 V8 엔진



### Node.js의 특징

- ##### 싱글 쓰레드

- ##### 비동기 I/O

  - 시간이 걸리는 I/O
    - 하드 디스크 접근
    - 데이터베이스 서버
    - 네트워크를 이용해서 다른 서비스 접근
  - I/O 동작이 끝날 때까지 대기 : 동기식
  - I/O 동작이 끝날 때까지 대기하지 않음 : **비동기식**

- ##### 이벤트 기반(event driven)



### Node.js의 장점

- ##### 싱글 쓰레드로 작성

- ##### 비동기 I/O

- ##### 간단한 구조의 경량 프레임워크와 풍부한 라이브러리

- ##### 서버와 클라이언트에서 사용하는 언어가 같다.



### Node.js 권장 분야

- ##### 실시간 소셜 네트워크 서비스

- ##### 데이터 중심의 서비스

- ##### IoT 기기 연동



### 아키텍처

- ##### 상위 레벨 - JavaScript

- ##### 로우 레벨 - C

  - 바인딩
  - V8 엔진
  - libev : Event
  - libeio : I/O



### Node.js 재단

- ##### Node.js 재단

  - Node.js 플랫폼과 관련된 모듈 개발 지원하는 협업 오픈 소스 프로젝트
  - open gevernance model
  - 기술 결정 위원회(Technical Streering Committee)

- ##### 주요 멤버

  - IBM, intel, Joyent, Microsoft, PayPal, redhat



### 버전 구성과 지원

- Node.js 버전을 두 단계로 진행
- 기존 : 짝수버전(Stable) 홀수 버전(Unstable)
- 4.x 이후 : Stable, LTS
- LTS : 짝수 버전 Stable 6개월 이후 LTS로 전환
  - LTS(Long Term Support)
  - LTS : 호환성이 깨지는 변경 없음
  - LTS 18개월. 그후 Maintain 상태(12개월)
  - 매년 새로운 메이저 버전의 LTS 시작


---


## 2. 프로그래밍 모델



### 프로그래밍 모델

#### 동기(Synchronous)

- A 실행 - A 결과 - 

  B 실행 - B 결과

- 실행이 끝나고 다음 실행

#### 비동기(Asynchronous)

- A 실행 - B 실행 - B 결과 - A 결과
- 실행 결과가 끝날 때까지 기다리지 않는다.



### 동기식

#### 파일 읽기

```javascript
var fs = require('fs');
var content = fs.readFileSync("readme.txt", "utf8");
console.log(content);
console.log('Reading file...');
```



### 비동기식

#### 파일 읽기

```javascript
var fs = require('fs');
fs.readFile("readme.txt", "utf8", function(err, content){
    console.log(content);
});
console.log('Reading file...');
```



### 동기/비동기 방식의 코드 차이점

- ##### 동기식 함수 구현과 사용

  - 동기식 함수 구현

    ```javascript
    function.add(i,j){
    	return i+j;
    }
    ```

  - 동기식 함수 사용

    ```javascript
    var result = add(1,2);
    console.log('Result:',result);
    ```

- ##### 비동기식 함수 구현과 사용

  - 비동기식 함수 구현

    ```javascript
    function.add(i,j,callback){
    	var result = i+j;
    	callback(result);
    }
    ```

  - 비동기식 함수 사용

    ```javascript
    add(1,2,function(result){
    	console.log('Result:', result);
    });
    ```



### 비동기 방식의 API로 파일 읽는 코드 예

- ##### 콜백을 이용한 파일 읽기

  ```javascript
  fs.readFile('textfile.txt', 'utf8', function(err, text){
  	console.log('Read File Async', text);
  });
  ```



### 콜백 함수 형태

- ##### 비동기 함수의 에러 처리

  콜백 함수의 파라미터로

- ##### 대부분 비동기 API

  ```javascript
  callbackFunc(arg1, arg2, function(error, result){
      if(error){
          // 에러 처리
          return;
      }
      // 정상 처리
  });
  ```

  콜백 함수의 첫 번째 파라미터로 error를 전달받고 함수 내부에서 error 발생 여부 체크 후 return


---


## 3. Node.js 개발환경



### 다운로드

- 홈페이지(nodejs.org)
- 플랫폼에 맞는 설치 파일 다운로드
- 설치 진행



### 설치 확인

- 콘솔에서 node 명령 실행

- node -v

  - v : 버전 확인 옵션

    ```powershell
    PS C:\Users\???> node -v
    v18.12.1
    ```



### Node.js 명령어

- node 콘솔 명령
- node [SOURCE.JS] [ARGS]
  - v : 버전
  - e, p : 스트립트 평가
  - c : 실행하지 않고 문법 체크
  - r : 모듈을 미리 로딩
  - --help : 명령어 도움말



### REPL

- 콘솔 기반의 실행 환경



### 개발 도구

- IDE : Eclipse, WebStorm
- Editor : **Visual Studio Code**, Sublime, ...


---


## 4. Hello World



### 코드 작성 : helloWorld.js

```javascript
console.log('hello world');
```



### 실행

```powershell
node helloWorld.js
```



### 서버 코드

- helloWorld2.js

  ```javascript
  var http = require('http');
  http.createServer(function(request,response){
      response.writeHead(200,{'Content-Type':'text/html'});
      response.end('<h1>Hello World!</h1>');
  }).listen(3000);
  ```

   

- 웹 브라우저로 확인

  127.0.0.1:3000

- 실행

  `node helloWorld2.js`