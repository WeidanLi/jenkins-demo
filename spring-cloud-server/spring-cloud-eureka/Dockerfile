FROM 192.168.1.53:5000/java8
MAINTAINER WeidanLi <toweidan@126.com>

ENTRYPOINT ["/usr/bin/java", "-jar", "/usr/share/myservice/myservice.jar"]

ARG JAR_FILE
ADD target/${JAR_FILE} /usr/share/myservice/myservice.jar