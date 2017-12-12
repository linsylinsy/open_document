# Lemay App Scheme

모바일 애플리케이션 및 브라우저에서 르메이 앱을 실행시키는 custom URL scheme을 사용해보세요. “http://”, “ftp://”, “market://”과 같은 문자열을 url scheme이라 부릅니다. 
url scheme을 통해 앱이 실행되는 방식은 다음과 같습니다.

웹페이지에서 하이퍼링크 클릭 시 url scheme이 system에 전달됨
system에서 전달된 url scheme을 보고 실행 가능한 앱이 있는지 확인
해당 url scheme을 받을 수 있는 앱이 있다면 앱을 실행시키며 이 url을 함께 전달
앱이 실행되면서 url에 포함된 내용을 참조해서 특정 기능을 수행함

## URL 스킴구성

1.기본형식
르메이 앱을 실행시키기 위해서는 다음과 같은 custom url을 구성해야합니다.
```
lemayapp://명령어?파라미터=옵션
```
2.Intent Scheme
안드로이드에서는 intent scheme을 이용할 수도 있습니다. 다음과 같은 형식의 custom url을 구성하면, 앱이 설치되어 있지 않을 때 자동으로 구글 플레이 설치 페이지로 이동합니다.
```
Intent://명령어?파라미터=옵션

#Intent;scheme=lemayapp;action=android.intent.action.VIEW;category=android.intent.category.BROWSABLE;package=com.linsy.lemay;end

```

## URL 스킴적용 예제

### 앱실행

 * Sample
```
lemayapp://
```

### 상품검색

| 기능  | 명령어  | 파라미터=옵션  |
|---|---|---|
| 상품검색  |  search | product={product_id}  |
| 이벤트검색  |  search | event={event_id}  |

 * Sample
```
//상품번호 1의 상품 상세정보를 표시
lemayapp://search?product=1

//이벤트번호 10의 이벤트상세화면을 표시
lemayapp://search?event=1

```
