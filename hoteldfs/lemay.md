# Lemay DB 사용방법
Hotel 시스템에서 Lemay 사용자로 회원가입할 때, 로그인 할 때, 회원정보 변경시에는 직접 DB를 접근해서 수정하고 패스워드 분실은 API를 통하여 접근한다. 

## Lemay 의 DB 접근
* Hotel 시스템과 동일한 DB 접근 주소, DB 유저, DB 패스워드를 이용하고 스키마만 lemay 로 접속한다.

## Hasing 된 패스워드 체계
* PBKDF2 
* Hash function : SHA256 알고리즘 적용
* Salt : ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789 글자중 9자리
  * ex) vyTUcCVVD, 8vPgc3QZP
* Iternation : 1000회
* DLen : 20byte
* 최종 결과는 20byte를 소문자 hex string 으로 변환한 40글자
* 참고 : http://d2.naver.com/helloworld/318732
* ex) 예1
  * salt : jA3BAWv9F
  * password : abcd1234
  * 결과 : c059b2879ac9fbe11469f0340c14573fc8f6a6e5
* ex) 예2
  * salt : jA3BAWv9F
  * password : ABCD1234
  * 결과 : 6ac6860b93ae64fadb0bed24604506a449bd81d1

## 회원가입 유저테이블
 * 테이블명 : customer
 * __customer_id__ : Primary Key 로 Auto Increasement 값
 * __customer_group_id__ : 2로 지정할 것
 * store_id : 0으로 지정할 것
 * __firstname__ : 회원가입시 이름을 입력할 경우 넣고 안 넣을 경우 empty string("") 처리
 * lastname : empty string 처리 
 * email : 가입된 이메일
 * password : 위에서 설명한 Hasing 된 패스워드 체계의 결과
 * newletter : 0 처러
 * address_id : 0 처리
 * ip : 회원가입한 클라이언트 IP
 * status : 1
 * approved : 1
 * safe : 1
 * date_added : 회원가일 l일시(UTC 기준)
 * lang_id : 클라이언트 사용언어 ( 1: 영어, 2 : 중국어)
 * type : email
 * hotel_id : 0
 * change_pwd_time : 0
 * 나머지 인자는 emptry string 으로 처리

## 로그인 체크
 * 테이블명 : customer
 * loginToken 같과 같은지 비교한다. 
 * 로그인시 0~9, A-Z, a-z로 이루어진 25자리 랜덤스트링을 생성하고 이 값을 저장하는 형태임

 ## 패스워드 분실시 
  * 