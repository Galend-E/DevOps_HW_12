FROM ubuntu:18.04 as build
ENV prj_path=/home/app42
RUN apt-get update \
    && apt-get install -y default-jdk git maven \
    && apt-get clean
RUN git clone https://github.com/shephertz/App42PaaS-Java-MySQL-Sample.git $prj_path
RUN mvn package -f $prj_path/pom.xml
COPY Config.properties $prj_path/target
WORKDIR $prj_path/target
RUN mv App42PaaS-Java-MySQL-Sample-0.0.1-SNAPSHOT.war app42.war \
    && jar uf app42.war Config.properties

FROM tomcat:6.0-alpine
COPY --from=build /home/app42/target/app42.war /usr/local/tomcat/webapps