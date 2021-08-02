FROM tomcat:8.5.43-jdk8-adoptopenjdk-hotspot

COPY /conf/* /usr/local/tomcat/conf/
COPY /META-INF/context.xml /usr/local/tomcat//webapps/manager/META-INF/context.xml
WORKDIR /usr/local/tomcat/bin

CMD ["catalina.sh", "run"]
