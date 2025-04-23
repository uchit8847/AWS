FROM ubuntu:22.04
LABEL dev="Rajatz"

# Install necessary packages
RUN apt update -y && \
    apt install -y unzip default-jdk && \
    apt clean && \
    rm -rf /var/lib/apt/lists/*

# Download and extract Tomcat
ADD https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.83/bin/apache-tomcat-9.0.83.zip /opt
RUN unzip /opt/apache-tomcat-9.0.83.zip -d /opt

# Set up Tomcat and deploy the WAR file
WORKDIR /opt/apache-tomcat-9.0.83/
ADD https://s3-us-west-2.amazonaws.com/studentapi-cit/student.war /opt/apache-tomcat-9.0.83/webapps/
ADD https://s3-us-west-2.amazonaws.com/studentapi-cit/mysql-connector.jar /opt/apache-tomcat-9.0.83/lib/mysql-connector.jar
COPY context.xml /opt/apache-tomcat-9.0.83/conf/context.xml

# Set permissions and run Tomcat
RUN chmod +rwx /opt/apache-tomcat-9.0.83/bin/*.sh

CMD ["/opt/apache-tomcat-9.0.83/bin/catalina.sh", "run"]

EXPOSE 8080

