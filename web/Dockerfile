FROM ubuntu:18.04 as build
ENV prj_path=/home/app42
RUN apt-get update \
    && apt-get install -y default-jdk git maven \
    && apt-get clean
RUN git clone https://github.com/shephertz/App42PaaS-Java-MySQL-Sample.git $prj_path
WORKDIR $prj_path
RUN mvn package \
    && mv ./target/App42PaaS-Java-MySQL-Sample-0.0.1-SNAPSHOT.war ./target/app42.war

FROM tomcat:8.0-alpine
COPY --from=build /home/app42/target/app42.war /usr/local/tomcat/webapps
COPY Config.properties /usr/local/tomcat/ROOT/