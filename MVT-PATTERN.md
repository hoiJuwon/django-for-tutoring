# MVT Pattern

- django 는 웹 프로그램 개발 시 일반적으로 언급되는 MVC 패턴을 따른다.
- MVC 패턴이란?
  - 데이터(Model), 사용자 인터페이스(View) , 데이터를 처리하는 로직(Controller)을 구분해서 한 요소가 다른 요소들에 영향을 주지 않도록 설계하는 방식
- django framework 에서는 View를 Template, Controller 는 View 라고 표현하며, MVC 를 MVT(Model-View-Template) 패턴이라고 한다.

### Model 요약

- 데이터베이스에 저장되는 데이터

### Template 요약

- 사용자에게 보여지는 interface

### View 요약

- 실질적으로 프로그램 로직이 동작하여 데이터를 가져오고 적절하게 처리한 결과를 Template 에 전달하는 역할

## MVT 패턴에 따라 처리하는 과정

1. 클라이언트로부터 request을 받으면 URLconf를 이용하여 URL 을 분석
2. URL 분석 결과를 통해 해당 URL 에 대한 처리를 담당할 View 를 결정
3. View 는 자신의 로직을 실행하면서, 만일 데이터베이스 처리가 필요하면 Model 을 통해 처리하고, 그 결과를 반환
4. View 는 자신의 로직 처리가 끝나면 Template 을 사용하여 클라이언트에 전송할 HTML 파일을 생성
5. View 는 최종 결과로 HTML 파일을 클라이언트에게 보내 응답

## Model - 데이터베이스 정의

- django 는 ORM(Object-Relational Mapping) 기법을 사용하여 애플리케이션에서 사용할 데이터베이스를 class로 매핑해서 코딩할 수 있다. 즉, 하나의 Model class 는 데이터베이스의 하나의 table 에 매핑되고, Model class 의 속성은 table 의 column 에 매핑된다.

- ORM 이란?
  - 객체와 관계형 데이터베이스를 연결해주는 역할.
  - 기존의 웹 프로그래밍에서 데이터베이스에 접근하려면 직접 SQL 언어를 사용해서 요청해야했지만 ORM 에서는 데이터배이스 대신에 객체를 사용해 데이터를 처리 할 수 있음.

```
from django.db import models

class Person(models.Model) :
   first_name = models.CharField(max_length=30)
   last_name = models.CharField(max_length=30)
```

## URLconf - URL 정의

- 클라이언트로부터 request를 받으면, 가장 먼저 request에 들어있는 URL을 분석한다. 즉, request에 들어있는 URL 이 urls.py 에 정의된 URL 패턴과 매칭되는지를 분석한다.
- URL을 정의하기 위해서는 urls.py 파일에 URL 과 views 를 매핑하는 파이썬 코드를 작성해야한다.

```
from django.urls import path

from . import views

urlpatterns = [
    path('', views.home, name="home"),
    path('/articles', views.articles, name="articles'),
]
```

## View - 로직 정의

- 일반적으로 웹 요청을 받아서 데이터베이스 접속 등 해당 애플리케이션의 로직에 맞는 처리를 하고, 그 결과 데이터를 HTML 로 변환하기 위하여 템플릿 처리를 한 후에, 최종 HTML로 된 응답 데이터를 웹 클라이언트로 반환하는 역할을 한다.

```
from django.http import HttpResponse
import datetime

def current_datetime(request) :
    now = datetime.new()
    html = "<html><body>It is now %s.</body></html>" % now

    return HttpResponse(html)

```

- View 의 함수는 첫 번째 인자로 HttpRequest 객체를 받는다. 그리고 필요한 처리를 한 후에 최종적으로 HttpResponse 객체를 반환한다.
