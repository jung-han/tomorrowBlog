# HTTP / HTTPS의 이해
- 이경환 수석님

nc -> netcat, tcp 서버 
$ nc -l 8080 // 8080 포트 서버를 띄운 것
$ http nc localhsot 8080 

HTTP 응답은 크롬 개발자도구에서 Response를 확인하는게 편할것..
(따로 nc사용하는 것보다..)


## Request
* 1.1에서는 HOST까지만 작성해도 작동함(나머지는 부가)

<메서드> <요청 URL> <버전>
<헤더>
바디와 헤더의 구문은 한줄 개행으로 구분
<엔터티 본문>

## Response
<버전> <상태 코드><사유 구절>
<헤더>

<엔티티 본문>


## 메서드
* GET
* POST
* DELETE
* PUT
* PATCH


