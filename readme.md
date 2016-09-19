API
=============================
1. 전체 유저에 대한 정보조회
-----------------------------
url: /users/

2. 회원가입
-----------------------------
- url: /users/ 포스트 형태로 회원가입 요청을 보냄.  

Data|Description
---|--- 
user_id|이메일형식아이디
password|비밀번호
name|사용자 이름

- Response
{
	"message":"Success"
	"ErrorCode":0
}

- ErrorCode

|Data|Description|
---|---
|0|성공|
|-1|에러|
|-100|이미 존재하는 유저|
|-200|잘못된 이메일 포맷|


3. 개별유저에 대한 정보조회
-----------------------------
* url:  /users/find/?user_id=osori@osori.com

4. 로그인
-----------------------------
* url: /login/

|Data|Description|
---|---
|user_id|사용자 아이디|
|user_key|서버에서 발급하는 키, user_key없이 request를 날리면, 서버에서 발급|
|password|비밀번호|
|token|Pushtoken|

* Response
{
	"user_key": "...",
	"message":"Success",
	"ErrorCode":0
}

* ErrorCode

|Data|Description|
---|---
|0|성공|
|-1|에러|
|-100|아이디 오류|
|-200|비밀번호 오류|
|-300|인증 필요|	

5. 크롤러 전체 목록
-----------------------------
* url: /crawlers/

* Response
{
	"message":"Success",
	"crawlers":[
		{
			...
		},
		{
			...
		}	
	]
	"ErrorCode":0
}

* ErrorCode

|Data|Description|
---|---
|0|성공|
|-100|크롤러가 한개도 없음|

6. 유저가 구독중인 크롤러 목록
-----------------------------
* url:/subscriptions/item/ 

|Data|Description|
---|---
|user_id|사용자 아이디|
|user_key|서버에서 발급하는 키|

* Response
{
	"message":"success",
	"subscriptions": [
		{
			...
		},
	]
	"ErrorCode":0
}

* ErrorCode

|Data|Description|
---|---
|0|성공|
|-100|유효하지 않은 유저|
|-200|구독하고 있는 크롤러 없음|

7. 유저가 구독하려는 크롤러 추가
-----------------------------
* url: /subscriptions/

|Data|Description|
---|---
|user_id|사용자 아이디|
|user_key|서버에서 발급받은 키|
|crawler_id|구독하려는 크롤러 id|

* Response
{
	"message":"success",
	"ErrorCode":0
}

* ErrorCode

|Data|Description|
---|---
|0|성공|
|-100|유효하지 않은 유저|
|-1|에러|

8. 유저가 구독하고 있는 크롤러 제거
-----------------------------
* url: /subscriptions/item/ user_id=osori@osori.com user_key=asdf crawler_id=... (DELETE이용)

|Data|Description|
---|---
|user_id|사용자 아이디|
|user_key|서버에서 발급받은 키|
|crawler_id|구독하려는 크롤러 id|

* Response
{
	"message":"success",
	"ErrorCode":0
}

* ErrorCode

|Data|Description|
---|---
|0|성공|
|-100|유효하지 않은 유저
|-1|에러

9. 푸시토큰 등록
-----------------------------
* url: /tokens/

|Data|Description|
---|---
|user_id|사용자 아이디|
|user_key|서버에서 발급받은 키|
|token|firebase cloud message token|

* Response
{
	"message":"success",
	"ErrorCode":0
}

* ErrorCode

|Data|Description|
---|---
|0|성공|
|-100|유효하지 않은 유저|
|-1|에러|

10. 패스워드 변경
-----------------------------
* url:/password_change/ 

|Data|Description|
---|---
|user_id|사용자아이디|
|password|현재사용중인 비밀번호|
|new_password|변경할 비밀번호|

* Response
{
	"message":"success", "ErrorCode":0
}

* ErrorCode

|Data|Description|
---|---
0|성공
-100|현재 비밀번호와 다름
-1|에러

11. 비밀번호 찾기
-------------------------
* url: /send_temp_password/  
임시로 비밀번호를 설정해두고 이를 이메일로 보내주는 형태 포스트 방식으로 user_id를 보낸다

|Data|Description|
---|---
|user_id|사용자아이디|

* Response
{
	"message":"Temp password sent",
	"ErrorCode":0
}

* ErrorCode

|Data|Description|
---|---
0|성공
-1|에러