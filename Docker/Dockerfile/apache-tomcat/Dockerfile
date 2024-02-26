
# Use Ubuntu as the base image
FROM ubuntu:latest

# Install dependencies
RUN apt-get update && \
    apt-get install -y default-jdk wget unzip

# Setup environment variables
ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk-amd64
ENV CATALINA_HOME /opt/tomcat
ENV PATH $CATALINA_HOME/bin:$JAVA_HOME/bin:$PATH

# Download and install Tomcat
ARG TOMCAT_VERSION=9.0.54
RUN wget -q https://downloads.apache.org/tomcat/tomcat-9/v$TOMCAT_VERSION/bin/apache-tomcat-$TOMCAT_VERSION.tar.gz && \
    tar -xvf apache-tomcat-$TOMCAT_VERSION.tar.gz && \
    mv apache-tomcat-$TOMCAT_VERSION $CATALINA_HOME && \
    rm apache-tomcat-*.tar.gz && \
    chmod +x $CATALINA_HOME/bin/*.sh

# Set work directory
WORKDIR $CATALINA_HOME

# Optional: Copy your webapp into the webapps directory
COPY ./your-webapp.war $CATALINA_HOME/webapps/

# Clean up APT when done
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Expose the default Tomcat port
EXPOSE 8080

# Start Tomcat from the specified work directory
CMD ["catalina.sh", "run"]


