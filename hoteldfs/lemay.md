# Lemay API 사용방법
Hotel 시스템에서 Lemay 사용자로 회원가입할 때, 로그인 할 때, 회원정보 변경시에는 사용하는 DB


## 공통사항
* URL 체계(URL 체계의 경우 차후에 변경 될 수 있다는 점을 고려해서 함수로 분리 필요합니다. )
  * http://www.lemaydfs.com/admin/index.php?route=[경로명]&[파라미터key1]=[파라미터value1]&[파라미터key2]=[파라미터value2]  
* 공통파라미터 
  * token
    * md5를 통해 구한 값으로 모든 API 마다 구하는 방법을 명시해 두었습니다. 차후에 보안을 위해 더 강화될 수 있다는 점을 고려해서 함수로 분리 필요합니다. 
* 모든 Methoud 는 POST 형입니다. 


## 회원가입 API
* /admin/index.php?route=api/user/add&totken=[token]
* 
| 파라미터 | 설명 |
| ------------- |:-------------:|
| token | md5("user/add" + "vizz") |
| firstname | 실제 이름 | 
| email | 실제 이름 | 
| tellephone | 전화번호 | 
| wechat | wechat 아이디 | 
| language_id | 1 : 영어, 2 : 중국어 |

## 로그인 API
* /admin/index.php?route=api/user/login&totken=[token]
* 
| 파라미터 | 설명 |
| ------------- |:-------------:|
| token | md5("user/login" + "vizz") |
| type | "email"  로 전달 할 것.  | 
| password | password | 

* 로그인 이 후 response 받는 형식

| 파라미터 | 설명 |
| ------------- |:-------------:|
| customer_id | 다른 API 를 보낼 때 필요한 값이므로 <br/>꼭 저장해 두어야 한다.  |
| token | 다른 API 를 보낼 때 customer_token 이라는<br/> 값으로 보내는 값이므로 꼭 저장대 두어야 한다.   | 



## 회원정보 수정 API
* /admin/index.php?route=api/user/edit&totken=[token]
* 
| 파라미터 | 설명 |
| ------------- |:-------------:|
| token | md5("user/edit" + "vizz") |
| customer_id | 로그인시 받은  customer_id  | 
| firstname | 실제 이름 | 
| email | 이메일 | 
| telephone | telephone | 
| wechat | wechat 아이디 | 
| status | 1 : Enabled, 0 : Disabled |
| language_id | 1 : 영어, 2 : 중국어 |


## 패스워드 변경  API
* /admin/index.php?route=api/user/editPassword&totken=[token]
* 
| 파라미터 | 설명 |
| ------------- |:-------------:|
| token | md5("user/editPassword" + "vizz") |
| customer_id | 로그인시 받은  customer_id  | 
| password | 현재 password | 
| new_password | 변경하려는 password | 
| language_id | 1 : 영어, 2 : 중국어 |

## 패스워드 변실  API
* /admin/index.php?route=api/user/forgetPassword&totken=[token]
* 
| 파라미터 | 설명 |
| ------------- |:-------------:|
| token | md5("user/editPassword" + "vizz") |
| email | 가입된 이메일 | 

* 해당 API 호출시 가입된 이메일로 인증 메일이 전달됩니다. 





