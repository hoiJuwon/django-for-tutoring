# settings.py 설정

- 프로젝트에 필요한 설정값들은 settings.py 파일에 지정한다.
- 프로젝트의 전반적인 사항 / 루트 디렉토리를 포함한 각종 디렉토리의 위치 / 로그의 형식 / 프로젝트에 포함된 애플리케이션의 이름 등이 포함된다.

## 기본적으로 체크해야하는 사항

1. ALLOWED_HOSTS 항목의 DEBUG 설정

   - django 는 "DEBUG = TRUE" 이면 개발모드로, FALSE 이면 운영모드로 인식한다. 운영 모드인 경우에는 반드시 ALLOWED_HOSTS 에 서버의 IP 나 도메인을 연결해야한다. 개발 모드인 경우에는 값을 지정하지 않으면 기본적으로 로컬이 연결된다.

2. 프로젝트에 포함되는 애플리케이션들은 모두 설정 파일에 등록되어야 한다.

   - 예를 들어, 'myapp' 애플리케이션을 만든 경우, 'myapp'만 등록해도 되지만, 애플리케이션의 설정 클래스로 등록하는 것이 가장 정확한 방법이다. myApp 의 설정 클래스는 django startapp myapp 시에 자동 생성된 apps.py 파일에 MyappConfig라고 정의 되어 있다.

3. 프로젝트에서 사용할 데이터베이스 엔진 설정을 확인한다.

   - SQLite3 가 default로 사용되도록 설정되어 있는데, 만약 다른 데이터베이스(MySQL, PostgreSQL)을 사용하고 싶다면 settings.py 파일에서 수정해주면 된다. 아닐 경우 변경 할 필요 없이 확인만 하면 된다.

   ```
    # Database
    # https://docs.djangoproject.com/en/2.0/ref/settings/#databases

    DATABASES = {
        'default' : {
            'ENGINE' : 'django.db.backends.sqlite3',
            'NAME' : os.path.join(BASE_DIR, 'db.sqlite3'),
        }
    }

   ```

4. 타임존을 한국 시간으로 변경한다.
