FROM jboss/wildfly:9.0.2.Final
MAINTAINER Jalel HAZBRI "jalel.hazbri@gmail.com"

# ENV VARIABLES 
ENV WILDFLY_HOME /opt/jboss/wildfly
ENV WILDFLY_VERSION 9.0.2.Final
ENV MYSQL_HOST 127.0.0.1:3306
ENV MYSQL_USER mjhazbri
ENV MYSQL_PASSWORD mjhazbri
ENV MYSQL_DATABASE mjhazbri


# Add standalone xml file
COPY standalone-mjhazbri.xml ${WILDFLY_HOME}/standalone/configuration/standalone-mjhazbri.xml

# Get MySQL driver
ADD https://repo1.maven.org/maven2/mysql/mysql-connector-java/5.1.39/mysql-connector-java-5.1.39.jar ${WILDFLY_HOME}/modules/com/mysql/jdbc/main/mysql-connector-java-5.1.39-bin.jar

# MYSQL JDBC Module
COPY module-mysql.xml ${WILDFLY_HOME}/modules/com/mysql/jdbc/main/module.xml

# Add console admin user
RUN ${WILDFLY_HOME}/bin/add-user.sh mjhazbri mjhazbri  --silent

# Ports
EXPOSE 8080 9990

# Volumes
VOLUME ${WILDFLY_HOME}/standalone/deployments/
VOLUME ${WILDFLY_HOME}/standalone/log/

# RUN script
COPY start-wildfly.sh ${WILDFLY_HOME}/bin/start-wildfly.sh
USER root
RUN chmod +x ${WILDFLY_HOME}/bin/start-wildfly.sh
#USER jboss

ENTRYPOINT ["sh", "-c", "${WILDFLY_HOME}/bin/start-wildfly.sh"]
