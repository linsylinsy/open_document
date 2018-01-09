# deprecated

<del>
# Lemay API 사용방법

Hotel 시스템에서 Lemay 사용자로 회원가입할 때, 로그인 할 때, 회원정보 변경시에는 사용하는 DB


## 공통사항
* URL 체계(URL 체계의 경우 차후에 변경 될 수 있다는 점을 고려해서 함수로 분리 필요합니다. )
  * http://www.lemaydfs.com/admin/index.php?route=[경로명]&[파라미터key1]=[파라미터value1]&[파라미터key2]=[파라미터value2]  
* 공통파라미터 
  * token
    * md5를 통해 구한 값으로 모든 API 마다 구하는 방법을 명시해 두었습니다. 차후에 보안을 위해 더 강화될 수 있다는 점을 고려해서 함수로 분리 필요합니다. 
* 모든 Methoud 는 <B style="color:red"> POST </B> 형입니다. 

## 테스트페이지
* http://www.lemaydfs.com/test/yoon_test.php?pw=[pw]
* [pw] 는 DB(yoon)의 패스워드와 동일합니다. 


## 회원가입 API
* /admin/index.php?route=api/user/add&totken=[token]
* 
| 파라미터 | 설명 |
| ------------- |:-------------:|
| token | md5("user/add" + "vizz") |
| apptype | "hotel" | 
| language_id | 1 : 영어, 2 : 중국어 |
| name | 이름 | 
| email | 이메일 | 
| password | password | 
| telephone | 전화번호 | 
| wechat | wechat 아이디 | 
| hotel_check_out | check out 날짜 | 
| language_id | 1 : 영어, 2 : 중국어 |

*  response 받는 형식

| 파라미터 | 설명 |
| ------------- |:-------------:|
| success | 성공시에만 전달됨  |
| error |  실패시에만 전달됨, 실패이유 |
| customer_id | 회원번호, 성공시에만 전달됨   | 

* 성공시<br/>
{"success":"Add Successed","customer_id":57}
* 실패시<br/>
{"error":"Parameter error"}

## 로그인 API
* /admin/index.php?route=api/user/login
* 
| 파라미터 | 설명 |
| ------------- |:-------------:|
| token | md5("user/login" + "vizz") |
| apptype | "hotel" | 
| language_id | 1 : 영어, 2 : 중국어 |
| type | "email"  로 전달 할 것.  | 
| email | 이메일 | 
| password | password | 

*  response 받는 형식

| 파라미터 | 설명 |
| ------------- |:-------------:|
| customer_id | 다른 API 를 보낼 때 필요한 값이므로 <br/>꼭 저장해 두어야 한다.  |
| token | 다른 API 를 보낼 때 <B style="color:red">customer_token  </B>이라는<br/> 값으로 보내는 값이므로 꼭 저장대 두어야 한다.   | 

* 성공시 <br/>
{"success":"Login success","customerInfo":{"customer_id":"57","type":"email","name":"이름","email":"nahanmil+abc@gmail.com","telephone":"01012345678","newsletter":"0","hotel_id":"0","hotel_name":"","hotel_address":"","hotel_room":"","hotel_check_in":"","hotel_check_out":"","token":"EUcGGgKCHXIb8QIMliLNpu6JO"}}
* 실패시<br/>
{"error":"Parameter error"}


## 회원정보 가져오기 API
* /admin/index.php?route=api/user/getUserInfo

| 파라미터 | 설명 |
| ------------- |:-------------:|
| token | md5("user/getUserInfo" + "vizz") |
| apptype | "hotel" | 
| language_id | 1 : 영어, 2 : 중국어 |
| customer_id | 로그인시 받은  customer_id  | 
| customer_token | 로그인시 받은  token  | 


*  response 받는 형식

| 파라미터 | 설명 |
| ------------- |:-------------:|
| name | 이름  |
| telephone | 전화번호  |
| email | email  |
| hotel_check_out | 체크아웃 시간  |


* 성공시 <br/>
{"success":"Get UserInfo","customer_id":"57","type":"email","name":"이름2","email":"nahanmil+abc@gmail.com","telephone":"01012345678","newsletter":"0","language_id":"1","status":"1","wechat":"","hotel_id":"0","hotel_name":"","hotel_address":"","hotel_room":"","hotel_check_in":"","hotel_check_out":"2018-03-01"}
* 실패시<br/>
{"error":"Parameter error"}

## 회원정보 수정 API
* /admin/index.php?route=api/user/edit

| 파라미터 | 설명 |
| ------------- |:-------------:|
| token | md5("user/edit" + "vizz") |
| apptype | "hotel" | 
| language_id | 1 : 영어, 2 : 중국어 |
| customer_id | 로그인시 받은  customer_id  | 
| customer_token | 로그인시 받은  token  | 
| name | 실제 이름 | 
| telephone | telephone | 
| wechat | wechat 아이디 | 
| hotel_check_out | check out 날짜 | 
| status | 1 : Enabled, 0 : Disabled |

* 성공시 <br/>
{"success":"Update Successed","token":"2KvT3MXsHXp0kflGIrKoDMgn5"}
* 실패시<br/>
{"error":"Parameter error"}

## 패스워드 변경  API
* /admin/index.php?route=api/user/editPassword

| 파라미터 | 설명 |
| ------------- |:-------------:|
| token | md5("user/editPassword" + "vizz") |
| apptype | "hotel" | 
| customer_id | 로그인시 받은  customer_id  | 
| customer_token | 로그인시 받은  token  | 
| password | 현재 password | 
| new_password | 변경하려는 password | 



* 성공시 <br/>
{"success":"Update Successed"}
* 실패시<br/>
{"error":"Parameter error"}


## 패스워드 분실  API
* /admin/index.php?route=api/user/forgetPassword

| 파라미터 | 설명 |
| ------------- |:-------------:|
| token | md5("user/editPassword" + "vizz") |
| apptype | "hotel" |
| language_id | 1 : 영어, 2 : 중국어 |
| email | 가입된 이메일 | 


* 성공시 <br/>
{"success":"Send Successed"}
* 실패시<br/>
{"error":"Parameter error"}
* 해당 API 호출시 가입된 이메일로 인증 메일이 전달됩니다. 

</del>



