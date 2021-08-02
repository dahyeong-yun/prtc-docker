# 단일 Tomcat 컨테이너

## Dokcer
- 실행중인 컨테이너에 접속하려면?
  - `exec`
  - `run` 날리는 시점에 shell로 접속할 수 없나?
- `run`할 때 `-it`랑 `-d` 옵션은 무슨 의미?

- 명령어 참고
  - https://velog.io/@conatuseus/2019-12-06-0012-%EC%9E%91%EC%84%B1%EB%90%A8-u3k3svyfa8#attach-%EB%AA%85%EB%A0%B9%EC%9C%BC%EB%A1%9C-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88%EC%97%90-%EC%A0%91%EC%86%8D%ED%95%98%EA%B8%B0

## Tomcat
- docker tag
  - tomcat 구동시 어떨 때는 초기 예시 파일이 있고, 어떨 때는 없어서 버전을 찾는 것도 시간이 좀 소요 되었다.
  - tomcat 버전 별로 아예 webapps 초기 파일이 없는 경우도 있는 것 같다.
  - tomcat의 docker hub 페이지에서 [tag 리스트](https://hub.docker.com/_/tomcat/?tab=tags&page=1&ordering=last_updated)를 검색해 볼 수 있다.
    - 여기서 사용한 tag는 `8.5.43-jdk8-adoptopenjdk-hotspot`이다.

- manager 페이지 접속
  - 관리자 페이지 접속에도 세팅이 조금 필요 했다.
    - 관리자 페이지 접속 시에 403이 뜨면서, tomcat 사용자와 context.xml 파일을 수정하라는 식의 메세지가 떴다.
    - 공식 문서 : https://tomcat.apache.org/tomcat-8.5-doc/manager-howto.html
    - https://stackoverflow.com/questions/38551166/403-access-denied-on-tomcat-8-manager-app-without-prompting-for-user-password/41286101
  - 참고로, error log가 아래와 같이 뜨긴 했었다.
    ```html
    403 Access Denied
    You are not authorized to view this page.

    By default the Manager is only accessible from a browser running on the same machine as Tomcat. If you wish to modify this restriction, you'll need to edit the Manager's context.xml file.

    If you have already configured the Manager application to allow access and you have used your browsers back button, used a saved book-mark or similar then you may have triggered the cross-site request forgery (CSRF) protection that has been enabled for the HTML interface of the Manager application. You will need to reset this protection by returning to the main Manager page. Once you return to this page, you will be able to continue using the Manager application's HTML interface normally. If you continue to see this access denied message, check that you have the necessary permissions to access this application.

    If you have not changed any configuration files, please examine the file conf/tomcat-users.xml in your installation. That file must contain the credentials to let you use this webapp.

    For example, to add the manager-gui role to a user named tomcat with a password of s3cret, add the following to the config file listed above.

    <role rolename="manager-gui"/>
    <user username="tomcat" password="s3cret" roles="manager-gui"/>
    Note that for Tomcat 7 onwards, the roles required to use the manager application were changed from the single manager role to the following four roles. You will need to assign the role(s) required for the functionality you wish to access.

    manager-gui - allows access to the HTML GUI and the status pages
    manager-script - allows access to the text interface and the status pages
    manager-jmx - allows access to the JMX proxy and the status pages
    manager-status - allows access to the status pages only
    The HTML interface is protected against CSRF but the text and JMX interfaces are not. To maintain the CSRF protection:

    Users with the manager-gui role should not be granted either the manager-script or manager-jmx roles.
    If the text or jmx interfaces are accessed through a browser (e.g. for testing since these interfaces are intended for tools not humans) then the browser must be closed afterwards to terminate the session.
    For more information - please see the Manager App How-To.
    ```